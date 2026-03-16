# H02 — Configurar variáveis de ambiente e conexão com Postgres

Objetivo:
Fornecer arquivo de exemplo `.env.example` e documentar as variáveis de ambiente necessárias para conectar o backend a uma instância PostgreSQL em ambiente local.

Entradas / Saídas:

- Entrada: nenhuma
- Saída: arquivo `.env.example` no repositório com chaves: `SPRING_DATASOURCE_URL`, `SPRING_DATASOURCE_USERNAME`, `SPRING_DATASOURCE_PASSWORD`, `SPRING_PROFILES_ACTIVE` e instruções no README.

Critérios de Aceite:

- `.env.example` presente no repositório com variáveis necessárias e valores de exemplo.
- README atualizado com instruções para criar um container Postgres via Docker Compose e como preencher `.env` local.

Dependências:

- H01 (esqueleto do backend) deve estar criado.

Estimativa: 0.25d (2 horas)

Checklist de QA:

- Verificar que preenchendo `.env` com dados de uma instância Postgres local a aplicação consegue iniciar e conectar.
