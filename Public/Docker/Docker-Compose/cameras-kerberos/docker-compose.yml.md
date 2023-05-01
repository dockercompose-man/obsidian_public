```yaml
version: '3'

services:
  cameras-kerberos:
    image: kerberos/kerberos
    container_name: cameras-kerberos
    ports:
      - "80:80"
      - "8889:8889"
    volumes:
      - /portainer/Files/AppData/Config/cameras-kerberos/config:/etc/opt/kerberosio/config
      - /portainer/Files/AppData/Config/cameras-kerberos/capture:/etc/opt/kerberosio/capture
      - /portainer/Files/AppData/Config/cameras-kerberos/logs:/etc/opt/kerberosio/logs
      - /portainer/Files/AppData/Config/cameras-kerberos/webconfig:/var/www/web/config
    restart: always

```
