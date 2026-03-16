# CONTEXTO DO PROJETO — Sistema de Agendamento de Eventos (Escola Municipal — Salvador)

## Visão Geral

Plataforma simples para solicitação e gestão de agendamentos do espaço físico de uma escola municipal em Salvador, destinada a festas e eventos.

- Portal Público (sem login): formulário para que qualquer pessoa solicite uso do espaço.
- Painel da Escola (login único): gestor visualiza todas as solicitações, aprova ou rejeita e gerencia o histórico.

Objetivo: permitir um fluxo claro, auditável e responsivo de solicitações, garantindo que apenas sábados e domingos sejam agendados, com bloqueio automático de datas em análise e liberação em caso de rejeição.

## Equipe e Propósito (TCC)

- Este projeto é o Trabalho de Conclusão de Curso (TCC) de uma equipe de 5 desenvolvedores estudantes.
- A equipe é composta por 5 devs estudantes responsáveis por projetar, implementar, documentar e validar o sistema.
- Meu papel (orquestrador) é fornecer especificações, planejamento, divisão de tarefas, critérios de aceite e revisão de segurança/LGPD; eu NÃO escrevo código nem gero snippets de implementação.

## Processo de Trabalho e Cerimônias

- Sprint cadence: sprints semanais iniciais (1 semana) até estabilizar para 2 semanas conforme ritmo da equipe.
- Cerimônias recomendadas: planejamento de sprint (kickoff), daily standup 15m, revisão/QA ao final da sprint, retrospectiva breve.
- Controle de versão: cada atividade/significativa deve ser desenvolvida em branch dedicada (ex.: `feature/h01-formulario`) e submetida via PR para revisão.
- Pull requests: título e descrição claros, vincular tarefas/IDs das sprints; reviewers: pelo menos 1 colega + orquestrador técnico (eu) para critérios e LGPD.
- Código e commits: mensagens curtas no imperativo; separar commits por propósito (ci/testes/docs).

## Como eu irei apoiar a equipe

- Forneço SPECS detalhadas, critérios de aceite e checklist de QA para cada task.
- Valido que as tasks contem todas as informações necessárias (arquitetura de alto nível, contratos, validações, requisitos não‑funcionais, critérios de aceite, e passos de QA) sem gerar código.
- Auxilio na priorização e divisão de trabalho entre os 5 estudantes; reviso requisitos de segurança e LGPD antes do aceite de cada história.

## Tech Stack

- Backend: Spring Boot (REST APIs)
- Frontend: React (responsivo: desktop / tablet / mobile)
- Banco de dados: PostgreSQL
- Testes: JUnit (backend)
- Segurança: Spring Security + JWT (painel da escola)
- Armazenamento de arquivos sensíveis: bucket protegido (ex.: S3) ou filesystem com controle de acesso e URLs assinadas

## Principais Atores

- Solicitante: usuário público que preenche o formulário e envia a solicitação (sem autenticação).
- Gestor / Escola: usuário administrativo (conta única) que faz login no painel para aprovar/rejeitar solicitações.

## Requisitos Funcionais (resumido)

1. Solicitantes enviam pedidos de agendamento apenas para sábados e domingos.
2. Formulário público coleta: data, horário, nome do requerente, CPF/CNPJ, nome do responsável, endereço, bairro, e‑mail, telefone, público aproximado, descrição do evento, anexos (foto do documento frente e verso) e aceite dos termos legais.
3. Não é necessário login para o solicitante.
4. Ao criar uma solicitação a data fica "bloqueada temporariamente" (status PENDING) para evitar duplicidade; somente um evento por data.
5. Painel da escola (autenticado) lista solicitações por status (pendentes, aprovadas, rejeitadas) e permite aprovar ou rejeitar.
6. Aprovação transforma o bloqueio em definitivo (status APPROVED); rejeição libera a data (status REJECTED).
7. Ao aprovar ou rejeitar, o sistema envia e‑mail ao solicitante e à escola com os dados: nome do requerente, nome do responsável, CPF/CNPJ e data do evento.
8. Após a data do evento passar, os registros do agendamento e arquivos associados são excluídos do banco/armazenamento.
9. Painel de escola permite alteração de e‑mail e senha após primeiro acesso (recuperação de senha via e‑mail a confirmar).

## Formulário Público — Campos

