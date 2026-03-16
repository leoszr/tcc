# Sprint 1 — MVP Inicial (2 semanas)

Objetivo: entregar o MVP mínimo para permitir envio público de solicitações com anexos e aceite dos termos, painel único da escola para aprovar/rejeitar, bloqueio temporário de datas, envio de e‑mails e job de exclusão de eventos passados.

Decisões adotadas:

- PENDING permanece até ação manual da escola (sem liberação automática).
- Exclusão automática de eventos e arquivos após a data do evento (job agendado).
- Recuperação de senha via e‑mail (implementar nas sprints seguintes se necessário).
- Anexos: jpg/png/pdf até 5 MB.
- Envio de e‑mail assíncrono (fila simples).

Entregáveis:

- Formulário público responsivo com validações e upload de documentos.
- Endpoint `POST /api/solicitacoes` com validações e persistência (status PENDING).
- Armazenamento seguro de anexos com links temporários.
- Painel da escola com JWT (login único), listagem e detalhe de reservas.
- Endpoints de aprovar/rejeitar e envio de e‑mail.
- Job para exclusão de eventos passados.
- Testes unitários/integrados básicos e documentação mínima (OpenAPI/Postman).

Backlog (priorizado): H01..H10 (cada task dentro de `tasks/`)
