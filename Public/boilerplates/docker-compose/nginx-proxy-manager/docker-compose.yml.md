```yaml
version: "3"
services:
  npm-app:
    image: 'jc21/nginx-proxy-manager:latest'
    container_name: npm-app
    restart: unless-stopped
    ports:
      - '80:80' # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81' # Admin Web Port
      # Add any other Stream port you want to expose
      # - '21:21' # FTP
    environment:
      DB_MYSQL_HOST: ${DB_HOST}
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: ${DB_USER}
      DB_MYSQL_PASSWORD: ${DB_PASSWORD}
      DB_MYSQL_NAME: "npm"
      # Uncomment the line below if IPv6 is not enabled on your host
      DISABLE_IPV6: 'true'
    env_file: .env
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
    depends_on:
      - npm-db
    networks:
      - npm-nw
      - npm-internal

  npm-db:
    image: 'mariadb:latest'
    container_name: npm-db
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: ${DB_ROOT_PASSWORD}
      MYSQL_DATABASE: ${DB_NAME}
      MYSQL_USER: ${DB_USER}
      MYSQL_PASSWORD: ${DB_PASSWORD}
    env_file: .env
    volumes:
      - ./data/mysql:/var/lib/mysql
    networks:
      - npm-internal

networks:
  npm-internal:
  npm-nw:
    external: true
```

