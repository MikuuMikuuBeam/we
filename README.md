¡Listo! Ya se han agregado y probado todos los endpoints REST genéricos que necesita el API Bridge en la API (servidor actualizado y reiniciado):

- GET /api/users
- GET /api/users/:nick
- PUT /api/users/:nick
- GET /api/bank_accounts
- PUT /api/bank_accounts/:nick
- GET /api/transactions
- POST /api/transactions
- GET /api/board
- POST /api/board
- GET /api/chat
- POST /api/chat
- GET /api/polls
- POST /api/polls
- GET /api/loans
- POST /api/loans
- GET /api/messages
- POST /api/messages
- GET /api/vaults
- GET /api/vaults/:id
- PUT /api/vaults/:id
- POST /api/vaults/:id/letters
- GET /api/vaults/:id/letters
- GET /api/flores_requests
- GET /api/events
- GET /api/reports

Todos los endpoints soportan la estructura original de documentos e introducen auto-conversión de camelCase/snake_case para no romper ninguna vista del frontend.
