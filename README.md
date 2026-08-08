¡Listo! He realizado los dos cambios necesarios:

1. 🗄️ Base de Datos (PostgreSQL):
Agregadas las 15 columnas a la tabla users como VARCHAR(100) con DEFAULT NULL:

mushokurank
berserkrank
chainsawrank
deathnoterank
elfenrank
rerank
rimururank
bocchirank
vocaloidrank
floresrank
ben10rank
godzillarank
mharank
nanatsurank
frierenrank
2. 📡 Endpoint PUT /api/users/:nick:
Actualizado 
src/routes/bridge.js
 para mapear y aceptar todas estas columnas tanto si el frontend las envía exactamente en minúsculas (ej. frierenrank) como si las envía en camelCase (ej. frierenRank).

Probado exitosamente con solicitudes de prueba. El backend ya guarda y responde los rangos de cada fandom.
