# Projeto: Tema - Made in Guarda

## Identificação

- **Nome do time:** Tema - Made in Guarda
- **Cliente:** Made in Guarda
- **Bots:** `Tema - Made in Guarda · Gerente`, `· Dev`, `· Designer`, `· Revisor` (ids no `registry.json`)

## Loja(s)

- **Loja:** `made-in-guarda.myshopify.com`
- **Domínio:** `madeinguarda.com.br` (DNS gerenciado no painel da SAN Internet / Cloud)
- **Tema publicado:** "[Check] Produção", conectado à branch `master`

## Repositório

- **Local:** `~/projects/made-in-guarda` (`C:\Users\Kariston\projects\made-in-guarda`)
- **GitHub:** `checkstore/made-in-guarda`
- **Branch base:** `master` (o tema publicado está conectado à `master`: merge nela afeta a loja)

## Revisão

- **revisor:** `bot`
- **revisor_github:** —
- **deploy:** Kariston (o merge na `master` publica o tema conectado)

## Design

- **designer:** `sim`
- **figma:** não informado

Tarefas com impacto visual/UI passam pelo Designer depois da validação do Kariston e antes do Dev. Sem Figma, o Designer segue o padrão existente do tema.

## Arquitetura

- **Arquivo:** [`projects/tema-made-in-guarda.arquitetura.md`](./tema-made-in-guarda.arquitetura.md). Leia antes de refinar, desenhar ou implementar; o Dev atualiza no mesmo ciclo do PR quando a mudança afetar a arquitetura.

## Jira

- **Projeto / prefixo:** `GDA`
- **Filtro do Gerente:** `project = GDA AND status = "Para fazer" AND assignee = "Kariston Stefane"`
- Épico de publicação: GDA-13 (Publicação e Monitoramento).

## Contatos

- Mayara: Gerente de Projetos (também liberou os acessos ao painel SAN/Cloud).
- Enrique: auxilia a Gerente de Projetos; reporter das tarefas GDA.

## Convenções

- Branch: `feat/GDA-<n>` ou `fix/GDA-<n>` (ex.: `feat/GDA-173`).
- PR contra `master`, com roteiro de teste e link do preview.

## Regras específicas

- **Labels dos schemas do tema ficam em inglês** (exceção à regra do pt-BR). As respostas aos bots e ao Kariston continuam em pt-BR.
- Cuidado com `settings_data.json` e `settings_schema.json` (já houve vírgula quebrando o JSON, corrigida em PR separado).
- Tarefas de DNS e GTmetrix não são de código: o Mestre trata com o Kariston.

## Pendências conhecidas

- GDA-59 (apontamento DNS) e GDA-61 (avaliação GTmetrix, rodar após o Go-Live) em refinamento.
