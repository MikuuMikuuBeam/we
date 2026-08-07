🛠️ Tablas Creadas en PostgreSQL:
user_inventory (id, nick, item_id, item_type, purchased_at, expires_at, active)
unlockable_titles (id, title, requirement_type, requirement_value, icon)
avatar_shop (id, filename, name, price_ppc, price_usd, category, limited)
effects_shop (id, name, css_class, price_ppc, price_usd, category)
Columnas cosméticas agregadas a users: nick_color, nick_style, avatar_frame, active_title, active_effect.
📡 Endpoints Disponibles:
🛍️ Inventario y Aros de Perfil
POST /api/inventory/buy: Compra items descontando saldo (PPC o PUSD) y agregándolos al inventario.
GET /api/inventory/:nick: Devuelve todos los items del usuario (activos y vigentes).
PUT /api/inventory/:nick/activate: Activa un item de inventario (desactiva otros del mismo tipo automáticamente y actualiza el aro de perfil en users).
PUT /api/inventory/:nick/deactivate: Desactiva un item de inventario.
🎨 Nick, Marcos, Efectos y Títulos
PUT /api/users/:nick/premium-settings: Guarda nickColor (rainbow, fire, ice, neon, gold) y nickStyle.
PUT /api/users/:nick/avatar-frame: Asigna marco de avatar (frame_fire, frame_ice, frame_neon, frame_galaxy).
PUT /api/users/:nick/title: Asigna el título activo mostrado en perfil y leaderboard.
PUT /api/users/:nick/active-effect: Asigna efecto activo (fire_particles, star_rain, neon_aura).
🚀 Boosters & Títulos Desbloqueables
POST /api/boosters/activate: Activa boosters (xp_boost, pp_boost, luck_boost) con tiempo límite en horas.
GET /api/titles/available/:nick: Calcula en tiempo real qué títulos desbloqueó el usuario según su balance, nivel o transferencias.
🛒 Tienda de Avatares y Efectos
GET /api/shop/avatars y POST /api/shop/avatars/buy: Catálogo y compra de skins/avatares.
GET /api/shop/effects y POST /api/shop/effects/buy: Catálogo y compra de efectos visuales.
El servidor fue reiniciado y todo probado con éxito. ¡Tu backend ya soporta la tienda premium completa!
