# H01 — Formulário Público (Front)

Descrição:
Criar o formulário público responsivo para que o solicitante possa preencher todos os campos necessários, enviar anexos (frente/verso do documento) e aceitar os termos.

Critérios de Aceite:

- Formulário coleta todos os campos obrigatórios e valida formatos (CPF/CNPJ, e‑mail, telefone).
- Calendário permite somente sábados e domingos.
- Uploads aceitam jpg/png/pdf até 5 MB por arquivo.
- Ao enviar, chama `POST /api/solicitacoes` e mostra confirmação com id.

Estimativa: 5d
Responsável: Dev 1
