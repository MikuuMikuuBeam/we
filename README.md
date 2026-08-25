Columna secret_achievements: Se ejecutó en PostgreSQL:
sql


ALTER TABLE users ADD COLUMN IF NOT EXISTS secret_achievements JSONB DEFAULT '[]';
(La columna ya existe en users y persiste correctamente los arreglos JSON).
Nuevas Tablas para Amigos (PapuWhats):
friends (id, nick1, nick2, created_at, UNIQUE(nick1, nick2))
friend_requests (id, from_nick, to_nick, status, created_at)
2. 🛣️ Rutas y Endpoints en la API (/api vs /papuwhats)
Endpoints de PapusBank original (/api/...):

POST /api/auth/login y POST /api/auth/register siguen intactos. (El 404 del agente fue porque llamó a /auth/login sin el prefijo /api).
GET /api/user/:nick / GET /api/users/:nick: Exponen explícitamente tanto secret_achievements como secretAchievements.
PUT /api/users/:nick: Acepta tanto secret_achievements como secretAchievements en la lista blanca de actualización.
Nuevos Endpoints para la app PapuWhats (/papuwhats/...):

POST /papuwhats/login (soporta claves bcrypt y hashPass de PapusBank, devuelve twofaRequired si tiene 2FA).
POST /papuwhats/2fa/confirm
GET /papuwhats/messages y POST /papuwhats/messages
PUT /papuwhats/messages/:id y DELETE /papuwhats/messages/:id
GET /papuwhats/friends y POST /papuwhats/friends/request, /accept, /reject, DELETE /friends/:nick
GET /papuwhats/conversations
3. 🌐 CORS y Middleware
Se agregó configuración permisiva de CORS para los endpoints /papuwhats/* (Access-Control-Allow-Origin: *) para evitar bloqueos desde aplicaciones nativas en Android.
Se agregaron validaciones con try/catch y sanitización en hashPass(p, salt) para garantizar que peticiones con contraseñas o hashes malformados respondan 401 Credenciales incorrectas en lugar de crash 500.
🖥️ Panel Admin (Localhost)
Se añadieron herramientas en la interfaz web local:
Cambiador/reseteador de contraseñas de usuarios.
Columna con geolocalización de IPs.
Pestaña de historial de chats privados (DMs) de PapuWhats con opción de moderación.
Todo el backend está en producción en CachyOS corriendo como servicio systemd (papusbank.service y papusbank-tunnel.service).
