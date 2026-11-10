# Arquitetura: Tema - Hercules

> Mantido pelo Dev no mesmo ciclo do PR do projeto (PR complementar no `aiagents`) quando a mudança afetar a arquitetura. Fatos verificados no repositório `checkstore/hercules` (`origin/master`, commit `00d06e2`, 06/11/2026) e nas decisões do Kariston. O que não se sabe: `não informado`.

## Visão geral

- Loja **100% B2B** da Hércules Motores: `totvsle-herculesmotores.myshopify.com`, domínio `herculesenergia.com.br`, plano Shopify Plus.
- O tema publicado acompanha a branch `master` (o merge publica o tema).
- Funcionalidades B2B do app compartilhado ficam no time **App - Mueller e Hercules** (`projects/app-mueller-hercules.arquitetura.md`).

## Stack e repositório

- **Repositório:** `checkstore/hercules` (local `~/projects/hercules`)
- **Branch base:** `master`
- **Base:** tema próprio **"Hercules" 1.0.0** (`theme_info`), não é um tema da Theme Store.
- **Estrutura:** `assets/`, `blocks/`, `config/`, `layout/`, `locales/`, `sections/`, `snippets/`, `templates/` (inclui `templates/metaobject/`), mais `docs/` e pastas de agentes (`.agents/`, `.claude/`, `skills-lock.json`).
- Há commits automáticos "Update from Shopify for theme [Check] Desenvolvimento" (edições no admin sincronizadas pelo GitHub).

## Integrações

- Integração com SAP e regras B2B: feitas pelo app `app-b2b-connect`, não pelo tema.
- Outras integrações no tema: não informado.

## Apps instalados e extensões

- App `app-b2b-connect` (custom app da Checkstore, config `app-b2b-connect-hercules`), com app proxy em `/apps/b2b` e a theme app extension `b2b-company-registration`.
- Demais apps da loja: não informado.

## Dados

- Templates de metaobject em `templates/metaobject/` (tipos: não informado).
- Agrupamento de produtos: `snippets/product-group-selector`, `snippets/product-group-option` (metafields exatos: não informado).
- Company locations: seletor em `snippets/company-location-selector`.

## Sections, blocks e snippets principais

- **B2B / acesso:** `sections/b2b-context`, `sections/b2b-status-modal`, `snippets/store-access-status`, `snippets/guest-filter`, `snippets/guest-product-allowed`, `sections/company-policies`.
- **Carrinho:** `sections/cart`, `sections/cart-drawer`, `snippets/cart-vendor-groups`, `snippets/delivery-schedule-summary`, `assets/cart-delivery-schedule.js`, `blocks/shipping-calculator`.
- **Carrinhos salvos:** `sections/saved-carts`, `snippets/save-cart-button`, `snippets/saved-cart-json`, `assets/saved-carts.js`, template `page.carrinhos-salvos`.
- **Configurador de produto / placa personalizada:** `sections/product-configurator`, `sections/product-configurator-data`, `sections/placa-personalizada`, template `product.placa-personalizada`.
- **Downloads/suporte:** `sections/downloads-hub`, `sections/downloads`, `sections/download-notes`, templates `page.suporte-downloads*`.
- **Utilitários pt-BR:** `snippets/format-cnpj`, `snippets/format-date-ptbr`.
- **Leitura de código de barras:** `sections/barcode-lookup`, `snippets/barcode-scanner`.
- Cadastro B2B: template `page.cadastro`; importação de pedido: `page.importacao-de-pedido`.

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| 2026-11-06 | WhatsApp e e-mail do Fale Conosco só viram link quando os campos do Personalizar estão preenchidos; ícone de leitor apenas visual no desktop. | Evitar links vazios; conteúdo configurável pelo cliente. | HCL-233 |

## Armadilhas conhecidas

- O tema publicado acompanha a `master`: merge publica direto na loja.
- Edições no Personalizar (inclusive da GP) geram commits na `master`; atualize a branch antes de começar.

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| 2026-11-06 | Ajustes do Fale Conosco e ícone de leitor. | HCL-233 |
