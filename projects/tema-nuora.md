# Projeto: Tema - Nuora

## Identificação

- **Nome do time:** Tema - Nuora
- **Cliente:** Nuora Cosméticos
- **Bots:** `Tema - Nuora · Gerente`, `· Dev`, `· Designer`, `· Revisor` (ids no `registry.json`)

## Loja(s)

- **Loja:** `nuora-cosmetic.myshopify.com`
- **Domínio:** `nuora.com.br`
- **Tema publicado:** "[CS] Check V3" (Horizon 3.3.1, id 150333259818), conforme 25/11/2026 (NU-67). O id 146770460714 ("[CS] Check V1" de 06/11/2026) não existe mais.
- **Tema conectado à `master`:** um "[CS] Check V1" **não publicado** (#150218735658 ou #150255403050, não confirmado qual).

## Repositório

- **Local:** `~/projects/nuoracosmetic` (`C:\Users\Kariston\projects\nuoracosmetic`)
- **GitHub:** `checkstore/nuoracosmetic`
- **Branch base:** `master` (conectada ao "[CS] Check V1" não publicado, não ao V3 publicado: merge nela atualiza o V1 conectado; quem publica é o Kariston)

## Revisão

- **revisor:** `bot`
- **revisor_github:** —
- **deploy:** Kariston (o merge na `master` atualiza o V1 conectado; a publicação na loja é feita pelo Kariston)

## Design

- **designer:** `sim`
- **figma:** não informado

Tarefas com impacto visual/UI passam pelo Designer depois da validação do Kariston e antes do Dev. Sem Figma, o Designer segue o padrão existente do tema.

## Arquitetura

- **Arquivo:** [`projects/tema-nuora.arquitetura.md`](./tema-nuora.arquitetura.md). Leia antes de refinar, desenhar ou implementar; o Dev atualiza no mesmo ciclo do PR quando a mudança afetar a arquitetura.

## Jira

- **Projeto / prefixo:** `NU`
- **Filtro do Gerente:** `project = NU AND status = "Para fazer" AND assignee = "Kariston Stefane"`

## Contatos

- Mayara: Gerente de Projetos (GP)

## Convenções

- Branch: `feature/NU-<n>-<slug>` (ex.: `feature/NU-67-gtm-password-page`).
- PR contra `master`, com roteiro de teste e link do preview.

## Regras específicas

- Tema baseado no Horizon: preferir blocos/seções nativos e manter compatibilidade com atualizações do tema base.
- GTM `GTM-KMGQRKMN` instalado também na página de senha (NU-67).

## Pendências conhecidas

- Nenhuma registrada.
