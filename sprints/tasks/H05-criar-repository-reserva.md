# H05 — Criar repository `ReservaRepository`

Objetivo:
Definir a interface do repositório para `Reserva`, incluindo métodos essenciais que serão usados no serviço.

Entradas / Saídas:

- Entrada: definição do model `Reserva` (H04)
- Saída: documento com assinatura dos métodos do repository e exemplos de uso (sem código). Métodos mínimos: `save(reserva)`, `findById(id)`, `findByDataEvento(date)`.

Critérios de Aceite:

- Documento `docs/repositories/reserva_repository.md` com as assinaturas e comportamento esperado de cada método.
- Testes futuros poderão mockar esse contrato.

Dependências:

- H04 (model Reserva)

Estimativa: 0.25d (2 horas)

Checklist de QA:

- Validar que as assinaturas cobririam os casos de uso (criação, consulta por data, busca por id).
