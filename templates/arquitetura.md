# Arquitetura: <Tipo> - <Cliente>

> Copie para `projects/<slug>.arquitetura.md`. Registre só fatos verificados no repositório, na loja ou decididos pelo Kariston. O que não se sabe fica como `não informado`. **Não coloque senhas, tokens nem credenciais.**
>
> Quem mantém: o **Dev**, no mesmo ciclo do PR do projeto (PR complementar no `aiagents`), sempre que a mudança afetar a arquitetura (nova integração, metafield, section, extensão, decisão). O Revisor confere.

## Visão geral

- O que é o projeto, para quem, modelo (B2C/B2B), lojas envolvidas.

## Stack e repositório

- **Repositório:** `checkstore/<repo>` (local `~/projects/<pasta>`)
- **Branch base:** `master` | `main`
- **Base:** tema (nome e versão) ou stack do app (framework, banco, hospedagem)
- **Estrutura:** pastas principais e o que vive em cada uma

## Integrações

- SAP, OMS, ERP, gateways, ferramentas de marketing etc.: o que integra, por onde (app, webhook, app proxy, script) e quem é o dono.

## Apps instalados e extensões

- Apps da loja relevantes para o tema/app e extensões (theme app extensions, checkout UI, Functions).

## Dados

- Metafields (namespace.key, recurso, tipo, uso), metaobjects, company locations, segmentos, catálogos/price lists.

## Sections, blocks e snippets principais / módulos do app

- O que é customizado e merece atenção (não listar o que é padrão do tema base).

## Decisões de arquitetura

| Data | Decisão | Motivo | Tarefa Jira |
|---|---|---|---|
| AAAA-MM-DD | | | |

## Armadilhas conhecidas

- Comportamentos que já causaram bug ou confusão.

## Histórico de mudanças relevantes

| Data | Mudança | Tarefa / PR |
|---|---|---|
| AAAA-MM-DD | | |
