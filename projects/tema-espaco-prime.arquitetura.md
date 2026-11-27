# Arquitetura: Tema - Espaço Prime

> Mantido pelo Dev no mesmo ciclo do PR do projeto (PR complementar no `aiagents`) quando a mudança afetar a arquitetura. Fatos verificados no repositório `checkstore/espaco-prime` (`origin/master` em `824f3fa`, levantamento em 27/11/2026), nas tarefas do Jira EP e nas confirmações do Kariston no mesmo dia. O que não se sabe: `não informado`.

## Visão geral

- Loja da Espaço Prime (bebidas): `espaco-prime-05iifq98.myshopify.com`. Modelo: B2C com venda para CNPJ (atacado/B2B nativo da Shopify, épico EP-91 "Venda CNPJ"). Plano: **não é Shopify Plus** (Kariston, 27/11/2026); plano exato não informado.
- Domínio customizado: não informado (o e-mail de atendimento usa `espacoprime.com.br`; DNS em EP-15, Backlog).
- Tema conectado à branch `master`: "[Check] Desenvolvimento", base **Expanse 10.0.1** (Archetype Themes). É o tema **publicado (MAIN)**, id `190697963841` (confirmado em 27/11/2026): **merge na `master` = publicação**. Único outro tema: "Cópia de Expanse" (não publicado). Enquanto a loja não está em produção, não há tema de preview: o teste é feito no tema publicado depois do merge (Kariston, 27/11/2026).

## Stack e repositório

- **Repositório:** `checkstore/espaco-prime` (local `~/projects/espaco-prime`, `C:\Users\Kariston\projects\espaco-prime`). Trabalhar sempre dentro dessa pasta, sem criar pastas ou arquivos soltos na raiz de `projects`.
- **Branch base:** `master` (única branch). Fluxo: branch `feat/EP-<n>-<slug>` ou `fix/EP-<n>-<slug>`, PR contra `master`, review do bot Revisor, merge manual do Kariston.
- **Base:** tema **Expanse 10.0.1** (Archetype Themes), Online Store 2.0.
- **Estrutura:** `assets/` (232), `blocks/` (1), `config/`, `layout/` (`theme.liquid`, `password.liquid`, `gift_card.liquid`), `locales/` (14), `sections/` (71), `snippets/` (257), `templates/` (37, com `customers/`). Não há README, `shopify.theme.toml`, workflows nem `package.json`.
- **Histórico Git:** repositório criado em 19/10/2026. Até 27/11/2026 quase todos os commits na `master` vieram do Shopify bot ("Update from Shopify for theme [Check] Desenvolvimento", por Mayara Silveira, Fabiano Trichez e Denner Moraes); há um commit manual de Denner Moraes (23/10/2026, tamanho da fonte do preço do produto). A partir desta data, vale o fluxo dos bots (branch separada, PR, review).

## Integrações

- **Anymarket:** recebe os pedidos da loja. Hoje o pedido B2B chega sem o nome da empresa; nas observações vão só a inscrição estadual e o CNPJ (EP-92). Quais campos ela lê (`note_attributes`, nota, `company`/`purchasingEntity`) e se relê o pedido em `orders/updated`: não informado.
- **ERP:** integração citada na EP-92 (pega o número do endereço no lugar errado e envia o nome do formulário de endereço em vez da empresa). Qual ERP e quem mantém a integração: não informado.
- `layout/theme.liquid` não instala GTM nem scripts de terceiros além dos do tema (o `design-mode.js` da Archetype só carrega no editor). Meta, GA, GTM, Ads, Search Console e Merchant Center estão em Backlog (EP-39 a EP-44).

## Apps instalados e extensões

- **Shopify Forms:** formulário `1175431` (bloco de app `forms/inline`) nas páginas `page.cadastre-sua-empresa` e `page.atacado`. É o formulário de cadastro B2B (company account request).
- **Shopify Flow:** usado na EP-92 (aprovação automática da empresa e reforço em Order created). Detalhes em "Cadastro B2B (EP-92)".
- Não é Plus: sem checkout UI extensions nem Functions/customizações de checkout exclusivas do Plus.
- Demais apps: não informado.

## Dados

- **Empresa (EP-92):** metafield definitions de COMPANY, texto, leitura pública no storefront (`PUBLIC_READ`): `custom.razao_social`, `custom.cnpj` (sempre só dígitos, 14) e `custom.inscricao_estadual` (já existia; pode ser "ISENTO"). O Forms grava a razão social em `company.name` e o CNPJ no Tax ID da location; o Flow de aprovação copia para os metafields.
- **Pedido (EP-92):** cart attributes `razao_social`, `cnpj` (só dígitos) e `ie`, que viram atributos adicionais (`note_attributes`) na criação do pedido.
- **Catálogo B2B:** "Catalogo Atacado" (-5%) no mercado Atacado.
- Demais metafields, metaobjects e price lists: não informado. Cada envio do Forms também vira um metaobject de submissão em Content > Metaobjects.

## Cadastro B2B (EP-92)

