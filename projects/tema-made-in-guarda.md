# Projeto: Tema - Made in Guarda

## Identificação

- **Nome do time:** Tema - Made in Guarda
- **Cliente:** Made in Guarda
- **Bots:** `Tema - Made in Guarda · Gerente`, `· Dev`, `· Revisor` (ids no `registry.json`)

## Loja(s)

- **Loja:** A CONFIRMAR (`*.myshopify.com`)
- **Domínio:** A CONFIRMAR (DNS gerenciado no painel da SAN Internet / Cloud)
- **Tema publicado / base:** A CONFIRMAR

## Repositório

- **Local:** `~/projects/made-in-guarda` (`C:\Users\Kariston\projects\made-in-guarda`)
- **GitHub:** `checkstore/made-in-guarda`
- **Branch base:** `master`

## Jira

- **Projeto / prefixo:** `GDA`
- **Filtro do Gerente:** `project = GDA AND status = "Para fazer" AND assignee = "Kariston Stefane"`
- Épico de publicação: GDA-13 (Publicação e Monitoramento).

## Contatos

- Enrique: reporter das tarefas GDA (papel A CONFIRMAR).
- Mayara: liberou os acessos ao painel SAN/Cloud (papel A CONFIRMAR).

## Convenções

- Branch: `feat/GDA-<n>` ou `fix/GDA-<n>` (ex.: `feat/GDA-173`).
- PR contra `master`, com roteiro de teste e link do preview.

## Regras específicas

- **Labels dos schemas do tema ficam em inglês** (exceção à regra do pt-BR). As respostas aos bots e ao Kariston continuam em pt-BR.
- Cuidado com `settings_data.json` e `settings_schema.json` (já houve vírgula quebrando o JSON, corrigida em PR separado).
- Tarefas de DNS e GTmetrix não são de código: o Mestre trata com o Kariston.

## Pendências conhecidas

- GDA-59 (apontamento DNS) e GDA-61 (avaliação GTmetrix, rodar após o Go-Live) em refinamento.
