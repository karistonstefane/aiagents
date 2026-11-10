# aiagents

Fonte da verdade das instruções dos bots da Checkstore usados pelo Kariston Stefane.

Cada projeto tem o **seu próprio time de bots** (Gerente, Dev, Designer e, quando configurado, Revisor), com memória separada, para evitar mistura de contexto entre clientes. Alguns agentes são **compartilhados** por todos os times (Mestre, Especialista Shopify e Reportador de Horas).

## Estrutura

```
aiagents/
├── README.md                  # este arquivo
├── roles/                     # instrução base de cada papel (vale para todo projeto)
│   ├── gerente.md
│   ├── dev.md
│   ├── designer.md
│   └── revisor.md
├── shared/                    # regras comuns a todos os bots
│   ├── workflow.md            # fluxo de uma tarefa, do Jira ao merge
│   ├── idioma-e-tom.md        # idioma, tom, aprovações, comandos no PC
│   └── agentes-compartilhados.md  # Mestre, Especialista Shopify, Reportador
├── projects/                  # um arquivo por time/projeto
│   ├── tema-mueller.md
│   ├── tema-mueller.arquitetura.md
│   ├── tema-hercules.md
│   ├── tema-hercules.arquitetura.md
│   ├── app-mueller-hercules.md
│   ├── app-mueller-hercules.arquitetura.md
│   ├── tema-made-in-guarda.md
│   ├── tema-made-in-guarda.arquitetura.md
│   ├── tema-nuora.md
│   └── tema-nuora.arquitetura.md
├── templates/
│   ├── project.md             # modelo para projeto novo
│   └── arquitetura.md         # modelo do arquivo de arquitetura do projeto
└── registry.json              # mapa projeto → ids dos bots criados (mantido pelo Mestre)
```

## Times iniciais

| Time | Arquivo | Jira | Repositório | Revisão | Designer |
|---|---|---|---|---|---|
| Tema - Mueller | `projects/tema-mueller.md` | MUEL | `checkstore/mueller` | bot | sim |
| Tema - Hercules | `projects/tema-hercules.md` | HCL | `checkstore/hercules` | bot | sim |
| App - Mueller e Hercules | `projects/app-mueller-hercules.md` | MUEL + HCL (só tarefas classificadas como App pelo Mestre) | `checkstore/app-b2b-connect` | GitHub: `victorcesc` | sim (Polaris) |
| Tema - Made in Guarda | `projects/tema-made-in-guarda.md` | GDA | `checkstore/made-in-guarda` | bot | sim |
| Tema - Nuora | `projects/tema-nuora.md` | NU | `checkstore/nuoracosmetic` | bot | sim |

### Roteamento MUEL/HCL

O app B2B não é um projeto separado no Jira e as labels não são confiáveis: as tarefas `MUEL`/`HCL` são classificadas como **App** ou **Tema** **pelo conteúdo**. Os Gerentes do Tema - Mueller (`MUEL`) e do Tema - Hercules (`HCL`) encaminham **todas** as tarefas da sua chave ao Mestre; o Gerente do App não encaminha, só recebe do Mestre. O Mestre classifica, mostra a classificação e o motivo ao Kariston e, na dúvida, pergunta. Só depois da validação a tarefa vai ao time. Detalhes em `shared/workflow.md`.

## Composição dos times

Todo time tem `<Time> · Gerente` e `<Time> · Dev`. Os demais dependem da configuração do arquivo do projeto.

**Designer** (seção **Design**, `designer: sim | não`, `figma: <link | não há | não informado>`):

- `designer: sim` → é criado o bot `<Time> · Designer`. Depois da validação do Kariston, tarefas com impacto visual/UI passam por ele antes do Dev. Ele lê o Figma (quando existe) ou analisa o padrão do tema e entrega as **"Diretrizes de design"** ao Mestre. No time App, o foco é a UI do admin do app (Shopify Polaris / App Home) e das extensões.
- `designer: não` → não é criado Designer; o Dev segue o padrão do tema.

**Revisor** (seção **Revisão**):