- **Forms 1175431** ("Company and customer", pt-BR): Razão Social → `company.name`; CNPJ → Tax ID da location; Inscrição Estadual (opcional) → metafield da empresa; e-mail e endereços de entrega/faturamento obrigatórios. Tags no cliente: `atacado` e `shopify-forms-1175431`. O bloco "Company set up" só aponta para o template de Flow; não tem configuração própria.
- **Flow "EP-92 Aprovação B2B (Forms)"** (criado desativado em 27/11/2026): gatilho Company location created, só quando o evento vem do Forms; espera 2 min; location sem checkout em rascunho, endereço de entrega travado e sem condições de pagamento; grava `custom.razao_social` e `custom.cnpj` (só dígitos); e-mail para `vendasweb@` e `ecommerce@` (`espacoprime.com.br`); tag `atacado` no contato principal; troca o papel do contato para Ordering only (remove o existente e atribui o novo, pois a Shopify aceita um papel por contato por location). Substitui os Flows "Get notified and set up companies created by company account requests", "Remover condições…" e "Cadastro Empresa" quando for ativado.
- **Flow de reforço "Adiciona informações fiscais ao pedido"** (Order created; nova versão em rascunho): `orderUpdate` reenviando os atributos existentes e acrescentando `razao_social`, `cnpj` e `ie`, mais a nota com `{{ order.note }}` e os dados fiscais.
- **Tema:** `snippets/b2b-cart-attributes.liquid`, só para `customer.b2b?` com `customer.current_company`. Lê os metafields da empresa (fallback `company.name` e `tax_registration_id` da location, com zeros à esquerda repostos), remove tudo que não é dígito do CNPJ. Render padrão em `layout/theme.liquid` (compara com `cart.attributes` e chama `/cart/update.js` só se mudou) e `mode: 'inputs'` (inputs hidden) dentro do form do carrinho em `snippets/header.cart-drawer.liquid` e `snippets/section.main-cart.liquid`.

## Sections, blocks e snippets principais

- Páginas B2B: `templates/page.atacado.json` ("Compre no Atacado com CNPJ", com o formulário, FAQ e contato comercial) e `templates/page.cadastre-sua-empresa.json` (só o formulário).
- Carrinho: `sections/main-cart.liquid`, `sections/cart-ajax.liquid`, `snippets/cart.order-note.liquid` (+ `assets/cart.order-note.js`), `snippets/header.cart-drawer.liquid`. É aqui que entram os cart attributes da EP-92 (carrinho de página e drawer).
- Conta do cliente: `templates/customers/*.json`, `sections/main-register.liquid`, `snippets/form.customer.liquid`, `snippets/customer-account.liquid`.
- Templates de produto além do padrão: `product.brand-story`, `product.cross-selling`, `product.form`, `product.gift-card`, `product.preorder`, `product.product-landing`.
- Páginas: `page.about`, `page.contact`, `page.faq`, `page.full-width`, `page.nossos-fornecedores`.
- Locales: `en.default`, `pt-BR` (com schema), `pt-PT`, `de`, `es`, `fr`, `it`.

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| 2026-11-27 | Loja não é Plus: nada de checkout UI extensions nem Functions exclusivas do Plus. | Confirmação do Kariston. | |
| 2026-11-27 | Cadastro B2B com Shopify Forms (cria Company, location e cliente), Flow de aprovação automática (template "Allow ordering for companies created by company account requests"), empresa sem condições de pagamento (checkout normal). | Caminho escolhido pelo Kariston entre as opções do Especialista Shopify; só configuração, sem app próprio. | EP-92 |
| 2026-11-27 | Razão social, CNPJ e IE vão ao pedido como cart attributes gravados pelo tema (`razao_social`, `cnpj`, `ie`), a partir de `customer.current_company` e da location; Flow em Order created como reforço (completa atributos com `orderUpdate` reenviando os existentes e acrescenta à nota). | Os atributos entram na criação do pedido, antes da leitura da Anymarket; o Flow cobre pedidos fora do carrinho do tema (ex.: "comprar novamente"). | EP-92 |
| 2026-11-27 | Metafields `custom.razao_social`/`custom.cnpj`/`custom.inscricao_estadual` em COMPANY com leitura pública; CNPJ só com dígitos em metafield, atributos e Flows. Sem tema de preview até a loja entrar em produção. | Decisões do Kariston. | EP-92 |
| 2026-11-27 | Figma: não informado. Designer mantém o padrão do tema Expanse configurado. | Dados do time. | |

## Armadilhas conhecidas

- A `master` recebe commits automáticos do Shopify bot (editor do tema). Merge ou rebase precisa de cuidado para não sobrescrever mudanças feitas na loja. `config/settings_data.json` e templates JSON podem sobrescrever a configuração se forem commitados sem intenção.
- Shopify Forms não valida CNPJ nem IE (só obrigatório/opcional), não vincula o cliente a uma Company existente (cada envio cria uma nova) e rejeitar significa excluir a Company.
- A ação "Update order note" do Flow substitui a nota inteira (incluir `{{order.note}}`); `orderUpdate.customAttributes` sobrescreve a lista inteira (reenviar os atributos existentes).
- O Flow em Order created roda depois da criação do pedido: pode haver corrida com a leitura da Anymarket.
- "[Check] Desenvolvimento" é o tema publicado e está conectado à `master`: todo merge vai direto para a loja.
- Contato de empresa aceita um único papel por location: atribuir Ordering only a quem já tem Location admin falha; é preciso remover o papel antes.
- Compras fora do carrinho do tema (comprar novamente pela conta, link direto de checkout, draft order) não passam pelos cart attributes.

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| 2026-10-23 | Tamanho de fonte configurável para o preço do produto (commit manual de Denner Moraes na `master`). | |
| 2026-10 / 2026-11 | Ajustes de layout e selos do cliente pelo editor Shopify. | EP-89 / EP-90 |
| 2026-11-27 | Definição do time "Tema - Espaço Prime" e levantamento inicial desta arquitetura. | |
| 2026-11-27 | Cadastro B2B: metafields da empresa, Flow de aprovação (desativado), rascunho do Flow de reforço, 6 empresas corrigidas e snippet `b2b-cart-attributes` no tema. | EP-92 / checkstore/espaco-prime#1 |
