# Sprint 1 — Inicial (1 semana)

Objetivo: preparar o projeto e entregar a mínima evidencia de fluxo de solicitação pública sem complexidade operacional: repositório, backend mínimo com endpoint de criação de solicitação (sem upload de arquivos), validação de dia da semana (sábado/domingo), persistência dos campos essenciais e front‑end simples que permita enviar uma solicitação e ver uma confirmação.

Decisões adotadas (reduzidas para iniciar):

- Sem upload de anexos nesta sprint; anexos ficam para sprint seguinte.
- Sem autenticação nem painel da escola nesta sprint (painel será alvo da Sprint 2).
- PENDING permanece até ação manual (decisão futura sobre expiração automática).
- Anexos, e‑mail, job de exclusão e fila de e‑mail adiados para sprints posteriores.

Entregáveis mínimos desta sprint:

- Repositório inicial com README e scripts de execução (dev).
- Backend (Spring Boot) com endpoint `POST /api/solicitacoes` que valida e persiste: `data_evento`, `hora_inicio` (opcional), `nome_requerente`, `email`, `cpf_cnpj`, `status` = `PENDING`.
- Validação server-side: somente sábado ou domingo para `data_evento` e formato básico de CPF/CNPJ.
- Frontend (React) simples: formulário single‑page sem upload, validações client‑side e chamada ao `POST` para criar solicitação; mostra confirmação com id retornado.
- Testes unitários mínimos cobrindo validação de dia e criação.

Tempo previsto: 1 semana (ajustável)

Backlog desta sprint (priorizado, subset das tasks existentes):

- H01 — Formulário público (adaptado: sem upload)
- H02 — API criar solicitação (adaptado: sem upload, validações mínimas)
- H09 — Testes unitários e integração mínima (focar validações)
- H10 — Observability e configuração básica (README, envs de dev)

Itens adiados para Sprint 2 (fora do escopo atual): H03, H04, H05, H06, H07, H08 (storage, auth, painel, aprovar/rejeitar, e‑mail, job exclusão)

Notas:

- Esta sprint reduz a complexidade inicial para permitir que a equipe comece pelo essencial e valide o fluxo de solicitação pública.
- Após entrega desta sprint, programar Sprint 2 com upload de anexos, painel da escola e notificações.
