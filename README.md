Revisión de los logs del backend realizada:

1. Base de datos: El archivo `BACKUP_DATOS.json` SÍ está completamente importado en PostgreSQL (19 usuarios, 10 cuentas bancarias y 8,771 transacciones verificados). 

2. Error visto en logs: El frontend llamó a `/api/bank/undefined`. Recuerda pasar el nick real en la URL (ej: `/api/bank/solariswat`).

3. Lógica del Login (`POST /api/auth/login`):
   - Si le envías `{ "nick": "...", "hash": "s2_..." }`, el backend COMPARARÁ DIRECTO contra PostgreSQL.
   - Si le envías `{ "nick": "...", "password": "..." }`, el backend RE-HASHEARÁ con SHA256+salt en formato base36 (`s2_...`) y luego comparará.¡Hola! He migrado exitosamente el backend de PapusBank de Firebase/Firestore a PostgreSQL + Node.js/Express, corriendo localmente en el servidor CachyOS con HTTPS mediante un túnel público.
Por favor, actualiza el frontend reemplazando las llamadas a Firestore con peticiones HTTP fetch() hacia la nueva API REST.
---
### 🌐 1. BASE URL DEL BACKEND
Sustituye la configuración de Firebase por esta URL base de la API:
- URL pública API (HTTPS): `https://friend-usage-image-cancel.trycloudflare.com/api`
---
### 🔑 2. AUTENTICACIÓN (JWT)
**Login (`POST /api/auth/login`)**
- Body (JSON): `{ "nick": "nick_usuario", "hash": "hash_en_base36" }`
  *(Nota: El backend soporta el mismo formato de hash `s2_XXXX` que calculaba el frontend anteriormente)*
- Respuesta: `{ "accessToken": "JWT_TOKEN...", "refreshToken": "JWT_REFRESH...", "nick": "...", "isAdmin": true|false }`
Guarda el `accessToken` en `localStorage` o `sessionStorage` para enviarlo en los headers de las siguientes peticiones:
```js
headers: {
  "Content-Type": "application/json",
  "Authorization": `Bearer ${accessToken}`
}
📡 3. ENDPOINTS PRINCIPALES PARA INTEGRAR
Perfil de Usuario (GET /api/user/:nick)

Retorna la información pública del usuario (avatar, rangos anime, logros, karma, pareja, etc.).
Cuenta Bancaria (GET /api/bank/:nick)

Header: Authorization: Bearer <token>
Retorna: { balance, totalIn, totalOut, txCount, frozen, inventory, bio, ... }
Transferencias de PPC (POST /api/bank/transfer)

Header: Authorization: Bearer <token>
Body: { "to": "nick_destino", "amount": 1000, "note": "regalo" }
Comprar Rangos (POST /api/rank/buy)

Header: Authorization: Bearer <token>
Body: { "rankId": "gojo" }
Leaderboard (GET /api/leaderboard?limit=50)

Retorna el ranking de usuarios ordenados por saldo de PPC.
Tablón de Anuncios (GET /api/board y POST /api/board)

GET: Lista los posts del tablón.
POST: Publica un mensaje { "msg": "Hola clan" } (requiere Token).
Chat General (GET /api/chat y POST /api/chat)

GET: Obtiene los últimos 100 mensajes.
POST: Envía un mensaje al chat { "msg": "Texto..." } (requiere Token).
Mensajes Directos / Social (GET /api/social/messages y POST /api/social/messages)

GET: Obtiene la bandeja de entrada.
POST: Envía mensaje privado { "to": "destinatario", "msg": "hola" }.
Parejas / Flores (POST /api/flores/request y POST /api/flores/accept/:id)

Manejo de solicitudes de pareja y relación.
Bóveda Compartida (POST /api/vault/deposit y POST /api/vault/withdraw)

Body: { "vaultId": "nombre_boveda", "amount": 500 }.
Préstamos (POST /api/loans/request y POST /api/loans/pay)

Solicitar o pagar préstamos bancarios.
Historial de Transacciones (GET /api/transactions/:nick)

Muestra las transacciones enviadas/recibidas del usuario.
⚠️ NOTAS DE INTEGRACIÓN
Todas las respuestas devolverán un código HTTP 200/201 en éxito o 400/401/403/404/409 con { "error": "mensaje" } en caso de falla.
La API tiene CORS habilitado para https://lospapusxdd.github.io.
Si el Access Token expira (duran 1h), puedes llamar a POST /api/auth/refresh enviando { "refreshToken": "..." } para obtener uno nuevo sin pedir contraseña de nuevo.
