```yaml
version: '3'
services:
  coturn:
    image: coturn/coturn
    ports:
      - "3478:3478"
      - "3478:3478/udp"
      - "5349:5349" #change to whatever you want
      - "5349:5349/udp" #change to whatever you want
      - "10000:49152/udp"
    volumes:
      - ./conf:/etc/turnserver/
      - ./cert:/etc/turnserver/cert
      - ./data:/var/run/
    environment:
      - PUID=1000
      - PGID=1000

```
