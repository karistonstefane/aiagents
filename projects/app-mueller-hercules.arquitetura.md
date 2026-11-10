# Arquitetura: App - Mueller e Hercules

> Mantido pelo Dev no mesmo ciclo do PR do projeto (PR complementar no `aiagents`) quando a mudança afetar a arquitetura. Fatos verificados no repositório `checkstore/app-b2b-connect` (`origin/main`, commit `8e0c3c4`, 09/11/2026) e nas decisões do Kariston. O que não se sabe: `não informado`. Detalhes técnicos de cada extensão estão nos READMEs dela e no `AGENTS.md`/`docs/` do repositório.

## Visão geral

- Custom app B2B **multi-tenant** da Checkstore que atende duas lojas Shopify Plus 100% B2B: Mueller (`totvsle-mueller.myshopify.com`) e Hércules (`totvsle-herculesmotores.myshopify.com`).
- Cobre cadastro B2B de empresas, integração com SAP no checkout (simulação, impostos, financeiro, condições de pagamento), carrinhos salvos, importação de carrinho, materiais técnicos e validações de checkout.
- Deploy feito pelo **Victor** (`victorcesc`), que também revisa os PRs.

## Stack e repositório

- **Repositório:** `checkstore/app-b2b-connect` (local `~/projects/ca-herculesmueller`)
- **Branch base:** `main`
- **Stack:** React Router 7 (template Shopify `@shopify/shopify-app-react-router`), App Bridge React, Polaris (tipos), Node ≥ 20.19, Vite, Vitest, ESLint/Prettier.
- **Banco:** MongoDB (`mongodb` no `package.json`).
- **Hospedagem:** Docker (`Dockerfile`, `docker-compose.yml`), um container por tenant (ex.: `b2b-app-hercules`) com env por tenant (ex.: `.env.hercules`, fora do Git). URLs: `https://mueller.fullcomm.app` e `https://hercules.fullcomm.app`.
- **Configs Shopify:** `shopify.app.toml` (Mueller, app `app-b2b-connect`) e `shopify.app.app-b2b-connect-hercules.toml` (Hércules). Scripts `deploy:mueller` e `deploy:hercules`.
- **Estrutura:** `app/routes/` (admin `app.*`, app proxy `app.proxy.*`, APIs `api.*`, webhooks `webhooks.*`), `app/services/`, `app/lib/` (inclui `tenant.server.ts` e catálogos por tenant, ex.: `payment-terms-catalog.mueller.ts` / `.hercules.ts`), `app/middleware/`, `extensions/` (workspaces npm), `docs/`, `scripts/`, `fixtures/`.

## Integrações

- **SAP:** simulação de checkout (`api.checkout.simulate`, `checkout-simulate.server`), sincronização financeira (`api.checkout.financial-sync`, `app.proxy.financeiro.sync`), condições de pagamento (ZTERM, MUEL-207), impostos SAP no pedido (MUEL-260), consulta de endereço no cadastro B2B (`SAP_ADDRESS_CONSULT_ENABLED` por tenant; `false` desliga).
- **EOX:** leads/cadastro (`app.proxy.eox.leads`, `b2b-company-registration-eox`). Finalidade de negócio exata: não informado.
- **Shopify Flow:** triggers `cadastro-b2b-recebido` e `data-change-requested`.
- **Webhooks:** `orders/create` (API 2026-07), `app/uninstalled`, `app/scopes_update`.
- **App proxy:** `/apps/b2b` → empresas/CNPJ, coligação, carrinhos salvos, importação de carrinho, materiais técnicos, financeiro, leads.

## Apps instalados e extensões

Extensões em `extensions/` (na `main`):

