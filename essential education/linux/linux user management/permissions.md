#### **User Permissions**
Permission	Value
	Read		4
	Write		2
	Execute	1
               = 644

Owner		Group		Others
read + write		read		read
4+2 = 6		           4		   4

```bash
drwxr-xr-x 2 ksanders users 4096 Nov 25 17:30 bin
```

**First Column**: displays the **mode** for **each** **file** and **directory**.
**~** - a regular file
**d** - a directory
**s** – a socket
**l** – a link
**p** – a named pipe
**b** – a block device
**c** – a character device

The **next three** characters are the permissions assigned to the owning **group**.  
The **last three** characters in the mode are the permissions assigned to **others**.

##### read/write permissions to users and group but 0 permissions to others
```bash
chmod 660 contacts.odt
```

#### Increase Overall Security with Umask

##### default umask 022 (Owner no permissions removed, Group/Other Write values removed)

##### each digit represents a numeric permission value to be removed.

```bash
umask 022
```

The **first** digit references **Owner**
The **second** digit references **Group**
The **third** digit references **Other**

##### remove execute permission that is automatically assigned to others whenever a new directory is created  

umask 023

##### **umask** is **stored** in **/etc/profile** file or the **/etc/login.defs** file depending on your distribution


#### **Working with Special Permissions**

**SUID**	Set User ID. (only binaries)	**Temporarily** becomes the **file’s** **owner**		None
**SGID**	Set Group ID (only binaries)	**Temporarily** becomes a **member** of the **group**	 Group changes
**Sticky Bit**				When stick bit is assigned to a dir, **users** can **only** **delete** **files** within the dir which **they** **are** **owner** of the **file** or **dir** itself. This negates the effect of having the write permission to a directory, which could allow a user to delete files in a directory they don’t own  
  
SUID: 4  
SGID: 2  
Sticky Bit: 1

##### Simple add an extra number to the beginning of the mode that references the special permissoins you want to associate with the file or directory.  

##### example applying SUID and SGID permissions to a file named run me that should be readable and executable by the Owner and Group.
```bash
chmod 6554 runme
```

#### **Auditing Files**
When the root user owns a file with the SUID permission set, is allows the process created by the file to perform actions as root, which the user who start is is probably not allowed to do.  
Other files owned by root/root that have the SUID/SGID permissions set represent a security vulnerability on your system.

**A file that has the SGID permissions set**  
-rw-r-Sr-x

##### Search for Files on your Linux System that have SUID Permissions Set
```bash
find / -type f -perm -u=s -ls
```

##### Search for Files on your Linux system that have the SGID Permissions Set**
```bash
find / -type f -perm -g=s -ls
```
