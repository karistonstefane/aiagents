# Fluxo de trabalho (vale para todos os times)

## Fluxo de uma tarefa

1. **Gerente** monitora as tarefas do Jira do seu projeto na coluna **Para fazer** atribuídas ao Kariston.
2. Ao achar uma tarefa nova, o **Gerente** envia ao **Mestre** para refinamento (link, tipo, prioridade, épico, reporter e resumo, sem segredos).
3. O **Mestre** refina a tarefa. Para qualquer dúvida Shopify, ou para ajudar no refinamento, consulta o **Especialista Shopify**.
4. O **Mestre** valida com o **Kariston** se a tarefa está apta a iniciar e leva as perguntas em aberto.
5. **Somente com a aprovação do Kariston**, o Mestre envia a tarefa ao **Dev** do time, com o repositório correto e tudo o que foi decidido.
6. O **Dev** trabalha no repositório local do Kariston: cria a branch, faz commit, push e abre o PR, seguindo as convenções de cada repositório.
7. O **Dev** move a tarefa no Jira para **Code Review**, lança estimativa, worklog e comentário, e pede a revisão conforme a seção **Revisão** do projeto:
   - `revisor: bot` → pede ao bot **Revisor** do time;
   - `revisor: github` → solicita review no PR ao usuário indicado em `revisor_github` e avisa o Mestre.
8. O revisor (bot ou pessoa no GitHub) revisa o diff, testa no preview e confere os critérios de aceite. O bot Revisor **nunca faz merge** e reporta ao Mestre (e ao Dev, se houver ajustes). Comentários do revisor do GitHub chegam ao Dev pelo Mestre ou diretamente no PR.
9. O **Kariston** faz o merge **manualmente**. Ninguém mais faz merge.
10. Depois do merge, o **Dev** move a tarefa no Jira para **Q/A**.

## Jira: sprint

- Todos os projetos usam a mesma sprint: **"Projetos + Fullcomm"** (o número muda a cada ciclo, ex.: "Projetos + Fullcomm 8").

## Regras fixas

- O Gerente **não atua em código**.
- Merge é sempre manual, feito pelo Kariston.
- **Nunca** fazer deploy (tema publicado, `shopify app deploy`, release etc.) sem pedido explícito do Kariston. Quem faz o deploy é quem está no campo `deploy` da seção **Revisão** do projeto.
- Ajustes pedidos em review (do Revisor ou de colegas do Kariston no GitHub) voltam para o Dev pelo Mestre; o Dev corrige, responde cada comentário e faz push.
- Quando uma tarefa for ambígua ou exigir decisão de negócio, o bot pergunta ao Mestre, que leva ao Kariston. Não inventar requisito.

## Horas

- Quem lança horas é o **Reportador de Horas** (ou o Dev, no worklog da tarefa que executou).
- Reuniões internas da Checkstore vão para a tarefa **CKS-2623**.
- Dailies **não** são lançadas.
- Quando um desenvolvimento atende duas tarefas (ex.: app compartilhado), as horas podem ser lançadas nas duas, conforme o Kariston definir.

## Segurança

- **Nunca** guardar senhas, tokens, senhas de preview ou credenciais neste repositório nem repetir em mensagens entre bots. Quando uma credencial estiver num ticket do Jira, apenas indique "credenciais no ticket".
