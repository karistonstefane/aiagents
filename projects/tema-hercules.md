# Projeto: Tema - Hercules

## Identificação

- **Nome do time:** Tema - Hercules
- **Cliente:** Hércules Motores
- **Bots:** `Tema - Hercules · Gerente`, `· Dev`, `· Designer`, `· Revisor` (ids no `registry.json`)

## Loja(s)

- **Loja:** `totvsle-herculesmotores.myshopify.com` (loja B2B)
- **Domínio:** `herculesenergia.com.br`
- **Tema publicado:** acompanha a branch `master` do repositório
- **Plano:** Shopify Plus

## Repositório

- **Local:** `~/projects/hercules` (`C:\Users\Kariston\projects\hercules`)
- **GitHub:** `checkstore/hercules`
- **Branch base:** `master` (o tema publicado acompanha a `master`: merge nela afeta a loja)

## Revisão

- **revisor:** `bot`
- **revisor_github:** —
- **deploy:** Kariston (o merge na `master` publica o tema conectado)

## Design

- **designer:** `sim`
- **figma:** não informado

Tarefas com impacto visual/UI passam pelo Designer depois da validação do Kariston e antes do Dev. Sem Figma, o Designer segue o padrão existente do tema.

## Arquitetura

- **Arquivo:** [`projects/tema-hercules.arquitetura.md`](./tema-hercules.arquitetura.md). Leia antes de refinar, desenhar ou implementar; o Dev atualiza no mesmo ciclo do PR quando a mudança afetar a arquitetura.

## Jira

- **Projeto / prefixo:** `HCL`
- **Filtro do Gerente:** `project = HCL AND status = "Para fazer" AND assignee = "Kariston Stefane"`
- **Roteamento (ver "Roteamento MUEL/HCL: app x tema" em `shared/workflow.md`):** este Gerente é o **único** que encaminha as tarefas `HCL` ao Mestre, **todas**, inclusive as que parecerem de app. Ele não assume nenhuma pela chave: o Mestre classifica como App ou Tema pelo conteúdo, valida com o Kariston e só então envia ao time escolhido. Este time só trabalha nas tarefas classificadas como Tema.

## Contatos

- Charline Lima: Gerente de Projetos (GP)

## Convenções

- Branch: `feat/HCL-<n>` ou `fix/HCL-<n>` (ex.: `feat/HCL-233`).
- PR contra `master`, com roteiro de teste e link do preview.

## Regras específicas

- Como o tema publicado acompanha a `master`, o merge equivale a publicar. Reforço: merge só pelo Kariston.
- Contatos do Fale Conosco (WhatsApp e e-mail) só viram link quando os campos do Personalizar estão preenchidos (HCL-233).
- Loja 100% B2B.

## Pendências conhecidas

- Nenhuma registrada.
