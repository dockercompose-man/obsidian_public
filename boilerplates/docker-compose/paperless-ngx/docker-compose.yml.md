```yaml
# docker-compose file for running paperless from the docker container registry.
# This file contains everything paperless needs to run.
# Paperless supports amd64, arm and arm64 hardware.
#
# All compose files of paperless configure paperless in the following way:
#
# - Paperless is (re)started on system boot, if it was running before shutdown.
# - Docker volumes for storing data are managed by Docker.
# - Folders for importing and exporting files are created in the same directory
#   as this file and mounted to the correct folders inside the container.
# - Paperless listens on port 8000.
#
# In addition to that, this docker-compose file adds the following optional
# configurations:
#
# - Instead of SQLite (default), PostgreSQL is used as the database server.
# - Apache Tika and Gotenberg servers are started with paperless and paperless
#   is configured to use these services. These provide support for consuming
#   Office documents (Word, Excel, Power Point and their LibreOffice counter-
#   parts.
#
# To install and update paperless with this file, do the following:
#
# - Copy this file as 'docker-compose.yml' and the files 'docker-compose.env'
#   and '.env' into a folder.
# - Run 'docker-compose pull'.
# - Run 'docker-compose run --rm webserver createsuperuser' to create a user.
# - Run 'docker-compose up -d'.
#
# For more extensive installation and update instructions, refer to the
# documentation.

version: "3.4"
services:
  broker:
    image: docker.io/library/redis:7
    restart: unless-stopped
    volumes:
      - "./redisdata:/data"
  db:
    image: docker.io/library/mariadb:10
    restart: unless-stopped
    volumes:
      - "./dbdata:/var/lib/mysql"
    environment:
      MARIADB_HOST: ${DB_HOST}
      MARIADB_DATABASE: ${DB_NAME}
      MARIADB_USER: ${DB_USER}
      MARIADB_PASSWORD: ${DB_PASSWORD}
      MARIADB_ROOT_PASSWORD: ${DB_ROOT_PASSWORD}
    env_file:
      - .env
    ports:
      - 3306:3306
  webserver:
    image: ghcr.io/paperless-ngx/paperless-ngx:latest
    restart: unless-stopped
    depends_on:
      - db
      - broker
      - gotenberg
      - tika
    ports:
      - 8000:8000
    healthcheck:
      test: ["CMD", "curl", "-fs", "-S", "--max-time", "2", "http://localhost:8000"]
      interval: 30s
      timeout: 10s
      retries: 5
    volumes:
      - "./data:/usr/src/paperless/data"
      - "./media:/usr/src/paperless/media"
      - "./export:/usr/src/paperless/export"
      - "/media/paperless/consume:/usr/src/paperless/consume"
    env_file: .env
    environment:
      PAPERLESS_REDIS: redis://broker:6379
      PAPERLESS_DBENGINE: mariadb
      PAPERLESS_DBHOST: db
      PAPERLESS_DBUSER: ${DB_USER}
      PAPERLESS_DBPASS: ${DB_PASSWORD}
      PAPERLESS_DBPORT: 3306
      PAPERLESS_TIKA_ENABLED: 1
      PAPERLESS_TIKA_GOTENBERG_ENDPOINT: http://gotenberg:3000
      PAPERLESS_TIKA_ENDPOINT: http://tika:9998
  gotenberg:
    image: docker.io/gotenberg/gotenberg:7.6
    restart: unless-stopped

    # The gotenberg chromium route is used to convert .eml files. We do not
    # want to allow external content like tracking pixels or even javascript.
    command:
      - "gotenberg"
      - "--chromium-disable-javascript=true"
      - "--chromium-allow-list=file:///tmp/.*"
  tika:
    image: ghcr.io/paperless-ngx/tika:latest
    restart: unless-stopped

volumes:
  data:
  media:
  dbdata:
  redisdata:
```
