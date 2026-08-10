¡Corregidos los dos errores 500! 🛠️🚀

🔍 Causas de los 500 identificadas:
Error de Mapeo en el Bridge SQL (bridge.js): Al intentar escribir twofa_pending_secret mediante PUT /api/users/:nick, el mapeador intentaba buscar twofapendingsecret en minúsculas y no lo encontraba en fieldMap, generando un error SQL no existe la columna «twofapendingsecret».
Incompatibilidad con API de otplib v13: En la versión instalada de otplib (v13+), authenticator fue deprecado/removido en favor de generateSecret, generateURI y verifySync. La llamada a authenticator.options = { window: 1 } lanzaba un TypeError: Cannot set properties of undefined.
🛠️ Soluciones aplicadas:
src/routes/bridge.js: Se mapearon explícitamente todas las variantes (twofaEnabled, twofa_enabled, twofaSecret, twofaPendingSecret, twofapendingsecret, twofaBackupCodes, etc.) a sus columnas correspondientes en la DB.
src/routes/auth.js: Se actualizaron todos los handlers de 2FA (/2fa/confirm, /2fa/setup, /2fa/verify, /2fa/disable, /2fa/backup-codes) para consumir la API moderna síncrona de otplib:
otplib.generateSecret()
otplib.generateURI({ label: nick, issuer: 'PapusBank', secret })
otplib.verifySync({ token, secret })
Probado y respondiendo correctamente (401 Token requerido en solicitudes sin autenticar en lugar de 500 Error interno).
