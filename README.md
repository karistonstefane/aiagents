# aiagents

Fonte da verdade das instruções dos bots da Checkstore usados pelo Kariston Stefane.

Cada projeto tem o **seu próprio time de bots** (Gerente, Dev e Revisor), com memória separada, para evitar mistura de contexto entre clientes. Alguns agentes são **compartilhados** por todos os times (Mestre, Especialista Shopify e Reportador de Horas).

## Estrutura

```
aiagents/
├── README.md                  # este arquivo
├── roles/                     # instrução base de cada papel (vale para todo projeto)
│   ├── gerente.md
│   ├── dev.md
│   └── revisor.md
├── shared/                    # regras comuns a todos os bots
│   ├── workflow.md            # fluxo de uma tarefa, do Jira ao merge
│   ├── idioma-e-tom.md        # idioma, tom, aprovações, comandos no PC
│   └── agentes-compartilhados.md  # Mestre, Especialista Shopify, Reportador
├── projects/                  # um arquivo por time/projeto
│   ├── tema-mueller.md
│   ├── tema-hercules.md
│   ├── app-mueller-hercules.md
│   ├── tema-made-in-guarda.md
│   ├── tema-nuora.md
│   └── tema-new-era.md
├── templates/
│   └── project.md             # modelo para projeto novo
└── registry.json              # mapa projeto → ids dos bots criados (mantido pelo Mestre)
```

## Times iniciais

| Time | Arquivo | Jira | Repositório |
|---|---|---|---|
| Tema - Mueller | `projects/tema-mueller.md` | MUEL | `checkstore/mueller` |
| Tema - Hercules | `projects/tema-hercules.md` | HCL | `checkstore/hercules` |
| App - Mueller e Hercules | `projects/app-mueller-hercules.md` | MUEL + HCL (tarefas de app) | `checkstore/app-b2b-connect` |
| Tema - Made in Guarda | `projects/tema-made-in-guarda.md` | GDA | `checkstore/made-in-guarda` |
| Tema - Nuora | `projects/tema-nuora.md` | NU | `checkstore/nuoracosmetic` |
| Tema - New Era | `projects/tema-new-era.md` | NE | A CONFIRMAR (`~/projects/newera`) |

Cada time tem três bots, nomeados `<Time> · Gerente`, `<Time> · Dev` e `<Time> · Revisor`.

## Como a instrução de um bot é composta

A instrução final de cada bot é a concatenação, nesta ordem:

1. `shared/workflow.md`
2. `shared/idioma-e-tom.md`
3. `shared/agentes-compartilhados.md`
4. `roles/<papel>.md` (gerente, dev ou revisor)
5. `projects/<projeto>.md`

Em caso de conflito, vale o mais específico: o arquivo do projeto prevalece sobre o papel, e o papel prevalece sobre o `shared/`. As regras de segurança (sem merge, sem deploy sem pedido, sem credenciais) **nunca** são sobrescritas.

## Sincronização

O repositório é mantido **sincronizado** com os bots:

1. O Kariston (ou um bot, via PR) altera os arquivos e faz o merge na `main`.
2. O Kariston avisa o Mestre (ou uma rotina do Mestre confere a `main`).
3. O Mestre recalcula a instrução de cada bot afetado:
   - mudou `shared/*` → todos os bots;
   - mudou `roles/<papel>.md` → todos os bots daquele papel;
   - mudou `projects/<projeto>.md` → os três bots daquele time.
4. O Mestre atualiza os bots e registra no `registry.json` o commit aplicado.

Só o conteúdo da `main` vale. Branches e PRs abertos não são aplicados.

## Projeto novo (onboarding)

1. Copiar `templates/project.md` para `projects/<tipo>-<cliente>.md` e preencher.
2. Adicionar a entrada do projeto no `registry.json` com os ids em `null`.
3. Abrir PR. Depois do merge, o Mestre cria os três bots do time com a instrução composta, preenche os ids no `registry.json` e faz um teste rápido de ponta a ponta (Gerente lê o Jira, Dev localiza o repositório, Revisor acessa o PR).

## Regras que valem para todos

- Merge é **sempre manual**, feito pelo Kariston.
- Deploy só quando o Kariston pedir.
- **Nunca** guardar senhas, tokens, senhas de preview ou outras credenciais neste repositório.
