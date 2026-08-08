El problema no era el body parser de Express, sino la estructura de claves esperadas en el cuerpo JSON (req.body).

Originalmente los endpoints de /api/bank/mint y /api/bank/burn buscaban exclusivamente las claves en inglés (to, amount, target, from). Al enviar claves en español (destino y monto), el servidor leía undefined y respondía {"error":"Destino y monto requeridos"}.

🛠️ Solución Aplicada:
He actualizado el router de banco (
src/routes/bank.js
) en los endpoints /mint, /burn, /transfer, /set-balance y /freeze para aceptar indistintamente los nombres de propiedades tanto en español como en inglés:

Destino/Usuario: acepta destino, monto, to, target, nick, usuario, origen, from.
Monto/Saldo: acepta monto, amount, saldo, balance.
Notas: acepta nota, note.
🧪 Pruebas Realizadas:
Se ejecutaron pruebas curl contra el servidor activo:

POST /api/bank/mint enviando {"destino":"solariswat","monto":500}:

json


{
  "message": "500 PPC acuñados para solariswat",
  "newBalance": 2474500
}
POST /api/bank/burn enviando {"destino":"solariswat","monto":100}:

json


{
  "message": "100 PPC quemados de solariswat",
  "newBalance": 2474400
}
Ambos endpoints ya procesan las solicitudes correctamente con cualquiera de las dos nomenclaturas
