```yaml
version: '3.5'

services:
  scrutiny:
    container_name: scrutiny
    image: ghcr.io/analogj/scrutiny:master-omnibus
    cap_add:
      - SYS_RAWIO
      - SYS_ADMIN
    ports:
      - "8080:8080" # webapp
      - "8086:8086" # influxDB admin
    volumes:
      - /run/udev:/run/udev:ro
      - ./config:/opt/scrutiny/config
      - ./influxdb:/opt/scrutiny/influxdb
    devices:
      - "/dev/nvme0"
      - "/dev/sdb"
      - "/dev/nvme1"
      - "/dev/sda"
      - "/dev/sdn"
      - "/dev/sdk"
      - "/dev/sdd"
      - "/dev/sdg"
      - "/dev/sdf"
      - "/dev/sdh"
      - "/dev/sdi"
      - "/dev/sdo"
      - "/dev/sdj"
      - "/dev/sdl"
      - "/dev/sde"
      - "/dev/sdm"
      - "/dev/sdp"
      - "/dev/sdq"
```