- Data do evento (apenas sábados e domingos)
- Horário: hora início e hora fim
- Nome do Requerente
- CPF ou CNPJ (validar formato)
- Nome do Responsável
- Endereço residencial
- Bairro
- E‑mail
- Telefone
- Público aproximado (número)
- Descrição do evento
- Anexos: foto do documento (frente e verso) — tipos permitidos: jpg, png, pdf; tamanho máximo sugerido: 5 MB por arquivo
- Checkbox obrigatório: aceite dos termos (texto legal completo exibido em popup/modal)

### Termos (texto que o solicitante deve aceitar)

DECLARO:

A) Que utilizarei o espaço da escola exclusivamente para os fins acima expostos e desde já me responsabilizo por quaisquer danos que vierem a ser causados ao Patrimônio Público, em decorrência de ação ou omissão minha ou de pessoa sob minha responsabilidade;

B) Que a limpeza e conservação, do equipamento público é de minha inteira responsabilidade;

C) Salvador, Ter plena ciência do nível máximo de ruído (som) permitido para a área pleiteada de acordo com a Lei do município;

D) Ter ciência que é proibido qualquer propaganda político eleitoral nas áreas da escola;

E) Ter ciência que é proibido a utilização de bebidas alcoólicas, substâncias tóxicas ou a exploração de jogo de azar nas dependências da escola;

F) Ter ciência que é proibido a cobrança de ingressos ou qualquer tipo de remuneração financeira para adentrar e utilizar o espaço da escola;

G) Ter ciência que é proibida a entrada não autorizada em outras dependências da escola que não sejam as especificadas;

H) Ter ciência que todo e qualquer JOGO será CANCELADO, caso ocorra a necessidade de um evento com número maior de pessoas no mesmo dia e horário agendado;

I) Ter ciência que haverá no máximo um evento agendado por mês no mesmo dia e horário da semana.

O solicitante deve marcar "Li e concordo" antes de enviar a solicitação. Após o envio, exibir confirmação informando que, se aprovada ou rejeitada, o solicitante receberá um e‑mail com a decisão.

## Regras de Negócio (detalhadas)

- Dias Permitidos: somente SÁBADOS e DOMINGOS.
- Bloqueio de Datas:
  - Solicitação criada → status `PENDING` (bloqueio temporário).
  - Escola aprova → status `APPROVED` (bloqueio definitivo).
  - Escola rejeita → status `REJECTED` (data liberada).
- Exclusividade: um único evento por data (não por horário dentro do dia).
- Exclusão: registros e arquivos relacionados a eventos passados devem ser removidos do sistema (processo automático via job ou job manual conforme operação).

## Modelo de Dados (resumo)

- `reservas`
  - id (UUID)
  - data_evento (date)
  - hora_inicio (time)
  - hora_fim (time)
  - status (ENUM: PENDING, APPROVED, REJECTED)
  - lock_timestamp (timestamp)
  - requerente_nome
  - cpf_cnpj
  - responsavel_nome
  - endereco
  - bairro
  - email
  - telefone
  - publico_estimado (int)
  - descricao (text)
  - doc_frente_path
  - doc_verso_path
  - consent_timestamp
  - created_at, updated_at
  - approved_by, approved_at

- `escola_user`
  - id
  - email
  - password_hash
  - last_password_change
  - created_at

- `audit_logs`
  - id
  - entity
  - entity_id
  - action (CREATE, UPDATE, APPROVE, REJECT, DELETE)
  - actor (PUBLIC or ESCOLA or user id)
  - details (prefer usar ids e motivos; evitar PII)
  - timestamp

Observação LGPD: armazenar o mínimo necessário; logs de auditoria devem evitar PII; arquivos sensíveis devem ser protegidos e removidos quando não mais necessários.

## API — Endpoints Principais (REST / JSON)

Público (sem auth):

- POST /api/solicitacoes
  - cria solicitação + upload de arquivos
  - validações: data seja sábado/domingo; CPF/CNPJ; ausência de reserva PENDING/APPROVED na mesma data
  - resposta: 201 { id, message }
- GET /api/solicitacoes/{id}
  - retorna confirmação básica (sem exibir arquivos completos; usar link temporário autenticado quando necessário)

Painel da Escola (JWT):

- POST /api/login
  - { email, password } → JWT
- GET /api/reservas?status=pending|approved|rejected|all
  - lista reservas com paginação
- GET /api/reservas/{id}
  - detalhes completos + links temporários para os anexos
