```yaml
version: '3'

services:

  teleport:
    image: quay.io/gravitational/teleport:10.0.2
    user: 1000:1000
    container_name: teleport
    entrypoint: /usr/bin/dumb-init
    command: "teleport start -d -c /etc/teleport/teleport.yml"
    ports:
      - "3023:3023"
      - "3024:3024"
      - "3025:3025"
      - "443:443"
    volumes:
      - /home/xcad/teleport-passwordless/config:/etc/teleport
      - /home/xcad/teleport-passwordless/data:/var/lib/teleport
```
