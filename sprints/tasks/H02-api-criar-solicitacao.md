# H02 — API criar solicitação `POST /api/solicitacoes`

Descrição:
Implementar o endpoint que recebe a solicitação, valida os dados (sábados/domingos, CPF/CNPJ, conflito de data), persiste o registro com status `PENDING` e retorna o id da solicitação.

Critérios de Aceite:

- Validações server-side para dia da semana, formato CPF/CNPJ, campos obrigatórios.
- Rejeitar criação se já existir `PENDING` ou `APPROVED` para a mesma `data_evento`.
- Retornar 201 com `{ id, message }` em caso de sucesso.

Estimativa: 4d
Responsável: Dev 2