- **Theme app extension:** `b2b-company-registration` (cadastro B2B de empresas, consulta SAP para endereço).
- **Checkout UI:** `checkout-carrier`, `checkout-cnpj-lock`, `checkout-delivery-mode`, `checkout-delivery-split`, `checkout-financial-sync`, `checkout-incoterm`, `checkout-payment-terms`, `checkout-scheduled-delivery`, `checkout-tax-display`.
- **Customer account UI:** `customer-account-order-taxes`, `order-product-image-download`, `profile-data-change`.
- **Functions:** validações de carrinho `checkout-cnpj-validation`, `checkout-financial-status`, `checkout-sap-business-error-gate`, `minimum-price`; customização de pagamento `payment-credit-gate`.
- **Flow triggers:** `cadastro-b2b-recebido`, `data-change-requested`.
- **Em PR #75, ainda não mergeado:** `b2b-segment-discount` (Discount Function de **produto**, classe PRODUCT, desconto por linha; ver abaixo). O PR também muda o `minimum-price` para checar o mínimo antes dos descontos de linha.

## Dados

- **Shop metafield** `app.minimum_price` (number_decimal): preço mínimo para compra (nas duas configs).
- **Order metafield** `app.impostos_sap` (json): impostos SAP estimados no checkout, gravado pelo webhook `orders/create`, lido na área do cliente (MUEL-260, config da Mueller).
- **Company Location metafields de segmento:** `checkstore.regional`, `checkstore.regiao`, `checkstore.setor`, `checkstore.equipe`, `checkstore.grupo_clientes` (vêm do SAP).
- **Organização de vendas (VKORG):** por produto, no `product.vendor` (ex.: Hércules `4000`/`5000`, Mueller `2000`/`3000`; allowlist em `tenant.server.ts`). É a fonte usada pelo simulate SAP (um simulate por VKORG em carrinho misto) e pela function de desconto por segmento.
- **Discount metafield** `$app:b2b-segment-discount-config` (json, PR #75): `{ version: 1, enabled, groups: [{ id, name, metafieldKey, values, percentage, salesOrgs }] }`. `enabled` é o gate da flag `SEGMENT_DISCOUNT_ENABLED` lido pela function; `salesOrgs` vazio = todas as orgs.
- Metaobjects: o app tem escopo para definir/escrever metaobjects; tipos: não informado.
- **Escopos atuais:** incluem `read/write_companies`, `write_customers`, `write_orders`, `write_draft_orders`, `write_payment_customizations`, `write_metaobjects`, `write_app_proxy` (lista completa nos `.toml`).

## Módulos do app

- **Admin (App Home):** `app._index`, `app.payment-terms`, `app.payment-customization.$functionId.$id`, `app.activate-payment-credit-gate`, `app.additional`.
- **Cadastro B2B / empresas:** `api.companies*`, `app.proxy.companies*`, coligação por CNPJ.
- **Checkout SAP:** `checkout-simulate`, cache de respostas, fingerprint de carrinho, erros de simulação.
- **Carrinhos salvos e importação de carrinho (xlsx):** `app.proxy.saved-carts*`, `app.proxy.cart-import.*`, `cart-import.server`.
- **Materiais técnicos / imagens de produto:** `app.proxy.materiais.*`, `api.customer-account.product-image`.
- **Alteração de dados cadastrais:** `api.customer-account.data-change` + Flow trigger.

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| não informado | Um único repositório e um único código para as duas lojas, com uma config `.toml` por loja e env por tenant. | Facilitar o desenvolvimento; as duas lojas usam o mesmo app. | não informado |
| 2026-11-10 | **Desconto por segmento (versão inicial do PR #75, substituída na linha abaixo):** um único desconto automático do app (Discount Function, classe **ORDER**), config JSON de grupos num metafield `$app` do próprio discount; grupos = metafield de segmento da Company Location + valores, cada um com uma %; se a location casar com mais de um grupo vale o **maior**; sem empresa ou sem grupo, sem desconto; aplica por cima do catálogo/price list; flag `SEGMENT_DISCOUNT_ENABLED`; novo escopo `write_discounts`. | Lojas 100% B2B sem cupons; limite de descontos automáticos por loja; uma implementação para dois projetos. | MUEL-270 / HCL-236 |
| 2026-11-10 | **Desconto por segmento na classe PRODUCT (por linha)**, criado com `context: { all: ALL }`; a function filtra por `purchasingCompany`. Desconto antigo na classe ORDER é migrado pelo botão de setup (`discountAutomaticAppUpdate`). | Kariston: "Vamos precisar mudar para o desconto ser aplicado no produto e não no pedido, assim o produto já vai com desconto pro SAP e para o calculo de impostos do SAP." Descontos B2B já vêm ativos nas lojas elegíveis (Especialista Shopify). | MUEL-270 / HCL-236 (PR #75) |
| 2026-11-10 | **Grupos por organização de vendas:** cada grupo tem `salesOrgs` (VKORG), comparado com o `product.vendor` de cada linha; vazio = todas; carrinho misto 4000/5000 resolve por linha. | Kariston: "Podemos colocar para definir por organizações também." | MUEL-270 / HCL-236 (PR #75) |
| 2026-11-10 | **Gate da flag dentro da function:** `enabled` na config; com a flag desligada, abrir a tela grava `enabled: false` e a function para de aplicar. | Ressalva do Revisor: desligar a flag não removia o desconto já criado. | MUEL-270 / HCL-236 (PR #75) |
| 2026-11-10 | **Pedido mínimo antes do desconto:** `minimum-price` soma `cart.lines[].cost.subtotalAmount` (antes dos descontos de linha) em vez de `cart.cost.subtotalAmount`. Vale para qualquer desconto de produto. | Kariston: "Pedido Minimo deve ser checato antes." | MUEL-270 / HCL-236 (PR #75) |
| 2026-11-10 | Percentual de 0,01 a 100 (até 2 casas), sem teto menor; sem exclusão de segmentos por desconto em dobro; impostos com valor descontado em nova tarefa. | Kariston: "Não precisa ter teto, se o usuário colocar 100% é problema dele." / "O SAP não traz descontos para a Shopify." / "Os impostos devem ser calculados com o valor já com desconto, mas vamos tratar em uma nova tarefa." | MUEL-270 / HCL-236 (PR #75) |

## Armadilhas conhecidas

- `shopify app deploy` libera a versão nas duas lojas; use os scripts por loja. Deploy só pelo Victor.
- Novos escopos exigem reautorização do app em **cada** loja.
- Configurações por loja (discount automático, metafields de config) precisam ser criadas em cada loja.
- Env por tenant fica fora do Git; um `restart` do container não relê o env (use `docker compose up -d --force-recreate <serviço>`).
- Cadastro B2B na Hércules gerando "Endereço Pendente": a consulta SAP estava desligada no tenant (`disabled for this tenant`) e depende do `IV_CONS_ENDERECO` no SAP.
- Desconto automático do segmento não combina com descontos de pedido nem de produto: em cada linha a Shopify aplica um só.
- **OMS → SAP (oms-backend, do Victor):** `createSAPPayload` envia `IT_PRODUCTS[].NETWR` com `item.price` (preço cheio), mesmo com o desconto na linha (`discount_allocations`). Enquanto o OMS não mandar o valor líquido, o desconto por segmento não pode ser ligado (ver `docs/contrato-pedido-oms.md`, P7, no repo do app).
- Function de desconto por linha: cerca de 9,6M instruções com 200 linhas (limite 11M até 200 linhas, cresce acima disso). Cuidado ao adicionar campos na input query.

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| 2026-11-09 | Totais de conta/checkout (impostos SAP). | MUEL-260 / PR #73 |
| 2026-11-10 | Desconto por segmento B2B aberto, em ajustes do review do Victor. | MUEL-270, HCL-236 / PR #75 (não mergeado) |
| 2026-11-10 | PR #75 ajustado com as decisões do Kariston: classe PRODUCT (por linha) com `context: { all: ALL }`, grupos por organização de vendas (`product.vendor`), gate `enabled` na function, contagem de descontos sem derrubar a tela, pedido mínimo antes dos descontos de linha. Pendente no OMS: `NETWR` líquido. | MUEL-270, HCL-236 / PR #75 (não mergeado) |
