# Arquitetura: Tema - Nuora

> Mantido pelo Dev no mesmo ciclo do PR do projeto (PR complementar no `aiagents`) quando a mudança afetar a arquitetura. Fatos verificados no repositório `checkstore/nuoracosmetic` (`origin/master`) e nas decisões do Kariston. O que não se sabe: `não informado`.

## Visão geral

- Loja da Nuora Cosméticos: `nuora-cosmetic.myshopify.com`, domínio `nuora.com.br`. Modelo: não informado.
- Tema publicado (25/11/2026): **"[CS] Check V3"**, id **150333259818**. Foi duplicado e publicado pelo cliente a partir de um tema fora do GitHub; o conteúdo foi sincronizado na `master` pelo PR #2 (NU-67).
- O id 146770460714 ("[CS] Check V1" em 06/11/2026) não existe mais na loja.
- A `master` está conectada (integração GitHub da Shopify) a um tema **"[CS] Check V1"** não publicado: #150218735658 ou #150255403050 (não confirmado qual). O V3 publicado **não** está conectado ao repositório.

## Stack e repositório

- **Repositório:** `checkstore/nuoracosmetic` (local `~/projects/nuoracosmetic`)
- **Branch base:** `master`
- **Base:** tema **Horizon 3.3.1** (Shopify).
- **Estrutura:** padrão Online Store 2.0 com theme blocks: `assets/`, `blocks/`, `config/`, `layout/`, `locales/`, `sections/`, `snippets/`, `templates/`. Há também um `AGENTS.md` (guia de autoria do tema) vindo do tema publicado.

## Integrações

- **Google Tag Manager:** `GTM-KMGQRKMN`.
  - `layout/password.liquid`: snippet oficial (script no `<head>` após `{{ content_for_header }}` + `<noscript>` logo após `<body>`). Instalado no PR #1 e restaurado no PR #2 (o V3 publicado veio sem ele).
  - `layout/theme.liquid`: **não** contém o GTM (nem na `master` antiga nem no V3). Provavelmente carregado via app ou Customer Events nas demais páginas (não verificado).
- Demais: não informado.

## Apps instalados e extensões

- Não informado.

## Dados

- Não informado.

## Sections, blocks e snippets principais

- Sections customizadas da Nuora (vindas do V3, PR #2): `sections/nuora-blog-grid.liquid`, `nuora-depoimentos.liquid`, `nuora-image-carousel.liquid`, `nuora-image-products.liquid`, `nuora-quiz-best-sellers.liquid`, `nuora-resultados-testes.liquid`, `nuora-seals-marquee.liquid`, `nuora-statement.liquid`, `nuora-video-banner.liquid`.
- Blocks customizados: `blocks/buy-now.liquid` (renderizado em `buy-buttons`) e `blocks/product-details-button.liquid`.
- Snippet `snippets/nuora-buttons.liquid` e asset `assets/nuora-brand.css`, ambos carregados em `layout/theme.liquid` para todas as páginas; asset `assets/nuora-symbol.svg`.
- Setting global "Fotos dos cards de produto" (`config/settings_schema.json`): troca a foto do card de produtos escolhidos, só neste tema.
- Blocks gerados por IA no editor: `blocks/ai_gen_block_*` (4 arquivos; `ai_gen_block_4628687.liquid` foi removido no PR #2 por não existir no tema publicado e não ser referenciado).
- Templates específicos: `page.quiz`, `page.prescritores`, `page.solucoes`, `page.nuora-experience`, `page.bastidores`, `page.qrcode`, `page.produtos`, `page.contato`.

### Customizações em arquivos core do Horizon

Atenção ao atualizar o Horizon: estas mudanças precisam ser reaplicadas.

- `assets/product-form.js`: tempo do estado "adicionado" do botão de adicionar ao carrinho de 800 ms para 2000 ms.
- `blocks/buy-buttons.liquid`: renderiza o block `buy-now` (`content_for 'block', type: 'buy-now'`) antes do `add-to-cart`.
- `snippets/header-actions.liquid`: passa `in_drawer: true` ao `cart-summary` no carrinho lateral.
- `snippets/header-drawer.liquid`: `min-height` dos itens do menu lateral passa a usar a variável `--menu-drawer-item-min-height` (com o valor original como fallback).
- `blocks/_header-logo.liquid`: logo inverso ganha `filter: brightness(0) invert(1)` (logo branco no header transparente da home, sem arquivo de logo branco).
- Outros arquivos core alterados pelo cliente (ver PR #2): `_announcement`, `_carousel-content`, `_featured-product-information-carousel`, `_header-menu`, `_product-card`, `_product-card-gallery`, `_product-list-text`, `group`, `product-title`, `text`, `carousel`, `featured-product-information`, `main-collection`, `product-list`, `add-to-cart-button`, `cart-products`, `cart-summary`, `divider`, `group` (snippet), `menu-font-styles`, `product-grid`, `text` (snippet).

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| 2026-11-06 | GTM também na página de senha. | não informado | NU-67 |
| 2026-11-25 | O tema publicado pelo cliente ("[CS] Check V3", #150333259818) é a fonte da verdade; seu conteúdo foi sincronizado na `master` preservando as mudanças do cliente, e o GTM da página de senha foi restaurado. | O cliente duplicou um tema fora do GitHub e publicou sem o GTM na página de senha. | NU-67 |

## Armadilhas conhecidas

- A `master` está conectada a um tema "[CS] Check V1" **não publicado**: merge na `master` atualiza esse V1, não o V3 publicado. Para chegar à loja é preciso publicar o tema conectado ou conectar o V3 à `master` (decisão do Kariston).
- Edições do cliente direto no V3 (fora do GitHub) divergem da `master` até o V3 ser conectado ao repositório.
- Tema baseado no Horizon: preferir blocos/seções nativos e manter compatibilidade com atualizações do tema base (ver "Customizações em arquivos core do Horizon").

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| 2026-11-06 | GTM na página de senha. | NU-67 / PR #1 |
| 2026-11-25 | Sincroniza o tema publicado "[CS] Check V3" na `master` (9 seções `nuora-*`, blocks `buy-now` e `product-details-button`, `nuora-buttons`, `nuora-brand.css`, `nuora-symbol.svg`, remoção de `ai_gen_block_4628687`) e restaura o GTM-KMGQRKMN no `password.liquid`. | NU-67 / [PR #2](https://github.com/checkstore/nuoracosmetic/pull/2) |
