##### Add User (Debian/Ubuntu)
```bash
adduser username
```

##### Add User (OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
useradd username
```

##### Create user WITH a home directory (Debian/Ubuntu)
```bash
useradd -m username
```

##### Create user WITH a home directory (OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
useradd -m username
```

##### Create/change password for user (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
passwd username
```

##### Add home directory afterwards (Debian/Ubuntu)
```bash
mkdir /home/<username>
chown <username>:<username> /home/<username>
```

##### Add home directory afterwards (OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
mkdir /home/<username>
chown <username>:<username> /home/<username>
```

### Deleting User Account

##### Locking a User Account (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
##### and disable all login methods
```bash
usermod -L username
```

##### Unlocking a User Account (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
usermod -U username
```

##### Remove a User Password (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
usermod -d username
```

##### Delete user home directory and mail spool (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
userdel -r username
```

##### Delete User (Debian/Ubuntu)
```bash
deluser username
```

##### Delete User (OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
userdel username
```

##### Changing a user's default shell to BASH (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
usermod --shell /bin/bash username
```
or
```bash
chsh -s /bin/bash username
```

##### Changing a User UID (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
usermod --uid new_uid username
```

##### Changing a User's GID (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
usermod --gid new_gid username
```

##### Changing a User Name (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
usermod -l new_username old_username
```

##### Locate files owned by a specific user (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
sudo find / -user <username> -type f 2>/dev/null
```

The `2>/dev/null` part of the command is used to redirect error messages to `/dev/null`, so they are not displayed on the screen.

##### Example
```bash
sudo find / -user jdoe -type f 2>/dev/null
```

##### Setting a User Expiry Date (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
chage -E date user_name
```
##### Example
```bash
chage -E 2022-02-21 username
```

##### Disable expiration of an account (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
chage -E -1 username
```

##### View a User's Expiry Date (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
chage -l username
```

**chage** – configure aging passwords
**-m** days – specifies the **minimum** number of days between password changes
**-M** days – specifies the **maximum** number of days between password changes
**-W** days – specifies the number of **warning** days before a password change is required

##### Minimum password age of 5 days, Maximum password age of 90 days, and SEVEN warning days for the user ksanders
```bash
chage -m 5 -M 90 -W 7 ksanders
```

#### **Configuring User Limits**
**Using pam_limits to restrict access to resources**
**configured using the /etc/security/limits.conf file**
Using ulimit to restrict access to resources
**Pam Limits**
domain type item value
_**domain**_ _-_ Describes the entity to which the limit applies. You can use one of the following values:  
**user** - Identifies a specific Linux **user**
**@**_**group_name**_ _-_ Identifies a specific Linux **group**
***** - Specifies **all** **users**
**type** - Defines a **hard** or **soft** **limit**. A hard limit cannot be exceeded. A soft limit can be temporarily exceeded.
**item** - Specifies the **resource** being limited.
**value** - Specifies a **value** for the limit.
**core** – restricts the **size** of **core** files (in KB)
**data** - restricts the **size** of a program’s **data** area in RAM (in KB)
**fsize** - restricts the **size** of **files** created by the user (in KB)
**nofile** – restricts the **number** of data **files** a user may have **open** **concurrently**
**stack** – restricts the **stack** **size** (in KB)
**cpu** – restricts the **CPU** **time** of a single process (in minutes)
**nproc** – restricts the **number** of **concurrent** **processes** a user may run
**maxlogins** – sets the **maxium** number of **simultaneous** **logins** for user
**priority** – sets the **priority** to run user **processes** with
**locks** – sets the maximum **number** of **locked** files**nice** – sets **maximum**
**nice** **priority** a user is allowed to raise a process to

##### Configure user rtracy with a soft CPU limit of 15 minutes. Edit **/etc/security/limits.conf**
```bash
rtracy soft cpu 15
```

##### Limit User rtracy to a Maximum of two Concurrent Logins
```bash
rtracy hard maxlogins 2
```

##### Using ulimit to Restrict Access to Resources
```bash
ulimit options limit
```

##### View the Current Value for All Resource Limits
```bash
ulimit -a
```

–**c** - Sets a limit on the maximum size of **core** **files** in blocks. If you set this limit to a value of **0**, core **dumps** on the system are **disabled**.
–**f** - Sets a limit on the maximum size (in blocks) of **files** created by the shell.–**n** - Sets a limit on the maximum **number** of **open file descriptors**.
–**t** - Sets a limit on the maximum amount of CPU **time** **(in seconds)** a process may use.–**u** - Sets a limit on the maximum number of **processes** **available** to a **single** **user**.
–**d** - Sets a limit on the maximum size (in KB) of a process’s **data** **segment** in RAM.–**m** - Sets a limit on the **maximum** **resident** **size** (in KB) of a process in RAM.–**s** - Sets a limit on the maximum **stack** **size** (in KB).–**H** - Sets a **hard** resource **limit**.
–**S** - Sets a **soft** resource **limit**.

##### Set a Soft Limit of 50 Processes
```bash
ulimit -S -u 50
```

##### Generating a list of logged in users
```bash
w
```

##### Brute Force Log-out for User
```bash
pkill -KILL -u user_name
```
**once everyone is logged off, deny logins**
create a file in /etc named nologin
Enter text inside the file if you wish **“The system is currently unavailable for login.”**

The line is actually read from **/etc/pam.d/login**
```bash
auth requistite pam_nologin.so
```

##### Archive User's Data (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
tar -czvf username-yyyymmdd.tar.gz /home/username
```

##### Modify a User's Properties (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
usermod username options
```

##### Remove a User's Cron Jobs (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
crontab -r -u username
```

##### Remove a User's Print Jobs (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
lpq -a | awk '{print $1}' | xargs cancel
```
##### Change User's Ownership (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
chown user.group file or directory
```
##### Change Just Ownership (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
```bash
chown ksanders /tmp/myfile.txt
```
##### Run Commands Without Password
```bash
orangebackup ALL = NOPASSWD: /usr/bin/rsync, /usr/bin/rsnapshot
```
AND/OR
```
rockybackup ALL = NOPASSWD: /usr/bin/rsync, /usr/bin/rsnapshot
```
