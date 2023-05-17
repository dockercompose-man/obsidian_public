```yaml
version: '3.3'

services:
   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     volumes:
       - /portainer/Files/AppData/Config/wordpress:/var/www/html
     ports:
       - "80:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: ${WORDPRESS_DB_HOST}
       WORDPRESS_DB_USER: ${WORDPRESS_DB_USER}
       WORDPRESS_DB_PASSWORD: ${WORDPRESS_DB_PASSWORD}

   db:
     image: mysql:8
     volumes:
       - /portainer/Files/AppData/Config/wordpress/db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
       MYSQL_DATABASE: ${MYSQL_DATABASE}
       MYSQL_USER: ${MYSQL_USER}
       MYSQL_PASSWORD: ${MYSQL_PASSWORD}
volumes:
    wordpress_files:
    db_data:
```
