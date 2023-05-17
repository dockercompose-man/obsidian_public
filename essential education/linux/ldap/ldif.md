```bash
dn: ou=groups,dc=example,dc=com
objectClass: organizationalUnit
ou: groups

dn: ou=users,dc=example,dc=com
objectClass: organizationalUnit
ou: users

dn: cn=IT,ou=groups,dc=example,dc=com
objectClass: groupOfNames
cn: IT
member: uid=Mike,ou=users,dc=example,dc=com
member: uid=James,ou=users,dc=example,dc=com

dn: cn=HR,ou=groups,dc=example,dc=com
objectClass: groupOfNames
cn: HR
member: uid=User3,ou=users,dc=example,dc=com

dn: cn=Accounting,ou=groups,dc=example,dc=com
objectClass: groupOfNames
cn: Accounting
member: uid=User4,ou=users,dc=example,dc=com

dn: cn=Nextcloud,ou=groups,dc=example,dc=com
objectClass: groupOfNames
cn: Nextcloud

dn: cn=Jellyfin,ou=groups,dc=example,dc=com
objectClass: groupOfNames
cn: Jellyfin

dn: uid=Mike,ou=users,dc=example,dc=com
objectClass: inetOrgPerson
uid: Mike
givenName: Mike
sn: Smith
cn: Mike Smith
userPassword: {SSHA}PnQ5nmXjovAsvNepb+lPpprM9jqYqMqE
mail: mike@example.com

dn: uid=James,ou=users,dc=example,dc=com
objectClass: inetOrgPerson
uid: James
givenName: James
sn: Johnson
cn: James Johnson
userPassword: {SSHA}LWjBSSJH9k+rO+1gl8UHQ8x68U72zn+j
mail: james@example.com

dn: uid=User3,ou=users,dc=example,dc=com
objectClass: inetOrgPerson
uid: User3
givenName: User
sn: Three
cn: User Three
userPassword: {SSHA}n7dV0aTbHkgpMSt5rwVcwbJYn+ZdD75H
mail: user3@example.com

dn: uid=User4,ou=users,dc=example,dc=com
objectClass: inetOrgPerson
uid: User4
givenName: User
sn: Four
cn: User Four
userPassword: {SSHA}WZvwT9KxIRY6nq9eKj+oszE6uGm/l3Td
mail: user4@example.com
```
