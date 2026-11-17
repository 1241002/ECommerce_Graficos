# Dashboard Marketplace — trabalho prático 1 ANDEC / PROPL (ISEP × Deloitte, 2026/27)

Aplicação web com dashboard interativo sobre o desempenho logístico de um marketplace
(dataset de e-commerce brasileiro, 2016–2018), para fundamentar uma prioridade de intervenção.
Escrever sempre em português de Portugal. Enunciado em `01_enunciados/`; estado e tarefas em `PLANO.md`.

## Stack (imposta pelo enunciado)
- Frontend Next.js · Backend NestJS · PostgreSQL. Versões e ambiente: ainda por comunicar.
- Gráficos, componentes, ORM e organização do código: escolha do grupo (registar em ADR).

## Design (obrigatório em todo o UI) — ver `docs/design.md`
- Animações < 300 ms, sempre com easing (nunca `linear`); quanto mais usado, menos anima. Resposta < 400 ms.
- Paletas e gradientes em OKLCH (`in oklch`); bordas com alfa; raio interior = exterior − padding; `100dvh`.
- Fontes proibidas: Geist, Space Grotesk, Bricolage Grotesque, Instrument Sans, JetBrains Mono, Space Mono.
- Antes de dar um ecrã por terminado: `/unslop` (plugin `unslop@heydamir`).

## Regras do enunciado que não se podem quebrar
- ETL reprodutível dos CSV para PostgreSQL; os CSV originais (`data/raw/`) nunca são alterados.
- O frontend só acede a dados pela API do backend. Indicadores e filtros calculados no servidor/BD.
- Testes automatizados para os 5 indicadores mínimos (nível de serviço, lead time, prazo de expedição,
  custo logístico relativo, ABC por receita por categoria).
- Credenciais e configuração em variáveis de ambiente (`.env`, nunca no git; `.env.example` sim).
- README com instruções para correr localmente.
- Spec-driven: especificação escrita **antes** do código, guardada no repositório, a orientar os agentes.
  Validar cálculos e interações de forma independente (ex.: recalcular em SQL/pandas).
- Não inventar dados em falta: documentar limitações.

## Workflow (Matt Pocock skills, plugin `mattpocock-skills`)
`/grill-with-docs` → `/to-spec` → `/to-tickets` → `/implement` (TDD por ticket) → `/code-review` → verificação humana.
Bugs: `/diagnosing-bugs` → teste de regressão. Antes de usar pela 1.ª vez: `/setup-matt-pocock-skills`.
- Vocabulário do domínio em `GLOSSARY.md`; decisões em `docs/adr/` (criados pelas skills quando surgem).
- Especificações em `docs/specs/`. Passagem de turno em `PLANO.md` (feito / próximo / decisões).

## Dados (`data/raw/`, ~126 MB, fora do git; o original está no zip em `01_enunciados/`)
- `dataset.csv` = encomendas (orders): timestamps de compra, aprovação, entrega à transportadora,
  entrega ao cliente e data estimada. `items_dataset.csv` tem `price` e `freight_value` por item.
- Juntam-se por `order_id`, `product_id`, `seller_id`, `customer_id`; geolocalização por prefixo de CP.
- Armadilhas: aspas inconsistentes; `product_name_lenght`/`product_description_lenght` (gralha original);
  `product_category_name_translation.csv` tem BOM UTF-8; categorias em português (há tradução EN).

## Ficheiros
- `01_enunciados/`, `02_aulas/`, `data/raw/` e `_arquivo/` são só de leitura.
- Nova versão de um documento = novo ficheiro; a anterior vai para `_arquivo/`.
- Ler .pdf com `pymupdf` (`import pymupdf`; em Python com `-I`, usar `sys.stdout.reconfigure(encoding='utf-8')`).
- Resumo da masterclass: `notas/resumo_aula_ai_agents.md`.
- Registar cada uso relevante de IA em `REGISTO_IA.md` no momento em que acontece.

## Agent skills

### Issue tracker

Issues e especificações em GitHub Issues (github.com/1241002/ECommerce_Graficos), via `gh`; cada especificação tem também cópia em `docs/specs/`. See `docs/agents/issue-tracker.md`.

### Triage labels

As 5 etiquetas por defeito (needs-triage, needs-info, ready-for-agent, ready-for-human, wontfix). See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: `GLOSSARY.md` + `docs/adr/` na raiz. See `docs/agents/domain.md`.
