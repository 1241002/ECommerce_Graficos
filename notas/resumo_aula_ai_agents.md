# Resumo — "Building Software with AI Agents" (ISEP × Deloitte, 17/11/2026)

Fonte: `02_aulas/ISEP_Building_Software_with_AI_Agents.pdf` (41 slides). Ideia central:
**a IA multiplica a disciplina que trouxeres — boa ou má.**

## 1. Fundamentos de LLM
- O modelo prevê o próximo token, em ciclo. Não há base de factos nem plano guardado.
- **Janela de contexto = a secretária**: só sabe o que está lá; esquece ao fechar a sessão; desarrumação piora respostas.
- Tokens ≈ 4 caracteres; tudo é pago e limitado em tokens. Embeddings: significado = geometria.
- **Temperatura**: não-determinismo é inerente → **a verificação tem de ser determinística**.
- Modelos de raciocínio: esforço alto para planear/depurar, baixo para edições de rotina.
- *Lost in the middle* / *context rot*: um contexto focado de 20k vence um ruidoso de 200k. Sessões novas por tarefa.
- **Prompt injection**: conteúdo externo é informação, não instruções.
- Para o modelo "saber das nossas coisas": treinar < fine-tune < **dar contexto (RAG)** — o que os agentes fazem.

## 2. Anatomia de um agente (Agente = Modelo + Harness)
Os 10 blocos comuns a Claude Code, Codex, Copilot e Cursor:
1. **Loop** — olhar → pensar → agir → verificar, até acabar.
2. **Tools** — Read, Edit/Write, Bash, Grep/Glob, WebFetch, Task.
3. **Permissões** — "avança / pergunta / nunca" (`.claude/settings.json`: allow/deny). Shift+Tab → plan mode.
4. **Contexto** — `/context`, `/compact` (dizer o que manter).
5. **Instruções** — `CLAUDE.md` lido em todas as sessões: comandos, regras, armadilhas. Curto. Repetiu um erro? +1 linha.
6. **Skills** — "livros de receitas": só nome+descrição ficam no contexto; o `SKILL.md` abre quando a tarefa pede.
7. **MCP** — ligação a sistemas externos (GitHub, BD, browser, Jira). Poucos e de confiança.
8. **Hooks** — o que tem de acontecer sempre (formatar, lint, testes após cada edição).
9. **Sub-agentes**.
10. **Memória** — passagem de turno: `CLAUDE.md` + `progress.md` (feito / próximo / decisões) + git log.

Hábitos: `/clear` entre tarefas, `/compact`, Esc Esc para voltar atrás, plan mode antes de editar.
Tokenomics: o contexto todo é reenviado a cada volta → sessões longas custam mais em dinheiro e qualidade;
caching (não mexer no prefixo estável), modelo certo para cada tarefa, inputs magros (grep antes de ler), módulos profundos.

## 3. Spec-driven development
- *Vibe coding* (prompt → esperança) só para protótipos descartáveis. O que vive precisa de spec.
- **Workflow do Matt Pocock** (github.com/mattpocock/skills — instalado como plugin `mattpocock-skills`):

  | Fase | Skill | Quem lidera |
  |---|---|---|
  | Alinhar o quê | `/grill-with-docs` — uma pergunta de cada vez, com resposta recomendada; atualiza `GLOSSARY.md` e ADRs | Humano |
  | Escrever | `/to-spec` | Humano |
  | Fatiar | `/to-tickets` — fatias verticais (BD + API + UI + testes), cada uma demonstrável | Humano |
  | Implementar | `/implement` (TDD por ticket) | Agente |
  | Rever | `/code-review` (olhos frescos) | Agente |
  | Verificar | humano decide | Humano |

  Bugs: `/triage` → novo ticket → `/diagnosing-bugs` → teste de regressão.
  Periódico: `/improve-codebase-architecture`.
- **Guardrails determinísticos**: formatter, linter, type checker, testes, SonarQube, scans de segurança, mutation testing.
  "Tudo o que se pode verificar com uma ferramenta sai do prompt e vai para o pipeline."
- **Shift left**: hook do agente (segundos) → pre-commit (segundos) → CI (minutos).
- **Módulos profundos** (Ousterhout): interface simples sobre muita funcionalidade. Com agentes ainda importa mais:
  o agente lê 1 interface em vez de 9 ficheiros (ex.: módulos Pricing / Checkout / Inventory).

## 4. Exercício
Equipas de 4 (~44 alunos). Enunciado: `01_enunciados/Enunciado_01_E_Commerce.pdf` (ver `CLAUDE.md` e `PLANO.md`).
Recursos: github.com/mattpocock/skills · *A Philosophy of Software Design* (J. Ousterhout) · docs do Claude Code/Codex.
