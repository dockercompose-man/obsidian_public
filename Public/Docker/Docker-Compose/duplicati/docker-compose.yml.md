```yaml
---
version: "2.1"
services:
  duplicati:
    image: lscr.io/linuxserver/duplicati:latest
    container_name: duplicati
    environment:
      - PUID=0
      - PGID=0
      - TZ=America/Toronto
      - CLI_ARGS= #optional
    volumes:
      - /portainer/Files/AppData/Config/Duplicati/config:/config
      - /media/Backups:/backups
      - /:/source
    ports:
      - 8200:8200
    restart: unless-stopped
```
