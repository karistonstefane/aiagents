# Projeto: Tema - Race Tech

## Identificação

- **Nome do time:** Tema - Race Tech
- **Cliente:** Race Tech
- **Bots:** `Tema - Race Tech · Gerente`, `· Dev`, `· Designer`, `· Revisor` (ids no `registry.json`)

## Loja(s)

- **Loja:** `brmotorsport-01-re0rgmhc.myshopify.com` (citada em RT-74)
- **Domínio:** ainda não tem
- **Tema publicado / base:** "[Check] Desenvolvimento" (Pebble 1.4.0, FoxEcom), conectado à `master`. É o tema publicado; a loja ainda está em desenvolvimento. Id numérico do tema: não informado.
- **Plano:** Shopify Plus (citado em RT-71)

## Repositório

- **Local:** `~/projects/race-tech` (`C:\Users\Kariston\projects\race-tech`)
- **GitHub:** `checkstore/race-tech`
- **Branch base:** `master` (o tema publicado "[Check] Desenvolvimento" está conectado à `master`: o merge publica o tema conectado). A `master` também recebe commits automáticos do Shopify bot

## Revisão

- **revisor:** `bot`
- **revisor_github:** não se aplica
- **deploy:** Kariston (o merge na `master` publica o tema conectado; a loja ainda está em desenvolvimento)

## Design

- **designer:** `sim`
- **figma:** não há

Tarefas com impacto visual/UI passam pelo Designer depois da validação do Kariston e antes do Dev. Não há Figma: é um tema comprado da loja Shopify (Pebble). O Designer deve apenas manter o padrão visual do tema.

## Arquitetura

- **Arquivo:** [`projects/tema-race-tech.arquitetura.md`](./tema-race-tech.arquitetura.md). Leia antes de refinar, desenhar ou implementar; o Dev atualiza no mesmo ciclo do PR quando a mudança afetar a arquitetura.

## Jira

- **Projeto / prefixo:** `RT`
- **Filtro do Gerente:** `project = RT AND status = "Para fazer" AND assignee = "Kariston Stefane"`
- **Reuniões externas:** `RT-2`

## Contatos

- Mayara Silveira: Gerente de Projetos (GP)
- Também no Jira: Marina Calinowski (lead do projeto RT); Enrique (reporter frequente de ajustes de tema); Paulo Damasco, Raphael Gorska e Suellen Menezes (contatos do cliente em RT-8, e-mails @brms.com.br)

## Convenções

- Branch: `feat/RT-<n>-<slug>` ou `fix/RT-<n>-<slug>`. PR contra `master`, com roteiro de teste e link do preview. Review do bot Revisor; merge manual do Kariston. O merge na `master` publica o tema conectado.
- Commits pequenos, com a chave do Jira na mensagem. O histórico anterior tem muitos syncs do Shopify bot ("Update from Shopify for theme [Check] Desenvolvimento") e commits manuais em português sem a chave; a partir de agora, incluir a chave.

## Regras específicas

- Tema baseado no **Pebble 1.4.0** (FoxEcom), comprado na loja Shopify: preferir blocos/seções nativos e manter o padrão visual e a compatibilidade com atualizações do tema base. Não há Figma.
- A `master` está conectada ao tema publicado "[Check] Desenvolvimento": o merge publica o tema. A loja ainda está em desenvolvimento. A `master` também recebe atualizações automáticas do editor Shopify. Cuidado ao rebase/merge.
- Locales: `en` (default), `pt-BR`, `de`, `es`, `fr`, `it`, `vi`. Não há `pt-BR.schema.json`.
- Banner de coleção: ocultar quando não houver imagem ou o metafield do banner estiver vazio (RT-72).

## Pendências conhecidas

- Nenhuma registrada.
