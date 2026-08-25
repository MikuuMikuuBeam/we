¡Listo! Se envolvió la verificación de contraseñas de /papuwhats/login y /api/auth/login en un bloque try/catch seguro. 

Ahora, si la contraseña o el hash enviado no coinciden o son incorrectos, la API responderá limpiamente un HTTP 401 Credenciales incorrectas sin generar ningún error 500 en el servidor.
