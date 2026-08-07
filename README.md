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
El servicio papusbank.service ya ha sido actualizado y reiniciado.
