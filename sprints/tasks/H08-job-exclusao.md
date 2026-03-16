# H08 — Job de exclusão de eventos passados

Descrição:
Implementar job agendado que remove registros de `reservas` cuja `data_evento` seja anterior ao dia atual e exclui arquivos associados; registra ação em `audit_logs`.

Critérios de Aceite:

- Job remove DB records e arquivos correspondentes.
- Gera entradas em `audit_logs` para cada remoção (sem PII).

Estimativa: 2d
Responsável: Dev 3
