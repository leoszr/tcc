# H04 — Criar model `Reserva` (fields e constraints)

Objetivo:
Definir a entidade/objeto `Reserva` com campos essenciais e documentar as constraints e tipos para implementação posterior.

Entradas / Saídas:

- Entrada: especificação de campos (ver CONTEXT.md)
- Saída: documento com a definição do model incluindo tipos de dados, restrições (not null, tamanho máximo), e mapeamento pro DB (colunas correspondentes).

Campos esperados (exemplo):

- id (UUID)
- data_evento (date) — not null
- hora_inicio (time) — nullable
- hora_fim (time) — nullable
- nome_requerente (varchar(255)) — not null
- cpf_cnpj (varchar(20)) — not null
- email (varchar(255)) — not null
- status (ENUM: PENDING, APPROVED, REJECTED) — default PENDING
- created_at (timestamp) — not null

Critérios de Aceite:

- Documento do model disponível em `docs/models/reserva.md` com tipos e constraints claros.
- As definições batem com a migration criada em H03.

Dependências:

- H03 (migration) ou, se a migration for criada após, alinhar os nomes/nomem de colunas.

Estimativa: 0.5d (4 horas)

Checklist de QA:

- Conferir `docs/models/reserva.md` e validar consistência com o schema do banco.
