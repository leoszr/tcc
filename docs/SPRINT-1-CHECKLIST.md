# SPRINT 1 — Checklist de Aceitação (Start-from-zero)

Uso: este documento agrega os checklists de QA e critérios de aceite para cada task atômica H01..H12. O revisor usa esta lista para validar implementação antes de aceitar a task/PR.

Como marcar conclusão: atualizar `sprints/progress.md` e o arquivo de task correspondente mudando `status` para `in_progress` e depois `completed`.

Resumo rápido das tasks

- H01 — Inicializar backend Spring
- H02 — Configurar env / Postgres
- H03 — Migration baseline
- H04 — Model Reserva
- H05 — Repository Reserva
- H06 — Service validar dia
- H07 — Service checar conflito
- H08 — Controller POST /api/solicitacoes
- H09 — Testes unitários (validadores)
- H10 — Teste de integração POST create
- H11 — README / setup dev
- H12 — Scripts dev / docker-compose

Checklist detalhado por task

- H01 — Inicializar backend Spring
  - [ ] Projeto Spring Boot presente com `pom.xml`/`build.gradle` contendo dependências listadas.
  - [ ] Classe principal da aplicação (bootstrap) e profile `dev` configurado.
  - [ ] Iniciar a aplicação localmente com as instruções do README; health endpoint responde.

- H02 — Configurar variáveis de ambiente e conexão com Postgres
  - [ ] Arquivo `.env.example` presente com `SPRING_DATASOURCE_URL`, `SPRING_DATASOURCE_USERNAME`, `SPRING_DATASOURCE_PASSWORD`, `SPRING_PROFILES_ACTIVE`.
  - [ ] README descreve como criar/rodar Postgres local (Docker Compose) e preencher `.env`.
  - [ ] Ao preencher `.env` e iniciar a aplicação, a conexão com o banco é estabelecida (sem erro de conexão).

- H03 — Criar migration inicial / DDL (baseline)
  - [ ] Arquivo de migration (Flyway/Liquibase) criado no repositório.
  - [ ] Aplicar migration em ambiente dev cria a tabela `reservas` com colunas esperadas.
  - [ ] Verificar tipos e constraints correspondem ao documento do model.

- H04 — Criar model `Reserva`
  - [ ] Documento `docs/models/reserva.md` com campos, tipos e constraints está presente.
  - [ ] Definições batem com a migration aplicada (nomes e tipos das colunas).

- H05 — Criar repository `ReservaRepository`
  - [ ] Documento `docs/repositories/reserva_repository.md` com assinaturas esperadas (`save`, `findById`, `findByDataEvento`).
  - [ ] Revisar se as assinaturas suportam os casos de uso previstos (persistir, buscar por data).

- H06 — Service: validar dia
  - [ ] Documento de regras `docs/services/validar_dia.md` com exemplos de entradas/saídas.
  - [ ] Comportamento esperado: sábado/domingo → ok; outro dia → erro com `code: INVALID_DAY`.
  - [ ] Testes unitários (H09) cobrem os cenários básicos.

- H07 — Service: checar conflito por data
  - [ ] Documento `docs/services/checar_conflito.md` descrevendo a lógica e mensagens de erro (`DATE_CONFLICT`).
  - [ ] Cenário de verificação: criar reserva PENDING e tentar criar outra para mesma data retorna 409.

- H08 — Controller POST /api/solicitacoes
  - [ ] Documento `docs/api/post_solicitacoes.md` com contrato (payload, respostas, erros).
  - [ ] Com payload válido, retorna 201 com `{ id, message }` e grava `status = PENDING`.
  - [ ] Erros coerentes: 400 para payload/validation, 409 para conflito.

- H09 — Testes unitários: validadores
  - [ ] Suíte de testes unitários inclui casos para validar dia e CPF/CNPJ.
  - [ ] Execução local dos testes passa (CI deverá executar também).

- H10 — Teste de integração: POST create
  - [ ] Teste de integração faz POST válido e verifica persistência em DB (status PENDING).
  - [ ] Teste roda com DB de teste (in-memory ou container Postgres) e passa.

- H11 — README e instruções de desenvolvimento
  - [ ] README explica como clonar, configurar `.env`, iniciar Postgres (docker-compose) e rodar backend/frontend.
  - [ ] Instruções de criação de branch e template de PR descritas.

- H12 — Scripts de execução local (dev)
  - [ ] `docker-compose.yml` mínimo para Postgres presente.
  - [ ] Scripts `start-backend` e `start-frontend` (ou scripts equivalentes) funcionam em ambiente dev.

Critérios de entrega da Sprint (para aceitar Sprint como completa)

- Todas as tasks H01..H12 marcadas `completed` em `sprints/progress.md`.
- Build do backend sobe e os testes unitários passam localmente.
- Teste de integração (H10) executa e passa.
- README e scripts permitem que um avaliador siga o fluxo de setup em uma máquina limpa.

Observações / notas para revisores

- Revisores devem checar consistência entre docs (models, repositories, api) e artefatos implementados.
- Não aceite tasks que escondam trabalho em outras branches ou que quebrem a build.
