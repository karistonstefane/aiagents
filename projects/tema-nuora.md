# Projeto: Tema - Nuora

## Identificação

- **Nome do time:** Tema - Nuora
- **Cliente:** Nuora Cosméticos
- **Bots:** `Tema - Nuora · Gerente`, `· Dev`, `· Designer`, `· Revisor` (ids no `registry.json`)

## Loja(s)

- **Loja:** `nuora-cosmetic.myshopify.com`
- **Domínio:** `nuora.com.br`
- **Tema publicado / base:** "[CS] Check V1" (Horizon 3.3.1, id 146770460714), conforme 06/11/2026

## Repositório

- **Local:** `~/projects/nuoracosmetic` (`C:\Users\Kariston\projects\nuoracosmetic`)
- **GitHub:** `checkstore/nuoracosmetic`
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
