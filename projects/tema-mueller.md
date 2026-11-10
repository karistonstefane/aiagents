# Projeto: Tema - Mueller

## Identificação

- **Nome do time:** Tema - Mueller
- **Cliente:** Mueller
- **Bots:** `Tema - Mueller · Gerente`, `· Dev`, `· Designer`, `· Revisor` (ids no `registry.json`)

## Loja(s)

- **Loja:** `totvsle-mueller.myshopify.com` (loja B2B)
- **Domínio:** ainda não definido
- **Tema publicado:** "[Check] Mueller", conectado à branch `master`
- **Plano:** Shopify Plus

## Repositório

- **Local:** `~/projects/mueller` (`C:\Users\Kariston\projects\mueller`)
- **GitHub:** `checkstore/mueller`
- **Branch base:** `master` (o tema publicado está conectado à `master`: merge nela afeta a loja)

## Revisão

- **revisor:** `bot`
- **revisor_github:** —
- **deploy:** Kariston (o merge na `master` publica o tema conectado)

## Design

- **designer:** `sim`
- **figma:** não informado

Tarefas com impacto visual/UI passam pelo Designer depois da validação do Kariston e antes do Dev. Sem Figma, o Designer segue o padrão existente do tema.

## Jira

- **Projeto / prefixo:** `MUEL`
- **Filtro do Gerente:** `project = MUEL AND status = "Para fazer" AND assignee = "Kariston Stefane"`
- **Roteamento (ver "Roteamento MUEL/HCL: app x tema" em `shared/workflow.md`):** este Gerente é o **único** que encaminha as tarefas `MUEL` ao Mestre, **todas**, inclusive as que parecerem de app. Ele não assume nenhuma pela chave: o Mestre classifica como App ou Tema pelo conteúdo, valida com o Kariston e só então envia ao time escolhido. Este time só trabalha nas tarefas classificadas como Tema.

## Contatos

- Charline Lima: Gerente de Projetos (GP)

## Convenções

- Branch: `fix/MUEL-<n>` ou `feat/MUEL-<n>` (ex.: `fix/MUEL-271`, PR #34).
- PR contra `master`, com roteiro de teste e link do preview.
- Depois do merge, a tarefa vai para **Q/A**.

## Regras específicas

- Variantes de produto usam metafields de **cor** e **tensão** e um metafield de **grupo de produto** para agrupar produtos (ex.: centrífugas). Trocar só a cor deve manter a tensão selecionada.
- Loja 100% B2B: preços vêm de catálogos/price lists B2B.

## Pendências conhecidas

- Nenhuma registrada.
