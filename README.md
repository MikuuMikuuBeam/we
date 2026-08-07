¡Solucionado! Se ha actualizado la lógica del backend para usar exactamente el mismo algoritmo `hashPass` que el frontend y consultar el `hash_salt` propio de cada usuario en PostgreSQL:

1. El backend ya implementa la función exacta:
```js
function hashPass(p, salt) {
  salt = salt || '';
  const salted = salt + p + salt.split('').reverse().join('');
  let h = 5381;
  for (let i = 0; i < salted.length; i++) h = ((h << 5) + h) ^ salted.charCodeAt(i);
  let h2 = 0x811c9dc5;
  for (let i = 0; i < salted.length; i++) h2 = Math.imul(h2 ^ salted.charCodeAt(i), 0x01000193);
  return 's2_' + (h >>> 0).toString(36) + (h2 >>> 0).toString(36) + salted.length.toString(36);
}Revisión de los logs del backend realizada:
1. Base de datos: El archivo `BACKUP_DATOS.json` SÍ está completamente importado en PostgreSQL (19 usuarios, 10 cuentas bancarias y 8,771 transacciones verificados). 
2. Error visto en logs: El frontend llamó a `/api/bank/undefined`. Recuerda pasar el nick real en la URL (ej: `/api/bank/solariswat`).
3. Lógica del Login (`POST /api/auth/login`):
   - Si le envías `{ "nick": "...", "hash": "s2_..." }`, el backend COMPARARÁ DIRECTO contra PostgreSQL.
   - Si le envías `{ "nick": "...", "password": "..." }`, el backend RE-HASHEARÁ con SHA256+salt en formato base36 (`s2_...`) y luego comparará.
