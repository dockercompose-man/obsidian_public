https://computingforgeeks.com/run-semaphore-ansible-in-docker/

-   _MYSQL_USER_ and _SEMAPHORE_DB_USER_ with the desired database user.
-   _MYSQL_PASSWORD_ and _SEMAPHORE_DB_PASS_ with the database password for the user
-   _SEMAPHORE_ADMIN_PASSWORD_ with the password for the admin user for Semaphore Ansible web UI
-   _SEMAPHORE_ACCESS_KEY_ENCRYPTION_ with the key to encrypt the access keys in your database. This key encryption can be generated using the command:

```bash
head -c32 /dev/urandom | base64
```
EXAMPLE:
```bash
MflCLIUF5bn6Lgkuwy4BoAdIFhoZ4Ief2oocXmuZSjs=
```

