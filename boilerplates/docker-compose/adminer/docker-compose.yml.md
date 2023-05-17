```yaml
version: '3.1'

services:

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080

  db:
    image: mysql:8
    restart: always
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
