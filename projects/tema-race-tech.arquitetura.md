# Arquitetura: Tema - Race Tech

> Mantido pelo Dev no mesmo ciclo do PR do projeto (PR complementar no `aiagents`) quando a mudança afetar a arquitetura. Fatos verificados no repositório `checkstore/race-tech` (`origin/master`, levantamento em 12/11/2026), nas tarefas do Jira RT e nas confirmações do Kariston no mesmo dia. O que não se sabe: `não informado`.

## Visão geral

- Loja da Race Tech (marca citada junto à BR Motorsport): `brmotorsport-01-re0rgmhc.myshopify.com` (RT-74). Modelo aparente: B2C. Plano: Shopify Plus (RT-71).
- Domínio customizado da loja Shopify: ainda não tem.
- Tema publicado, conectado à branch `master`: "[Check] Desenvolvimento", base **Pebble 1.4.0** (FoxEcom, tema comprado na loja Shopify). A loja ainda está em desenvolvimento. O merge na `master` publica o tema conectado. Id numérico: não informado.

## Stack e repositório

- **Repositório:** `checkstore/race-tech` (local `~/projects/race-tech`)
- **Branch base:** `master` (o tema publicado está conectado à `master`: o merge publica o tema). Fluxo: branch `feat/RT-<n>-<slug>` ou `fix/RT-<n>-<slug>`, PR contra `master`, review do bot Revisor, merge manual do Kariston.
- **Base:** tema **Pebble 1.4.0** (FoxEcom), Online Store 2.0.
- **Estrutura:** `assets/`, `blocks/` (168), `config/`, `layout/` (`theme.liquid`, `password.liquid`), `locales/`, `sections/` (80), `snippets/`, `templates/` (32). Não há README, `shopify.theme.toml`, workflows nem `package.json`.
- **Histórico Git:** até 12/11/2026, a maior parte dos commits na `master` veio do Shopify bot ("Update from Shopify for theme [Check] Desenvolvimento", vários por Mayara Silveira). Commits manuais do Kariston estavam em português, sem chave Jira e sem PR. A partir desta data, vale o fluxo dos bots (branch separada, PR, review).

## Integrações

- Não informado no repositório. `layout/theme.liquid` e `layout/password.liquid` não instalam GTM nem scripts de terceiros além de `storefront-events` e `content_for_header`.

## Apps instalados e extensões

- Não informado.

## Dados

- Banner de coleção: o tema oculta o espaço do banner/hero quando não há imagem ou o metafield do banner está vazio (RT-72; commits do Kariston em 30/10 e 06/11/2026). Namespace/key exatos do metafield: não informados neste levantamento.
- Demais metafields, metaobjects e segmentos: não informado.

## Sections, blocks e snippets principais

- Header/footer/overlay: `sections/header-group.json`, `sections/footer-group.json`, `sections/overlay-group.json` (há também `overlay-group.context.espanhol.json`).
- Banner de coleção: `sections/main-collection-banner.liquid`, snippet `collection-banner-image.liquid`.
- Templates de produto além do padrão: `product.capacetes`, `product.flash-sale`, `product.2-columns`, `product.inside-thumbnails`.
- Templates de coleção além do padrão: `collection.minimal`, `collection.with-banner`, `collection.with-banner-2`, `collection.with-full-wide-banner`.
- Páginas: `page.about`, `page.contact`, `page.faqs`, `page.help-center`, `page.store-location`.
- Locales: `en.default` (idioma padrão dos arquivos), `pt-BR`, `de`, `es`, `fr`, `it`, `vi`. Não há `pt-BR.schema.json`.
- Cabeçalho da loja (descrição em RT-74): menus Capacete e Peças e Acessórios à esquerda, logo RACE TECH no centro, busca e ícones à direita. Há trabalho em andamento no seletor de idioma (RT-74, Homologação).

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| 2026-10-30 | Ocultar o espaço do banner de coleção quando não houver imagem, e o hero quando o metafield do banner estiver vazio. | Evitar o espaço vazio na página de coleção. | RT-72 |
| 2026-11-12 | "[Check] Desenvolvimento" é o tema publicado; a loja ainda está em desenvolvimento. O merge na `master` publica o tema conectado. | Confirmação do Kariston. | |
| 2026-11-12 | Sem Figma: tema comprado da loja Shopify (Pebble); manter o padrão visual dele. | Confirmação do Kariston. | |

## Armadilhas conhecidas

- A `master` está conectada ao tema publicado "[Check] Desenvolvimento": o merge publica o tema. A loja ainda está em desenvolvimento, mas o tema publicado é atualizado no merge. A `master` também recebe commits automáticos do Shopify bot. Merge ou rebase precisa de cuidado para não sobrescrever mudanças do editor ou da loja.
- `settings_data.json`, `config/` e templates JSON podem sobrescrever a configuração da loja se forem commitados sem intenção.
- Até 12/11/2026 o trabalho vinha direto na `master` ou pelo editor Shopify. O fluxo oficial é branch + PR + review do bot Revisor, com merge manual do Kariston.

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| 2026-10-30 | Seletor de idioma no cabeçalho e correção de cor no rodapé (commit direto na `master`; tarefa segue em Homologação). | RT-74 |
| 2026-10-30 / 2026-11-06 | Ocultar banner/hero de coleção quando vazio (commits diretos na `master`). | RT-72 |
