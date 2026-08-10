1. 🔐 Endpoints 2FA Backend Implementados
POST /api/auth/login:

Si el usuario tiene twofa_enabled = true, responde:
json


{ "twofaRequired": true, "tempToken": "JWT_TEMP_TOKEN" }
tempToken expira en 5 minutos, viene con flag isTemp2FA: true y no otorga acceso general.
POST /api/auth/2fa/confirm:

Body: { "tempToken": "...", "code": "123456" }
Valida contra el secreto TOTP o contra un código de respaldo (BACKUP-XXXX-XXXX).
Al usar un código de respaldo, se marca como usado en DB.
En caso de éxito, retorna los tokens reales (accessToken, refreshToken, hash, etc.).
En error, retorna 401 "Código inválido".
POST /api/auth/2fa/setup (requiere auth JWT):

Genera secreto TOTP con otplib y lo guarda en users.twofa_pending_secret.
Responde { "secret": "...", "otpauthUrl": "otpauth://totp/PapusBank:nick...?secret=...&issuer=PapusBank" }.
POST /api/auth/2fa/verify (requiere auth JWT):

Body: { "code": "123456" }
Verifica contra twofa_pending_secret.
Marca twofa_enabled = true, mueve el secreto a twofa_secret, invalida el pendiente y genera 10 códigos de respaldo hasheados con SHA-256 (BACKUP-XXXX-XXXX).
Responde { "backupCodes": ["BACKUP-XXXX-XXXX", ...] } en texto plano por única vez.
POST /api/auth/2fa/disable (requiere auth JWT):

Body: { "code": "123456" }
Requiere TOTP válido para marcar twofa_enabled = false y limpiar secretos/backups.
POST /api/auth/2fa/backup-codes (requiere auth JWT):

Body: { "code": "123456" }
Requiere TOTP válido para generar y retornar 10 nuevos códigos de respaldo.
GET /api/user/:nick:

Ahora incluye "twofa_enabled": true/false dentro de la respuesta.
2. 🧹 Cleanup
Encuesta id = 5 ("Test de votacion") borrada.
Cuentas de prueba test_ranks_x y test_finger2 verificadas y eliminadas.
3. ⚡ Operaciones Atómicas
La ruta POST /api/bank/transfer fue optimizada usando UPDATE ... RETURNING balance, evitando la lectura previa con SELECT extra y eliminando condiciones de carrera por doble click.
