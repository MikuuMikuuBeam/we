Revisión de los logs del backend realizada:
1. Base de datos: El archivo `BACKUP_DATOS.json` SÍ está completamente importado en PostgreSQL (19 usuarios, 10 cuentas bancarias y 8,771 transacciones verificados). 
2. Error visto en logs: El frontend llamó a `/api/bank/undefined`. Recuerda pasar el nick real en la URL (ej: `/api/bank/solariswat`).
3. Lógica del Login (`POST /api/auth/login`):
   - Si le envías `{ "nick": "...", "hash": "s2_..." }`, el backend COMPARARÁ DIRECTO contra PostgreSQL.
   - Si le envías `{ "nick": "...", "password": "..." }`, el backend RE-HASHEARÁ con SHA256+salt en formato base36 (`s2_...`) y luego comparará.
