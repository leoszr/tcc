# H08 — Controller: POST /api/solicitacoes (contrato)

Objetivo:
Definir o contrato do endpoint `POST /api/solicitacoes` que recebe a solicitação pública, valida os dados chamando os services apropriados e persiste a reserva com status `PENDING`.

Entradas / Saídas (payload):

- Requisição JSON (exemplo de campos):
  - `data_evento` (YYYY-MM-DD) — obrigatório
  - `hora_inicio` (HH:MM) — opcional
  - `hora_fim` (HH:MM) — opcional
  - `nome_requerente` — obrigatório
  - `cpf_cnpj` — obrigatório
  - `email` — obrigatório
  - `descricao` — opcional
- Resposta de sucesso: HTTP 201 `{ id: <uuid>, message: "Solicitação recebida" }`
- Erros possíveis:
  - 400 `{ code: "INVALID_DAY", message: "Datas permitidas: sábado ou domingo" }`
  - 400 `{ code: "INVALID_PAYLOAD", message: "Campo X é obrigatório" }`
  - 409 `{ code: "DATE_CONFLICT", message: "Já existe uma solicitação para esta data" }`

Critérios de Aceite:

- Documento `docs/api/post_solicitacoes.md` com contrato e exemplos.
- Ao enviar payload válido, o registro é persistido na tabela `reservas` com `status` = `PENDING` e `created_at` preenchido.

Dependências:

- H04..H07 (model, repo, services)

Estimativa: 1d

Checklist de QA:

- Testar envio de payloads válidos e inválidos e validar respostas conforme contrato.