- `revisor: bot` → é criado o bot `<Time> · Revisor`, que revisa os PRs do Dev.
- `revisor: github` → **não** é criado bot Revisor. O Dev solicita a revisão no PR ao usuário do GitHub indicado em `revisor_github` e avisa o Mestre.

A mesma seção define **quem faz o deploy** (`deploy`).

## Arquivo de arquitetura por projeto

Cada projeto tem `projects/<slug>.arquitetura.md`: visão geral, stack, integrações, apps/extensões, dados, módulos principais, decisões, armadilhas e histórico. O Mestre e o Especialista Shopify leem antes de propor solução, o Designer antes de propor diretrizes e o Dev antes de implementar. O Dev atualiza no mesmo ciclo do PR quando a mudança afetar a arquitetura, e o Revisor confere.

Em 2026-11-10 o Kariston escolheu este arquivo **em vez de um bot Arquiteto**. O bot pode ser reavaliado se os arquivos ficarem grandes demais ou se as soluções continuarem errando.

## Como a instrução de um bot é composta

A instrução final de cada bot é a concatenação, nesta ordem:

1. `shared/workflow.md`
2. `shared/idioma-e-tom.md`
3. `shared/agentes-compartilhados.md`
4. `roles/<papel>.md` (gerente, dev, designer ou revisor; o designer só existe quando `designer: sim` e o revisor só quando `revisor: bot`)
5. `projects/<projeto>.md`

O arquivo `projects/<projeto>.arquitetura.md` **não** é concatenado na instrução (para não crescer demais): os bots o leem sob demanda, como indicado no fluxo.

Em caso de conflito, vale o mais específico: o arquivo do projeto prevalece sobre o papel, e o papel prevalece sobre o `shared/`. As regras de segurança (sem merge, sem deploy sem pedido, sem credenciais) **nunca** são sobrescritas.

## Sincronização

O repositório é mantido **sincronizado** com os bots:

1. O Kariston (ou um bot, via PR) altera os arquivos e faz o merge na `main`.
2. O Kariston avisa o Mestre (ou uma rotina do Mestre confere a `main`).
3. O Mestre recalcula a instrução de cada bot afetado:
   - mudou `shared/*` → todos os bots;
   - mudou `roles/<papel>.md` → todos os bots daquele papel;
   - mudou `projects/<projeto>.md` → os bots daquele time (se a seção **Revisão** mudar de `bot` para `github`, o Mestre desativa o Revisor do time; de `github` para `bot`, cria o Revisor).
4. O Mestre atualiza os bots e registra no `registry.json` o commit aplicado.

Só o conteúdo da `main` vale. Branches e PRs abertos não são aplicados.

## Projeto novo (onboarding)

1. Copiar `templates/project.md` para `projects/<tipo>-<cliente>.md` e preencher, incluindo a seção **Revisão** (`revisor: bot | github`, `revisor_github`, `deploy`) e a seção **Design** (`designer: sim | não`, `figma`).
2. Criar `projects/<tipo>-<cliente>.arquitetura.md` a partir de `templates/arquitetura.md`, com o que já se sabe do repositório (o resto como `não informado`).
3. Adicionar a entrada do projeto no `registry.json` (incluindo `architecture`) com os ids em `null` e os blocos `review` e `design` iguais ao do arquivo do projeto. Com `revisor: github`, o campo `bots.revisor` fica ausente; com `designer: não`, o campo `bots.designer` fica ausente.
4. Abrir PR. Depois do merge, o Mestre cria os bots do time com a instrução composta (Gerente e Dev sempre; Designer só com `designer: sim`; Revisor só com `revisor: bot`), preenche os ids no `registry.json` e faz um teste rápido de ponta a ponta (Gerente lê o Jira, Dev localiza o repositório, Revisor acessa o PR ou o Dev confirma que consegue pedir review ao usuário do GitHub).

## Regras que valem para todos

- Merge é **sempre manual**, feito pelo Kariston.
- Deploy só por quem a seção **Revisão** do projeto indicar, e só quando o Kariston pedir. Bots nunca fazem deploy por conta própria.
- **Nunca** guardar senhas, tokens, senhas de preview ou outras credenciais neste repositório.
