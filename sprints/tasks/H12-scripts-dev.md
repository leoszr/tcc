# H12 — Scripts de execução local (dev)

Objetivo:
Adicionar scripts de conveniência para iniciar o backend e frontend em ambiente de desenvolvimento (por exemplo, `./scripts/start-backend.sh`, `./scripts/start-frontend.sh` ou entradas no `package.json`). Incluir também um `docker-compose.yml` mínimo para Postgres.

Entradas / Saídas:

- Entrada: nenhum
- Saída: scripts executáveis e `docker-compose.yml` para desenvolvimento local.

Critérios de Aceite:

- Comandos/scripts simples para iniciar backend e frontend em modo dev; docker-compose inicia Postgres com credenciais compatíveis com `.env.example`.

Dependências:

- H01, H02

Estimativa: 0.5d (4 horas)

Checklist de QA:

- Em máquina limpa, rodar `docker-compose up` e os scripts de start e verificar conectividade entre backend e Postgres.
