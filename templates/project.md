# Projeto: <Tipo> - <Cliente>

> Copie este arquivo para `projects/<tipo>-<cliente>.md` e preencha. Marque o que não souber como `A CONFIRMAR`. **Não coloque senhas nem credenciais.**

## Identificação

- **Nome do time:** <Tipo> - <Cliente>
- **Cliente:** <nome do cliente>
- **Bots:** `<Tipo> - <Cliente> · Gerente`, `· Dev`, `· Designer` (se `designer: sim`) e `· Revisor` (se `revisor: bot`) (ids no `registry.json`)

## Loja(s)

- **Loja:** `<loja>.myshopify.com`
- **Domínio:** A CONFIRMAR
- **Tema publicado / base:** A CONFIRMAR
- **Plano:** A CONFIRMAR

## Repositório

- **Local:** `~/projects/<pasta>`
- **GitHub:** `checkstore/<repo>`
- **Branch base:** `master` | `main`

## Revisão

- **revisor:** `bot` | `github`
- **revisor_github:** `<handle do GitHub>` (só quando `revisor: github`)
- **deploy:** <quem faz o deploy/publicação, ex.: Kariston, ou o revisor do GitHub>

Com `revisor: github` não é criado bot Revisor: o Dev solicita review no PR ao `revisor_github` e avisa o Mestre.

## Design

- **designer:** `sim` | `não`
- **figma:** <link do arquivo> | `não há` | `não informado`

Com `designer: sim`, tarefas com impacto visual/UI passam pelo Designer depois da validação do Kariston e antes do Dev. Use `não informado` quando não souber se existe Figma.

## Jira

- **Projeto / prefixo:** `<PREFIXO>`
- **Filtro do Gerente:** `project = <PREFIXO> AND status = "Para fazer" AND assignee = currentUser()` (ajustar)

## Contatos

- A CONFIRMAR

## Convenções

- Branch: `<tipo>/<PREFIXO>-<n>[-slug]`
- PR contra a branch base, com roteiro de teste.

## Regras específicas

- A CONFIRMAR

## Pendências conhecidas

- Nenhuma.
