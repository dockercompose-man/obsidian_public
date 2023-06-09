```yaml
version: '3.7'
services:
  openldap:
    image: osixia/openldap:latest
    container_name: openldap
    hostname: openldap
    ports:
      - "389:389"
      - "636:636"
    volumes:
      - ./data/certificates:/container/service/slapd/assets/certs
      - ./data/slapd/database:/var/lib/ldap
      - ./data/slapd/config:/etc/ldap/slapd.d
    environment:
      - LDAP_ORGANISATION=yourorg
      - LDAP_DOMAIN=yourdomain.com
      - LDAP_ADMIN_USERNAME=admin
      - LDAP_ADMIN_PASSWORD=youradminpassword
      - LDAP_CONFIG_PASSWORD=yourconfigpassword
      - "LDAP_BASE_DN=dc=domainname,dc=com"
      - LDAP_TLS_CRT_FILENAME=domainname.com.crt
      - LDAP_TLS_KEY_FILENAME=domainname.com.key
      - LDAP_TLS_CA_CRT_FILENAME=domainname.com.ca.crt
      - LDAP_READONLY_USER=true
      - LDAP_READONLY_USER_USERNAME=user-ro
      - LDAP_READONLY_USER_PASSWORD=ro_password #change
    networks:
      - openldap

  phpldapadmin:
    image: osixia/phpldapadmin:latest
    container_name: phpldapadmin
    hostname: phpldapadmin
    ports:
      - "80:80"
    environment:
      - PHPLDAPADMIN_LDAP_HOSTS=openldap
      - PHPLDAPADMIN_HTTPS=false
    depends_on:
      - openldap
    networks:
      - openldap

networks:
  openldap:
    driver: bridge
```
