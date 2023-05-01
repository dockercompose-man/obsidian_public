#### **Administering Disk Quotas**
##### Check if it’s installed rpm -qi quota
```bash
rpm -qi quota
```
OR
```bash
apt install quota
```
OR
```bash
dnf install quota
```
OR
```bash
yum install quota
```

Open **/etc/fstab** file in a text editor. **Add** **usrquota** and **grpquota** parameters to the **mount** **options** for the **file** **system** you want to estabilsh quotas on. Save your changes and restart the system for changes to take effect.

#### Create Quota Files
```bash
quotacheck -amvug
```

**-a** - checks **all** **mounted** file systems
**-m** - forces checks on **mounted** file systems
**-u** - checks **users**
**-g** - checks **groups**
**-v** - operates in **verbose** mode

##### two files named **aquota.user** and **aquota.group** should have been **created** in the **mount** **point**.

##### Enable Quotas on your file system by entering:
```bash
quotaon -av
```

##### View current disk space used by your users by entering:
```bash
repquota -av
```

##### Create Disk Quotas
```bash
edquota -u username
```

**Soft Quotas** – temporarily can be exceeded
**Hard Quotas** – cannot be exceeded

**Block Quotas** specify how many **blocks** **on** **disk** the user can consume. **Inode quotas** specify how many **files** the **user** **can** **own**.

##### Copy Quotas from one User to Another
```bash
edquota -p source_user destination_user
```

##### Create Disk Quotas for Groups
```bash
edquota -g groupname
```

##### Change the Grace Period
```bash
edquota -t
```

##### Check your New Quotas**
```bash
repquota -av
```
