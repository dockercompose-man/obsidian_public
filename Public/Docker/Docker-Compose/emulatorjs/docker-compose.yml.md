```yaml
---
version: "2.1"
services:
  emulatorjs:
    image: lscr.io/linuxserver/emulatorjs:latest
    container_name: emulatorjs
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Toronto
      - SUBFOLDER=/ #optional
    volumes:
      - /portainer/Files/Apps/EmulatorJS/config:/config
      - /media/Jellyfin2/ROMS/Organized:/data
    ports:
      - 3070:3000
      - 8070:80
#      - 4001:4001 #optional
    restart: unless-stopped
```
