# Arquitetura: Tema - Made in Guarda

> Mantido pelo Dev no mesmo ciclo do PR do projeto (PR complementar no `aiagents`) quando a mudança afetar a arquitetura. Fatos verificados no repositório `checkstore/made-in-guarda` (`origin/master`, commit `ef60410`, 06/11/2026) e nas decisões do Kariston. O que não se sabe: `não informado`.

## Visão geral

- Loja da Made in Guarda: `made-in-guarda.myshopify.com`, domínio `madeinguarda.com.br` (DNS na SAN Internet / Cloud). Modelo: não informado.
- Tema publicado: "[Check] Produção", conectado à branch `master` (o merge publica o tema).

## Stack e repositório

- **Repositório:** `checkstore/made-in-guarda` (local `~/projects/made-in-guarda`)
- **Branch base:** `master`
- **Base:** tema **Prestige 11.4.1** (Maestrooo).
- **Estrutura:** `assets/` (JS/CSS compilados do Prestige: `theme.js`, `theme.css`, `vendor.min.js`), `blocks/`, `config/`, `layout/`, `locales/`, `sections/`, `snippets/`, `templates/` (inclui `customers/`).

## Integrações

- Não informado.

## Apps instalados e extensões

- Não informado.

## Dados

- Não informado.

## Sections, blocks e snippets principais

- **Disponibilidade de variantes:** `snippets/variant-is-sellable`, `snippets/option-value-is-sellable` (toggle `treat_last_unit_as_sold_out`, GDA-173).
- Templates específicos: `product.pre-order`, `product.vestido`, `page.lojas`, `page.mig-surf`, `page.quem-somos`, `page.trocas`, `page.ecological-trend`.
- Demais customizações: não informado.

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| 2026-11-06 | Toggle global para tratar a última unidade em estoque como esgotada, desligado por padrão em `settings_data.json`. | Pedido do cliente, configurável no Personalizar. | GDA-173 |
| não informado | Labels dos schemas do tema em inglês. | Padrão definido pelo Kariston para este tema. | não informado |

## Armadilhas conhecidas

- O tema publicado está conectado à `master`: merge publica direto na loja.
- `config/settings_schema.json` já quebrou por vírgula sobrando (corrigido em PR separado após a GDA-173): valide o JSON.
- `assets/theme.js`/`theme.css` são do Prestige: prefira arquivos próprios para customizações, para facilitar atualizações do tema.

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| 2026-11-06 | Toggle `treat_last_unit_as_sold_out` (e correção de vírgula no `settings_schema.json`). | GDA-173 / PR #2 |
