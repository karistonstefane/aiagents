# Arquitetura: Tema - Nuora

> Mantido pelo Dev no mesmo ciclo do PR do projeto (PR complementar no `aiagents`) quando a mudança afetar a arquitetura. Fatos verificados no repositório `checkstore/nuoracosmetic` (`origin/master`) e nas decisões do Kariston. O que não se sabe: `não informado`.

## Visão geral

- Loja da Nuora Cosméticos: `nuora-cosmetic.myshopify.com`, domínio `nuora.com.br`. Modelo: não informado.
- Tema publicado (06/11/2026): "[CS] Check V1", id 146770460714, conectado à branch `master` (o merge publica o tema).

## Stack e repositório

- **Repositório:** `checkstore/nuoracosmetic` (local `~/projects/nuoracosmetic`)
- **Branch base:** `master`
- **Base:** tema **Horizon 3.3.1** (Shopify).
- **Estrutura:** padrão Online Store 2.0 com theme blocks: `assets/`, `blocks/`, `config/`, `layout/`, `locales/`, `sections/`, `snippets/`, `templates/`.

## Integrações

- **Google Tag Manager:** `GTM-KMGQRKMN`, inclusive na página de senha (NU-67).
- Demais: não informado.

## Apps instalados e extensões

- Não informado.

## Dados

- Não informado.

## Sections, blocks e snippets principais

- Blocks gerados por IA no editor: `blocks/ai_gen_block_*` (5 arquivos).
- Templates específicos: `page.quiz`, `page.prescritores`, `page.solucoes`, `page.nuora-experience`, `page.bastidores`, `page.qrcode`, `page.produtos`.
- Demais customizações: não informado.

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| 2026-11-06 | GTM também na página de senha. | não informado | NU-67 |

## Armadilhas conhecidas

- O tema publicado está conectado à `master`: merge publica direto na loja.
- Tema baseado no Horizon: preferir blocos/seções nativos e manter compatibilidade com atualizações do tema base.

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| 2026-11-06 | GTM na página de senha. | NU-67 / PR #1 |
