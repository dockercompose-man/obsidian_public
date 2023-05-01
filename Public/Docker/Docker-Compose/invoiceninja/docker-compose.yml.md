```yaml
version: '3.7'

services:
  server:
    image: nginx
    restart: always
    env_file: env
    volumes:
      # Vhost configuration
      #- ./config/caddy/Caddyfile:/etc/caddy/Caddyfiledocker-com
      - ./config/nginx/in-vhost.conf:/etc/nginx/conf.d/in-vhost.conf:ro
      - ./docker/app/public:/var/www/app/public:ro
    depends_on:
      - app
    # Run webserver nginx on port 80
    # Feel free to modify depending what port is already occupied
    ports:
      - "80:80"
      - "443:443"
    networks:
      - invoiceninja
    extra_hosts:
      - "in5.localhost:192.168.0.124 " #host and ip

  app:
    image: invoiceninja/invoiceninja:5
    env_file: env
    restart: always
    volumes:
      - ./config/hosts:/etc/hosts:ro
      - ./docker/app/public:/var/www/app/public:rw,delegated
      - ./docker/app/storage:/var/www/app/storage:rw,delegated
    depends_on:
      - db
    networks:
      - invoiceninja
    extra_hosts:
      - "in5.localhost:192.168.0.124 " #host and ip

  db:
    image: mysql:8
#    When running on ARM64 use MariaDB instead of MySQL
#    image: mariadb:10.4
#    For auto DB backups comment out image and use the build block below
#    build:
#      context: ./config/mysql
    ports:
      - "3306:3306"
    restart: always
    env_file: env
    volumes:
      - ./docker/mysql/data:/var/lib/mysql:rw,delegated

      # remove comments for next 4 lines if you want auto sql backups
      #- ./docker/mysql/bak:/backups:rw
      #- ./config/mysql/backup-script:/etc/cron.daily/daily:ro
      #- ./config/mysql/backup-script:/etc/cron.weekly/weekly:ro
      #- ./config/mysql/backup-script:/etc/cron.monthly/monthly:ro
    networks:
      - invoiceninja
    extra_hosts:
      - "in5.localhost:192.168.0.124 " #host and ip

  # THIS IS ONLY A VALID CONFIGURATION FOR IN 4. DO NOT USE FOR IN 5.
  # cron:
  #   image: invoiceninja/invoiceninja:alpine-4
  #   volumes:
      # - ./docker/app/public:/var/www/app/public:rw,delegated
      # - ./docker/app/storage:/var/www/app/storage:rw,delegated
      # - ./docker/app/public/logo:/var/www/app/public/logo:rw,delegated
  #   entrypoint: |
  #     /bin/sh -c 'sh -s <<EOF
  #     trap "break;exit" SIGHUP SIGINT SIGTERM
  #     sleep 300s
  #     while /bin/true; do
  #       ./artisan ninja:send-invoices
  #       ./artisan ninja:send-reminders
  #       sleep 1d
  #     done
  #     EOF'
  #   networks:
  #     - invoiceninja
  #

networks:
  invoiceninja:  
------------------------------------------------------------------------------------
.env
------------------------------------------------------------------------------------
# IN application vars
APP_URL=https://invoice.yourdomain.com
APP_KEY=
APP_DEBUG=false
REQUIRE_HTTPS=false
PHANTOMJS_PDF_GENERATION=false
PDF_GENERATOR=snappdf
TRUSTED_PROXIES='*'


QUEUE_CONNECTION=database

# DB connection
DB_HOST=db
DB_PORT=3306
DB_DATABASE=ninja
DB_USERNAME=ninja
DB_PASSWORD=

# Create initial user
# Default to these values if empty
# IN_USER_EMAIL=admin@example.com
# IN_PASSWORD=changeme!
#IN_USER_EMAIL=
#IN_PASSWORD=

# Mail options
MAIL_MAILER=log
MAIL_HOST=email.com
MAIL_PORT=2525
MAIL_USERNAME=your@email.com
MAIL_PASSWORD=
MAIL_ENCRYPTION=starttls
MAIL_FROM_ADDRESS='your@email.com'
MAIL_FROM_NAME='Invoice Ninja'

# MySQL
MYSQL_ROOT_PASSWORD=
MYSQL_USER=ninja
MYSQL_PASSWORD=
MYSQL_DATABASE=ninja

# V4 env vars
# DB_STRICT=false
# APP_CIPHER=AES-256-CBC
```
