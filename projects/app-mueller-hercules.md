# Projeto: App - Mueller e Hercules

## Identificação

- **Nome do time:** App - Mueller e Hercules
- **Cliente:** Mueller e Hércules Motores (app compartilhado)
- **Bots:** `App - Mueller e Hercules · Gerente` e `· Dev` (ids no `registry.json`). **Sem bot Revisor**: a revisão é feita no GitHub pelo Victor.

## Loja(s)

O mesmo app (custom app, multi-tenant) roda nas duas lojas:

- `totvsle-mueller.myshopify.com`
- `totvsle-herculesmotores.myshopify.com`

Ambas no plano Shopify Plus. As duas lojas já estão com o app instalado e funcionando. O deploy atende as duas.

## Repositório

- **Local:** `~/projects/ca-herculesmueller` (`C:\Users\Kariston\projects\ca-herculesmueller`)
- **GitHub:** `checkstore/app-b2b-connect` (atenção: o nome da pasta local é diferente do nome no GitHub)
- **Branch base:** `main`
- **Stack:** app Remix multi-tenant (Shopify), com extensões como `b2b-company-registration` e a Discount Function de desconto por segmento.
- **Infra:** roda em Docker no servidor, um container por tenant (ex.: `b2b-app-hercules`), com env por tenant (ex.: `.env.hercules`, fora do Git).

## Revisão

- **revisor:** `github`
- **revisor_github:** `victorcesc` (Victor)
- **deploy:** Victor (`victorcesc`). Nem o Dev nem o Kariston fazem o deploy deste app.

O Dev solicita a revisão do Victor no PR (`--add-reviewer victorcesc`) e avisa o Mestre. Os apontamentos do Victor são corrigidos pelo Dev, que responde cada comentário no PR.

## Jira

- **Projetos / prefixos:** `MUEL` **e** `HCL`
- **Filtro do Gerente:** `project in (MUEL, HCL) AND assignee = "Kariston Stefane"`, usado **só para acompanhar** as tarefas que o Mestre atribuiu a este time.
- **Roteamento (ver "Roteamento MUEL/HCL: app x tema" em `shared/workflow.md`):** o app não é um projeto separado no Jira e as labels não são confiáveis, então a classificação é **pelo conteúdo**, feita pelo Mestre e validada pelo Kariston. Este Gerente **não encaminha** tarefas `MUEL`/`HCL` ao Mestre por conta própria (quem encaminha são os Gerentes do Tema - Mueller e do Tema - Hercules) e **nunca assume** uma tarefa pela chave. Ele só recebe do Mestre as tarefas já classificadas como App e acompanha essas (comentários, prioridade, vencimento).
- **Tarefa que mexe em app e tema:** fica neste time; o Mestre, com a validação do Kariston, abre um follow-up vinculado para o time de tema.
- **Horas:** sempre na chave original. Uma mesma entrega pode atender uma tarefa MUEL e uma HCL (ex.: MUEL-270 + HCL-236): faz-se **um único desenvolvimento** e as horas e transições são lançadas **nas duas tarefas**.

## Contatos

- Charline Lima: Gerente de Projetos (GP)
- Victor (`victorcesc`): revisor no GitHub e responsável pelos deploys

## Convenções

- Branch: `feat/<chave-minúscula>-<slug>` quando atende mais de uma tarefa (ex.: `feat/muel-270-hcl-236-desconto-segmento`), ou `feat|fix/<CHAVE>-<n>`.
- PR contra `main`, com roteiro de teste e pendências pós-deploy (escopos novos, setup por loja, QA em cada loja).

## Regras específicas

- **Deploy e release** (`shopify app deploy`) ficam com o **Victor** e liberam a versão nas duas lojas ao mesmo tempo. Os bots nunca fazem deploy; no PR, liste o que o Victor precisa fazer no deploy.
- Mudança de escopo exige reautorização do app nas duas lojas: sempre listar no PR.
- Configurações por loja (discount automático, metafields de config) precisam ser criadas em **cada** loja.
- Segmentos B2B ficam em metafields da Company Location: `checkstore.regional`, `checkstore.regiao`, `checkstore.setor`, `checkstore.equipe`, `checkstore.grupo_clientes`.
- Desconto por segmento (MUEL-270/HCL-236): grupos por metafield de segmento + valores, cada um com uma %; desconto de **pedido**; acumula com as tabelas de preço (aplica por cima do catálogo); se a location cair em mais de um grupo, vale o **maior**. Lojas 100% B2B, sem cupons.
- Cadastro B2B (`b2b-company-registration`): consulta o SAP para preencher o endereço da empresa; controlado pela env `SAP_ADDRESS_CONSULT_ENABLED` por tenant (`false` desliga).
- Nunca commitar arquivos `.env` nem tokens do SAP/Shopify.

## Pendências conhecidas

- PR #75 (MUEL-270/HCL-236): ajustes do review do victorcesc em andamento; depois merge (Kariston), deploy (Victor), reautorização (`write_discounts`), setup por loja e QA. Teto de % por grupo (hoje 100%) a decidir pelo Kariston.
- Cadastro B2B ainda gerando empresas com "Endereço Pendente" na Hércules: consulta SAP estava desligada no tenant (`disabled for this tenant`) e depende da liberação do `IV_CONS_ENDERECO` no SAP.
