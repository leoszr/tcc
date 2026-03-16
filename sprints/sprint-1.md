# Sprint 1 — Inicial (start-from-zero, 1 semana)

Objetivo: iniciar o projeto do zero e entregar um fluxo mínimo utilizável que permita validar a jornada do solicitante: desde o formulário público até a persistência inicial no banco. A prioridade é criar a base do repositório, ambiente de desenvolvimento, contrato do endpoint e uma interface simples que permita enviar solicitações.

Escopo reduzido e justificado:

- Trabalhar a partir do repositório: estrutura inicial, README e scripts para rodar localmente.
- Implementar backend mínimo com o endpoint de criação de solicitação (sem uploads, sem painel e sem envio de e‑mail).
- Implementar frontend mínimo (React) com formulário que chame o endpoint e mostre confirmação.
- Incluir testes e documentação mínima para que a equipe entenda onde continuar.

Entregáveis desta sprint (detalhados):

1. Repositório inicial

- README com objetivos do projeto, instruções para rodar localmente, convenções de branch, e checklist de revisão de PR.
- Estrutura de pastas sugerida para backend/frontend/docs.
- Arquivo de exemplo com variáveis de ambiente necessárias para desenvolvimento local.

2. Backend mínimo

- Endpoint para receber solicitação pública (contrato documentado em docs).
- Validações server-side: data do evento deve ser sábado ou domingo; CPF/CNPJ com validação básica; campos obrigatórios presentes.
- Persistência mínima: tabela `reservas` com colunas essenciais (id, data_evento, hora_inicio, hora_fim, nome_requerente, cpf_cnpj, email, status, created_at).
- Resposta consistente: incluir identificador da reserva e mensagem de confirmação.

3. Frontend mínimo

- Página única (single page) com formulário que contém os campos essenciais e validações client-side equivalentes às do backend.
- Calendário ou seletor de data que indica claramente que apenas sábados e domingos são permitidos.
- Fluxo de envio e tela de confirmação com o id retornado.

4. Testes e documentação

- Testes unitários para validadores críticos (dia da semana, CPF/CNPJ) e testes de integração básicos que verificam o fluxo de criação.
- Documento em docs/ descrevendo o contrato do endpoint (campos, formatos, mensagens de erro) e instruções de QA.

Tempo previsto: 1 semana. Se a equipe for iniciante, separar tarefas por dia e revisar impedimentos diariamente.

Backlog desta sprint (tarefas atômicas, priorizadas):

- H01.1 — Inicializar repositório Spring Boot (esqueleto, dependências mínimas)
- H01.2 — Configurar variáveis de ambiente e conexão com Postgres (`.env.example`)
- H01.3 — Criar migration inicial / DDL (baseline)
- H02.1 — Criar model `Reserva` (fields, constraints, documentação do DDL)
- H02.2 — Criar repository `ReservaRepository` (interface com método `findByDataEvento`)
- H02.3 — Implementar service: validar dia (sábado/domingo)
- H02.4 — Implementar service: checar conflito por data (PENDING/APPROVED)
- H02.5 — Criar controller `ReservaController` com endpoint POST `/api/solicitacoes` (contrato documentado)
- H09.1 — Testes unitários dos validadores (dia da semana, CPF/CNPJ)
- H09.2 — Teste de integração mínimo: POST cria reserva e persiste
- H10.1 — README e instruções de desenvolvimento local (setup JDK, Postgres, Node)
- H10.2 — Scripts de execução local (scripts para iniciar backend e frontend em dev)

Dependências e pontos de atenção

- Equipe começa do zero: reservar tempo na sprint para configurar IDEs, Java JDK, Node.js, e ferramentas de banco (Postgres) — documentar em README.
- Garantir que as validações sejam consistentes entre frontend e backend (mesma regra para sábado/domingo, CPF/CNPJ).
- Estabelecer convenções de commit e PR desde o início para não perder tempo depois.

Critérios de aceite (resumidos)

- O projeto inicia com README e instruções para rodar localmente.
- É possível enviar uma solicitação via UI e ver o registro persistido no banco com status PENDING.
- Validadores críticos passam nos testes automatizados.
