# H04 — Autenticação painel (login JWT) + user store básico

Descrição:
Implementar endpoint de login para o painel da escola, com JWT, e persistência básica do usuário da escola (email + senha hash).

Critérios de Aceite:

- POST /api/login retorna JWT válido.
- Senhas armazenadas com hash seguro (bcrypt/argon2).
- Endpoint de alteração de e‑mail/senha disponível no painel.

Estimativa: 3d
Responsável: Dev 5
