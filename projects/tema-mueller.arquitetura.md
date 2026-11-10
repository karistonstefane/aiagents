# Arquitetura: Tema - Mueller

> Mantido pelo Dev no mesmo ciclo do PR do projeto (PR complementar no `aiagents`) quando a mudança afetar a arquitetura. Fatos verificados no repositório `checkstore/mueller` (`origin/master`, commit `cf2987c`, 03/11/2026) e nas decisões do Kariston. O que não se sabe: `não informado`.

## Visão geral

- Loja **100% B2B** da Mueller: `totvsle-mueller.myshopify.com`, plano Shopify Plus. Domínio ainda não definido.
- Tema publicado: "[Check] Mueller", conectado à branch `master` (o merge publica o tema).
- Funcionalidades B2B do app compartilhado (cadastro de empresas, checkout, descontos) ficam no time **App - Mueller e Hercules** (`projects/app-mueller-hercules.arquitetura.md`).

## Stack e repositório

- **Repositório:** `checkstore/mueller` (local `~/projects/mueller`)
- **Branch base:** `master`
- **Base:** tema **Horizon 3.4.0** (Shopify), customizado.
- **Estrutura:** padrão de tema Online Store 2.0 com theme blocks: `assets/`, `blocks/`, `config/`, `layout/`, `locales/`, `sections/`, `snippets/`, `templates/`.
- Há commits automáticos "Update from Shopify for theme [Check] Desenvolvimento" (edições feitas no admin/Personalizar sincronizadas pelo GitHub).

## Integrações

- Integração com SAP e demais regras B2B: feitas pelo app `app-b2b-connect`, não pelo tema.
- Outras integrações no tema: não informado.

## Apps instalados e extensões

- App `app-b2b-connect` (custom app da Checkstore), com app proxy em `/apps/b2b` e a theme app extension `b2b-company-registration`.
- Demais apps da loja: não informado.

## Dados

- Metafields de produto para variantes agrupadas: **cor**, **tensão** e **grupo de produto** (produtos separados agrupados como "variantes"). Namespace/keys exatos: não informado.
- Company locations / catálogos B2B: os preços vêm de catálogos/price lists B2B.

## Sections, blocks e snippets principais

- **B2B:** `sections/b2b-context`, `snippets/company-location-selector`, `snippets/login-required-cta`, `assets/customer-access-gate.js`, `sections/quick-order-list`.
- **Carrinhos salvos:** `sections/saved-carts`, `snippets/save-cart-button`, `snippets/saved-cart-json`, `snippets/saved-carts-*`, `assets/saved-carts.js`, template `page.carrinhos-salvos`.
- **Importação de pedidos:** template `page.importacao-de-pedidos`.
- **Leitura de código de barras:** `sections/barcode-lookup`, `snippets/barcode-scanner`, `assets/barcode-scanner.js`.
- **Variantes por metafield:** `blocks/metafield-variant-picker`, `blocks/_metafield-variant-option`, `snippets/metafield-variant-candidate|dimension|target`.
- **Downloads/suporte:** `sections/downloads-cards`, `blocks/_downloads-card`, templates `page.downloads`, `page.suporte`, `page.assistencia-tecnica`.
- Cadastro B2B: template `page.cadastro`.

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| 2026-11-09 | Ao trocar só a cor no grupo de produtos, manter a tensão selecionada. | UX das centrífugas (ex.: continuar em 220 V ao trocar preto por branco). | MUEL-271 |

## Armadilhas conhecidas

- O tema publicado está conectado à `master`: merge publica direto na loja.
- Edições no Personalizar geram commits na branch conectada; atualize a branch antes de começar.

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| 2026-11-09 | Seleção de cor mantém a tensão no grupo de produtos (merge pelo Kariston). | MUEL-271 / PR #34 |
