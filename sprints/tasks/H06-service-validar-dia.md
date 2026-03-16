# H06 — Service: validar dia (sábado/domingo)

Objetivo:
Especificar a regra de negócio que valida se uma data recebida é permitida (somente sábados e domingos) e documentar mensagens de erro associadas.

Entradas / Saídas:

- Entrada: `data_evento` (formato ISO date, ex: 2026-05-09)
- Saída: `ok` booleano ou erro com código HTTP 400 e payload de erro contendo `code` e `message`.

Regras:

- Aceitar somente datas cujo dia da semana seja sábado (SATURDAY) ou domingo (SUNDAY).
- Se inválido, retornar erro: `{ code: "INVALID_DAY", message: "Datas permitidas: sábado ou domingo" }`.

Critérios de Aceite:

- Documento `docs/services/validar_dia.md` descrevendo a regra e exemplos de entradas/saídas.
- Testes unitários definidos (H09.1) devem cobrir pelo menos: uma data válida (sábado), uma data válida (domingo), uma data inválida (segunda-feira).

Dependências:

- H04 (model) para tipos; H05 para integração futura.

Estimativa: 0.25d (2 horas)

Checklist de QA:

- Validar comportamento manual enviando payloads de datas e verificando respostas (documentadas).
