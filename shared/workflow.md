# Fluxo de trabalho (vale para todos os times)

## Fluxo de uma tarefa

1. **Gerente** monitora as tarefas do Jira do seu projeto na coluna **Para fazer** atribuídas ao Kariston.
2. Ao achar uma tarefa nova, o **Gerente** envia ao **Mestre** para refinamento (link, tipo, prioridade, épico, reporter e resumo, sem segredos).
3. O **Mestre** refina a tarefa. Antes de propor uma solução, o Mestre lê o **arquivo de arquitetura do projeto** (`projects/<slug>.arquitetura.md`). Para qualquer dúvida Shopify, ou para ajudar no refinamento, consulta o **Especialista Shopify**, que também lê o arquivo de arquitetura antes de recomendar.
4. O **Mestre** valida com o **Kariston** se a tarefa está apta a iniciar e leva as perguntas em aberto.
5. **Somente com a aprovação do Kariston**, o Mestre segue para a execução:
   - se a tarefa tem **impacto visual/UI** e o projeto tem `designer: sim`, o Mestre envia primeiro ao **Designer** do time, com o link do Figma quando existir;
   - o Designer devolve ao Mestre as **"Diretrizes de design"**. Quando for proposta sem Figma, o Mestre mostra ao Kariston para aprovação;
   - o Mestre envia a tarefa ao **Dev** do time, com o repositório correto, tudo o que foi decidido e as Diretrizes de design (quando houver).
6. O **Dev** trabalha no repositório local do Kariston: cria a branch, faz commit, push e abre o PR, seguindo as convenções de cada repositório e as Diretrizes de design. Diretriz pouco clara: pergunta ao Mestre.
7. O **Dev** move a tarefa no Jira para **Code Review**, lança estimativa, worklog e comentário, e pede a revisão conforme a seção **Revisão** do projeto:
   - `revisor: bot` → pede ao bot **Revisor** do time;
   - `revisor: github` → solicita review no PR ao usuário indicado em `revisor_github` e avisa o Mestre.
8. O revisor (bot ou pessoa no GitHub) revisa o diff, testa no preview, confere os critérios de aceite e verifica se a entrega segue as **Diretrizes de design**. O bot Revisor **nunca faz merge** e reporta ao Mestre (e ao Dev, se houver ajustes). Comentários do revisor do GitHub chegam ao Dev pelo Mestre ou diretamente no PR.
9. O **Kariston** faz o merge **manualmente**. Ninguém mais faz merge.
10. Depois do merge, o **Dev** move a tarefa no Jira para **Q/A**.

## Roteamento MUEL/HCL: app x tema

O custom app B2B (`checkstore/app-b2b-connect`, pasta local `ca-herculesmueller`) **não é um projeto separado no Jira**: as tarefas dele chegam como `MUEL` ou `HCL`, junto com as de tema, e as labels do Jira não são confiáveis. Por isso a classificação é feita **pelo conteúdo** da tarefa. O Kariston pediu: "precisamos ter muito cuidado com isso".

1. **Nenhum Gerente assume tarefa pela chave.** Toda tarefa `MUEL` e `HCL` vai primeiro ao **Mestre**.
2. **Quem encaminha (para não duplicar):** só o Gerente do tema daquela chave encaminha ao Mestre: `MUEL` → Gerente do **Tema - Mueller**; `HCL` → Gerente do **Tema - Hercules**. O Gerente do **App - Mueller e Hercules** **não** encaminha tarefas `MUEL`/`HCL` por conta própria; ele só recebe do Mestre as tarefas já classificadas como App e acompanha essas.
3. **O Mestre classifica pelo conteúdo** (título, descrição, critérios de aceite, anexos e comentários):
   - **Sinais de App:** custom app, `app-b2b-connect` / `ca-herculesmueller`, extension, Discount/Shopify Function, checkout extension, SAP/OMS/integração, cadastro B2B de empresas, painel/B2B Connect, webhooks, app proxy.
   - **Sinais de Tema:** Liquid, sections/blocks, Personalizar, layout, CSS/JS do tema, páginas, templates de produto/coleção.
4. **Validação com o Kariston:** ao pedir a validação da tarefa, o Mestre **sempre mostra a classificação (App ou Tema) e o motivo**. Se houver **qualquer dúvida**, o Mestre pergunta ao Kariston em vez de decidir. Só depois da validação do Kariston a tarefa vai para o time escolhido.
5. **Tarefa que mexe nos dois:** fica no time **App**. O Mestre, com a validação do Kariston, abre uma tarefa de follow-up vinculada para o time de tema correspondente.
6. **Horas:** sempre lançadas na chave original da tarefa. Um desenvolvimento que atende uma tarefa `MUEL` e uma `HCL` lança horas nas duas.

## Arquivo de arquitetura do projeto

Cada projeto tem `projects/<slug>.arquitetura.md` (modelo em `templates/arquitetura.md`) com visão geral, stack, integrações, apps/extensões, dados, módulos principais, decisões de arquitetura, armadilhas e histórico.

- **Quem lê:** o Mestre e o Especialista Shopify no refinamento, antes de propor solução; o Designer antes de propor diretrizes; o Dev antes de implementar.
- **Quem atualiza:** o Dev, **no mesmo ciclo do PR** (como o arquivo vive neste repositório, ele abre um PR complementar no `aiagents` junto com o PR do projeto e cita os dois), sempre que a mudança afetar a arquitetura (nova integração, metafield, section/block, extensão, Function, decisão).
- **Quem confere:** o Revisor (bot). Nos projetos com revisor no GitHub, o Dev declara no PR se o arquivo foi atualizado ou por que não foi necessário.
- **Decisão (2026-11-10):** o Kariston escolheu manter um arquivo de arquitetura por projeto **em vez de um bot Arquiteto**. Um bot Arquiteto pode ser reavaliado se os arquivos ficarem grandes demais ou se as soluções propostas continuarem errando por falta de contexto.

## Jira: sprint

- Todos os projetos usam a mesma sprint: **"Projetos + Fullcomm"** (o número muda a cada ciclo, ex.: "Projetos + Fullcomm 8").

## Regras fixas

- O Gerente **não atua em código**. O Designer também não edita código: entrega diretrizes.
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
