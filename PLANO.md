# Plano

## Onde ficámos
- 17/11: masterclass e enunciado estudados (resumo em `notas/resumo_aula_ai_agents.md`); skills do Matt Pocock
  instaladas (plugin `mattpocock-skills`); estrutura do projeto criada; repositório git iniciado.
- 17/11: `/setup-matt-pocock-skills` feito: tickets em GitHub Issues (github.com/1241002/ECommerce_Graficos),
  especificações também em `docs/specs/`, etiquetas por defeito, single-context. `gh` 2.104 instalado.
- 17/11: `gh` autenticado (1241002); etiquetas de triagem criadas no repo.
- **Próximo passo:** commit inicial + push; depois `/grill-with-docs` sobre o enunciado.

## Decisões por tomar (o enunciado deixa ao grupo)
- Utilizador principal do dashboard e ≥ 3 perguntas de negócio.
- Indicadores adicionais aos mínimos (e porquê).
- Segmentos a comparar (categoria, estado/região, vendedor, período, ...) e critérios de prioridade.
- Organização visual: página principal + até 3 subpáginas; onde ficam tooltip, drill-down e drill-through.
- Regras de cálculo: que encomendas contam (só `delivered`?), datas nulas, ABC (cortes 80/15/5?), frete por encomenda vs. item.
- Bibliotecas: gráficos, componentes de UI, ORM, framework de testes. Onde fica o repositório (GitHub?).

## Requisitos (checklist do enunciado)
- [ ] ETL reprodutível CSV → PostgreSQL
- [ ] API NestJS; frontend só consome a API
- [ ] 5 indicadores mínimos + adicionais, calculados no servidor
- [ ] Filtros dinâmicos (produto, período, ...) consistentes em toda a página
- [ ] Comparação ao longo do tempo
- [ ] Tooltip, drill-down e drill-through (≥ 1 de cada)
- [ ] Página principal + até 3 subpáginas com navegação
- [ ] Testes automatizados dos indicadores mínimos
- [ ] Configuração em variáveis de ambiente
- [ ] README com instruções de execução local
- [ ] Especificações no repositório, escritas antes do código
- [ ] Justificação de critérios, ABC, tratamento de dados e limitações
