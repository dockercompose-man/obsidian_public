```yaml
version: "2.1"
services:
  phpmyadmin:
    image: lscr.io/linuxserver/phpmyadmin:latest
    container_name: phpmyadmin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New York
      - PMA_ARBITRARY=1 #optional
      - FILE__PASSWORD=./data/config/keys/.pass
#      - PMA_ABSOLUTE_URI=https://phpmyadmin.yourdomain.com #optional
    volumes:
      - ./data/config:/config
    ports:
      - 80:80
    restart: unless-stopped
```
