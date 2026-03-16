# H07 — Envio de e‑mail assíncrono (worker + templates)

Descrição:
Implementar fluxo de envio de e‑mail assíncrono (fila/worker) e templates para as notificações de aprovação/rejeição.

Critérios de Aceite:

- Mensagens geradas contêm: nome do requerente, nome do responsável, CPF/CNPJ e data do evento.
- Worker processa fila e envia e‑mails; retries básicos em falhas.

Estimativa: 2d
Responsável: Dev 4
