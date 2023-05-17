##### Change User's Primary Group (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
usermod -g new_primary_group username
```

##### Add User to Secondary Group (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
usermod -a -G group username
```
OR
```bash
usermod -aG group username
```

##### Change Group Ownership (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
chgrp group filename or directory
```

##### View what groups a user belongs to (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
groups username
```
OR
```bash
less /etc/group | grep username
```

##### View if a user exists on the system (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
id username
```
OR
```bash
less /etc/shadow | grep username
```

##### List All Users on the System (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
cut -d: -f1 /etc/passwd | sort
```
