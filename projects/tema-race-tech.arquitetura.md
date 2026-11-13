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
- Cabeçalho da loja (descrição em RT-74): menus Capacete e Peças e Acessórios à esquerda, logo RACE TECH no centro, busca e ícones à direita. No desktop (`lg`), o seletor de idioma é o último item de `.header__buttons`, depois do carrinho, e mostra só a bandeira do idioma (RT-74, PR `checkstore/race-tech#1`). O header desktop mostra só o idioma (sem país/moeda). No celular o seletor continua no menu (`snippets/menu-drawer.liquid`), e o rodapé não mudou.
- Seletor de idioma só com bandeira: `sections/header.liquid` chama `snippets/dropdown-localization.liquid` com o parâmetro `language_flag_only: true`; com ele, `snippets/localization-form.liquid` troca o `<select>` de idiomas por uma lista de `<button type="submit" name="language_code">` (bandeira + `endonym_name`) no mesmo `{% form 'localization' %}`, reaproveitando o `dropdown-localization-component` de `assets/localization.js` (sem JS novo). Sem o parâmetro (rodapé e menu mobile), os snippets se comportam como antes. CSS escopado em `assets/component-localization-dropdown.css` (`.header__localization--flag-only`).
- Snippet `snippets/language-flag.liquid`: bandeira circular por idioma, mapeada pelo `iso_code` completo: `pt-BR` → Brasil, `en` → EUA, `es` → Espanha; qualquer outro código (ex.: `pt-PT`, `en-GB`, `es-MX`) mostra o ícone de globo (`icon-globe`).
- Assets de bandeira: `assets/flag-br.svg`, `assets/flag-us.svg`, `assets/flag-es.svg`, do projeto flag-icons (licença MIT, formato 4x3, viewBox 640x480). O `flag-es.svg` foi otimizado com svgo (de 81 KB para 41 KB), mantendo o brasão.
- Setting `show_language_flag` no schema do header (Personalizar), padrão `true`: ligado, usa o seletor só com bandeira depois do carrinho; desligado, volta o seletor antigo do header desktop (país/moeda e idioma com texto, antes da busca). Rótulos em `locales/*.schema.json` (sem `pt-BR.schema.json`, o admin em português mostra o rótulo em inglês).

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| 2026-10-30 | Ocultar o espaço do banner de coleção quando não houver imagem, e o hero quando o metafield do banner estiver vazio. | Evitar o espaço vazio na página de coleção. | RT-72 |
| 2026-11-12 | "[Check] Desenvolvimento" é o tema publicado; a loja ainda está em desenvolvimento. O merge na `master` publica o tema conectado. | Confirmação do Kariston. | |
| 2026-11-12 | Sem Figma: tema comprado da loja Shopify (Pebble); manter o padrão visual dele. | Confirmação do Kariston. | |
| 2026-11-12 | Header desktop: seletor de idioma só com bandeira, depois do carrinho, sem país/moeda; parâmetro novo `language_flag_only` em `dropdown-localization`/`localization-form`, para não alterar rodapé nem menu mobile. Controlado pelo setting `show_language_flag` (padrão `true`; desligado volta o seletor antigo). | Pedido da cliente (Mayara) e decisões do Kariston: "No celular continua no menu", "Pode tirar país e moeda do header desktop", "Com checkbox no Personalizar". | RT-74 |
| 2026-11-12 | A bandeira segue o idioma, não o país: `pt-BR` Brasil, `en` EUA, `es` Espanha, outro código globo; SVGs locais do flag-icons (MIT, 4x3) em `assets/`, sem CDN. | "Inglês com bandeira dos EUA"; "Idiomas publicados: português, inglês e espanhol (bandeira da Espanha)". | RT-74 |

## Armadilhas conhecidas

- A `master` está conectada ao tema publicado "[Check] Desenvolvimento": o merge publica o tema. A loja ainda está em desenvolvimento, mas o tema publicado é atualizado no merge. A `master` também recebe commits automáticos do Shopify bot. Merge ou rebase precisa de cuidado para não sobrescrever mudanças do editor ou da loja.
- `settings_data.json`, `config/` e templates JSON podem sobrescrever a configuração da loja se forem commitados sem intenção.
- Até 12/11/2026 o trabalho vinha direto na `master` ou pelo editor Shopify. O fluxo oficial é branch + PR + review do bot Revisor, com merge manual do Kariston.

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| 2026-10-30 | Seletor de idioma no cabeçalho e correção de cor no rodapé (commit direto na `master`; tarefa segue em Homologação). | RT-74 |
| 2026-11-12 | Ajuste do seletor de idioma: só a bandeira, depois do carrinho, no header desktop (`language_flag_only`, `snippets/language-flag.liquid`, `assets/flag-*.svg`, setting `show_language_flag`); `content.language` traduzido para "Idioma" em `locales/pt-BR.json`. | RT-74 / `checkstore/race-tech#1` |
| 2026-10-30 / 2026-11-06 | Ocultar banner/hero de coleção quando vazio (commits diretos na `master`). | RT-72 |
