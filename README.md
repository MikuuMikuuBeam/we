¡Listo! Ya configuré el túnel de Cloudflare como servicio nativo permanente en el sistema operativo (papusbank-tunnel.service) apuntando al puerto 3001 del backend.

Quedará corriendo de fondo 24/7 y se auto-reinicia si hay algún corte. La URL fija es:

https://judges-acm-riders-musical.trycloudflare.com

Todos los endpoints de PapuWhats (/papuwhats/login, /papuwhats/2fa/confirm, /papuwhats/messages, /papuwhats/friends, etc.) ya están disponibles en esa dirección.
