# Projeto: Tema - Espaço Prime

## Identificação

- **Nome do time:** Tema - Espaço Prime
- **Cliente:** Espaço Prime
- **Bots:** `Tema - Espaço Prime · Gerente`, `· Dev`, `· Designer`, `· Revisor` (ids no `registry.json`)

## Loja(s)

- **Loja:** `espaco-prime-05iifq98.myshopify.com`
- **Domínio:** A CONFIRMAR (o e-mail de atendimento da loja usa `espacoprime.com.br`; a configuração de DNS, EP-15, está em Backlog)
- **Tema publicado / base:** "[Check] Desenvolvimento" (Expanse 10.0.1, Archetype Themes), conectado à `master`. Se é o tema publicado: A CONFIRMAR. Id numérico do tema: não informado.
- **Plano:** **não é Shopify Plus** (confirmado pelo Kariston em 27/11/2026). Plano exato: não informado.

## Repositório

- **Local:** `~/projects/espaco-prime` (`C:\Users\Kariston\projects\espaco-prime`)
- **GitHub:** `checkstore/espaco-prime`
- **Branch base:** `master` (única branch; conectada ao tema "[Check] Desenvolvimento" e com commits automáticos do Shopify bot)
- **Pastas:** trabalhe sempre dentro de `projects\espaco-prime`. Não crie pastas nem arquivos soltos na raiz de `projects`.

## Revisão

- **revisor:** `bot`
- **revisor_github:** não se aplica
- **deploy:** Kariston (merge manual na `master`; publicação do tema só com pedido explícito dele)

## Design

- **designer:** `sim`
- **figma:** não informado

Tarefas com impacto visual/UI passam pelo Designer depois da validação do Kariston e antes do Dev. Sem Figma, o Designer mantém o padrão visual do tema Expanse já configurado na loja.

## Arquitetura

- **Arquivo:** [`projects/tema-espaco-prime.arquitetura.md`](./tema-espaco-prime.arquitetura.md). Leia antes de refinar, desenhar ou implementar; o Dev atualiza no mesmo ciclo do PR quando a mudança afetar a arquitetura.

## Jira

- **Projeto / prefixo:** `EP`
- **Filtro do Gerente:** `project = EP AND status = "Para fazer" AND assignee = "Kariston Stefane"`
- **Reuniões externas:** `EP-4`
- **Reuniões internas do projeto:** `EP-3`
- **Depois do merge:** a tarefa vai para **Homologação** (o fluxo do EP não tem Q/A; confirmado pelo Kariston em 27/11/2026).

## Contatos

- Mayara Silveira: Gerente de Projetos (GP)
- Também no Jira e no histórico do tema: Marina Calinowski (acessos da Check, EP-75); Denner Moraes, Fabiano Trichez, Tiago Wasielewski, Leticia Almeida Gioia e Gabriel Fernandes (tarefas e ajustes anteriores). Papéis exatos: não informados.

## Convenções

- Branch: `feat/EP-<n>-<slug>` ou `fix/EP-<n>-<slug>`. PR contra `master`, com roteiro de teste e link do preview. Review do bot Revisor; merge manual do Kariston.
- Commits pequenos, com a chave do Jira na mensagem. O histórico anterior é quase todo de syncs do Shopify bot ("Update from Shopify for theme [Check] Desenvolvimento"); a partir de agora, incluir a chave.

## Regras específicas

- Tema baseado no **Expanse 10.0.1** (Archetype Themes): preferir seções e blocos nativos e manter a compatibilidade com atualizações do tema base.
- **Não é Plus:** não há checkout UI extensions nem Functions ou customizações de checkout exclusivas do Plus. As soluções passam pelo tema, pelo Shopify Flow, pelo Shopify Forms ou por apps.
- A `master` recebe atualizações automáticas do editor Shopify. Cuidado ao rebase/merge, e não commitar `config/settings_data.json` nem templates JSON sem intenção.
- Locales: `en` (default), `pt-BR` (com `pt-BR.schema.json`), `pt-PT`, `de`, `es`, `fr`, `it`.
- **Cadastro B2B (EP-92):** formulário do Shopify Forms (form `1175431`) nas páginas `page.cadastre-sua-empresa` e `page.atacado`. Caminho escolhido pelo Kariston em 27/11/2026: Forms cria a Company, a location e o cliente; Flow de aprovação automática (template "Allow ordering for companies created by company account requests"); o tema grava os cart attributes `razao_social`, `cnpj` e `ie` a partir da empresa do cliente logado; Flow de reforço em Order created completa atributos e nota quando faltarem. Detalhes em `projects/tema-espaco-prime.arquitetura.md`.
- Criar, alterar ou ativar Flows, formulários, metafields ou configurações da loja só com aprovação do Kariston, via Mestre.

## Pendências conhecidas

- EP-92 (Fluxo de cadastro B2B) em andamento.
- Domínio e se "[Check] Desenvolvimento" é o tema publicado: A CONFIRMAR.
- Quais campos a Anymarket lê do pedido (`note_attributes`, nota, `company`) e qual é a integração com o ERP: A CONFIRMAR.
