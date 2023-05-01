```yaml
version: "3"

services:
  bind9:
    container_name: bind9
    image: ubuntu/bind9:latest
    environment:
      - BIND9_USER=root
      - TZ=America/Toronto
    ports:
      - "53:53/tcp"
      - "53:53/udp"
    volumes:
      - /portainer/Files/AppData/Config/Bind9/config:/etc/bind
      - /portainer/Files/AppData/Config/Bind9/cache:/var/cache/bind
      - /portainer/Files/AppData/Config/Bind9/records:/var/lib/bind
    restart: always
```

