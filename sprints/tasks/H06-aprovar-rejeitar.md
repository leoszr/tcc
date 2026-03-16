# H06 — Aprovar / Rejeitar (API + UI)

Descrição:
Implementar endpoints e UI para que a escola aprove ou rejeite solicitações. As ações devem gravar `approved_by`/`approved_at` ou `rejected_at`, inserir entry em `audit_logs` e enfileirar e‑mail de notificação.

Critérios de Aceite:

- PUT /api/reservas/{id}/aprovar e /rejeitar alteram status corretamente.
- Geram entrada em `audit_logs` sem PII.
- Enfileiram envio de e‑mail com dados obrigatórios.

Estimativa: 2d
Responsável: Dev 2