- PUT /api/reservas/{id}/aprovar
  - marca `APPROVED`, grava `approved_by`/`approved_at`, envia e‑mail
- PUT /api/reservas/{id}/rejeitar
  - marca `REJECTED`, envia e‑mail
- DELETE /api/reservas/{id}
  - somente admin (remoção manual se necessário)

Responses devem seguir convenções HTTP e retornar mensagens de erro claras para validações falhas.

## Bloqueio e Concorrência

- Ao criar solicitação, sistema verifica se existe `reservas` com mesma `data_evento` e status `PENDING` ou `APPROVED`. Se existir, recusar criação.
- Criação grava `PENDING` e torna a data indisponível.
- Aprovação converte para `APPROVED`.
- Rejeição converte para `REJECTED` e libera a data.
- Decisão sobre liberação automática de `PENDING` (ex.: após 24 horas) deve ser confirmada — por padrão, manter `PENDING` até ação manual da escola.

## Notificações por E‑mail

- Ao aprovar ou rejeitar, enviar e‑mail para solicitante e para o e‑mail da escola com os campos: nome do requerente, nome do responsável, CPF/CNPJ e data do evento.
- Templates: solicitação recebida (opcional), aprovado, rejeitado.
- Envio asíncrono (fila) para evitar travamento do request.

## Segurança e LGPD

- Consentimento explícito gravado com `consent_timestamp`.
- TLS obrigatório (HTTPS).
- Armazenamento de anexos com criptografia em repouso (S3 SSE ou disco criptografado).
- Acesso a anexos via URLs assinadas expiradas; somente painel autenticado pode gerar/baixar links.
- Senhas com hashing seguro (bcrypt/argon2).
- Logs de auditoria com identificadores, sem PII.
- Procedimento para exclusão de dados por solicitação: como solicitantes não fazem login, definir fluxo de atendimento via e‑mail para requisição de remoção.

## UX / Frontend (visão)

- Formulário público responsivo, preferencialmente em passos:
  1. Seleção de data (calendário que habilita apenas sábados/domingos)
  2. Horário
  3. Dados pessoais e contato
  4. Upload de documentos (frente/verso)
  5. Apresentação dos termos + checkbox de aceite
  6. Enviar → confirmação com número da solicitação e mensagem informativa sobre e‑mail de decisão
- Painel da escola: lista filtrável (pendentes/aprovados/rejeitados), visualização detalhada com anexos e ações rápidas (aprovar/rejeitar).

## Critérios de Aceite (MVP)

1. Formulário público aceita e valida todos os campos obrigatórios; arquivos aceitos e armazenados com segurança.
2. Calendário permite somente sábados e domingos.
3. Criação de solicitação marca a data como indisponível enquanto `PENDING` ou `APPROVED`.
4. Escola faz login e visualiza solicitações pendentes; consegue aprovar ou rejeitar.
5. Aprovação/rejeição disparam e‑mails com as informações requeridas.
6. Arquivos de identidade acessíveis apenas via painel autenticado (links temporários).
7. Job/rotina remove registros e arquivos após a data do evento.
8. Auditoria registra criação, aprovação, rejeição e exclusão (sem PII).

## Operação e Manutenção

- Ambientes sugeridos: dev / staging / prod
- Job agendado para exclusão de eventos passados e arquivos associados
- Backups regulares do banco de dados
- Monitoramento básico (logs, métricas, fila de e‑mail)

## Pendências / Decisões a confirmar

1. Liberação automática de `PENDING` após X horas? (sugestão: manter manual; se preferir, adotar 24h)
2. Política legal de retenção: você solicitou exclusão após o evento — confirmar se há obrigação legal para manter registros por período (ex.: 6 meses)
3. Política de recuperação de senha para o login único da escola (recuperação via e‑mail?)
4. Tamanho máximo de anexo e tipos aceitos (sugestão: 5 MB; jpg/png/pdf)

## Próximos Passos Recomendados

1. Confirmar pendências apontadas acima.
2. Gerar SPEC detalhada para `POST /api/solicitacoes` (validações, DTOs, mensagens de erro, fluxos de upload).
3. Criar backlog priorizado e planejar sprint inicial (2 semanas) com divisão de tarefas entre desenvolvedores.
4. Implementar job de exclusão automática e configurar armazenamento seguro para anexos.

---

Arquivo criado: `CONTEXT.md`
