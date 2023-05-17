```yaml
version: '3'

services:
  vanilla-forums:
    image: vanillaforums
    build:
      context:  ./src
    container_name: vanilla-forums
    restart: always
    volumes:
      - "./data:/var/www/html/upload"
    ports:
      - 80:80
    environment:
      - DB_ROOT_PASSWORD=${DB_ROOT_PASSWORD}
      - DB_NAME=${DB_NAME}
      - DB_USER=${DB_USER}
      - DB_PASSWORD=${DB_PASSWORD}
    depends_on:
      - db
    env_file:
      - .env
  db:
    image: mysql:8
    environment:
      - MYSQL_ROOT_PASSWORD=${DB_ROOT_PASSWORD}
      - MYSQL_DATABASE=${DB_NAME}
      - MYSQL_USER=${DB_USER}
      - MYSQL_PASSWORD=${DB_PASSWORD}
    env_file:
      - .env
    ports:
      - "3306:3306"
    volumes:
     - "./data:/var/lib/mysql"
```
