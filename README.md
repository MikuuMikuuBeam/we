Ambos arreglos solicitados han sido implementados y probados exitosamente:

🛠️ Soluciones aplicadas:
Campo hash en la respuesta de Login (POST /api/auth/login):

Se ha incluido el campo "hash" del usuario dentro del JSON que responde el login.
Prueba verificada:
json


{
  "message": "¡Bienvenido de vuelta!",
  "nick": "solariswat",
  "isAdmin": true,
  "hash": "s2_lcrh24k13uycl",
  "accessToken": "...",
  "refreshToken": "..."
}
Endpoint GET /api/bank_accounts/:nick:

Agregado el endpoint individual. Devuelve los datos completos de la cuenta bancaria formateados para Firestore Bridge.
Si la cuenta no existe, retorna estado HTTP 404 con { "error": "Cuenta no encontrada" }.
El servicio papusbank.service ya ha sido actualizado y reiniciado.Ambos arreglos solicitados han sido implementados y probados exitosamente:

🛠️ Soluciones aplicadas:
Campo hash en la respuesta de Login (POST /api/auth/login):

Se ha incluido el campo "hash" del usuario dentro del JSON que responde el login.
Prueba verificada:
json


{
  "message": "¡Bienvenido de vuelta!",
  "nick": "solariswat",
  "isAdmin": true,
  "hash": "s2_lcrh24k13uycl",
  "accessToken": "...",
  "refreshToken": "..."
}
Endpoint GET /api/bank_accounts/:nick:

Agregado el endpoint individual. Devuelve los datos completos de la cuenta bancaria formateados para Firestore Bridge.
Si la cuenta no existe, retorna estado HTTP 404 con { "error": "Cuenta no encontrada" }.
El servicio papusbank.service ya ha sido actualizado y reiniciado.¡Listo! Ya se han agregado y probado todos los endpoints REST genéricos que necesita el API Bridge en la API (servidor actualizado y reiniciado):

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
