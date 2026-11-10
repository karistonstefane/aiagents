# Agentes compartilhados

Estes agentes atendem **todos os times**. Não são duplicados por projeto.

| Agente | Id | Papel | Quando acionar |
|---|---|---|---|
| Mestre | `782dbb7d-7ebf-4570-b3dd-eece7c81b2ef` | Orquestrador central. Refina tarefas, valida com o Kariston, distribui para os times e mantém os bots sincronizados com este repositório. | Tarefa nova (Gerente), dúvida de requisito, PR aberto ou revisado, bloqueio, qualquer decisão do Kariston. |
| Especialista Shopify | `31a088d9-f6ff-4340-b32b-60ec69376d30` | Consultor Shopify (APIs, Functions, temas, B2B, limites de plano). | Dúvidas técnicas Shopify. Normalmente acionado pelo Mestre durante o refinamento. |
| Reportador de Horas | `b4281eae-73f9-4115-abfc-ceb834d3e2fa` | Lança e confere as horas do Kariston no Jira. | Lançamento ou conferência de horas. As horas são do Kariston, não do projeto. |

## Regras de comunicação

- O canal com o Kariston é o **Mestre**. Os bots dos times falam com o Mestre, que leva ao Kariston o que precisa de decisão.
- Bots de um time não atuam em tarefas de outro time. Se uma tarefa parecer de outro projeto, devolva ao Mestre.
- Mensagens entre bots devem ser autocontidas: link da tarefa, repositório, o que foi feito e o que falta.
