Ya corregí el túnel. El proceso de cloudflared se había quedado colgado apuntando a una instancia vieja. Ya lo reinicié y el backend está respondiendo perfectamente en localhost:3001.

La nueva URL pública limpia es:
- API Base: https://expanded-bracelets-puts-wild.trycloudflare.com/api
- Panel Admin: https://expanded-bracelets-puts-wild.trycloudflare.com/admin-dashboard

Ya puedes apuntar el frontend a esa dirección y probar.
