```yaml
- nfs-utils
- hosts: master
  become: yes
  tasks:
  - name: Install Samba and NFS Tools / multiple packages using dnf (MASTER/ORACLE9)
    dnf:
      name:
        - samba
        - samba-client
        - samba-common-tools
        - cifs-utils
        - nfs-utils
      state: present

- hosts: crashoverride
  become: yes
  tasks:
  - name: Install Samba and NFS Tools / multiple packages using dnf (CRASHOVERRIDE/ROCKY9)
    dnf:
      name:
        - samba
        - samba-client
        - samba-common-tools
        - cifs-utils
        - nfs-utils
      state: present

- hosts: acidburn
  become: yes
  tasks:
  - name: Install Samba and NFS Tools / multiple packages using apt (ACIDBURN/DEBIAN11)
    apt:
      name:
        - samba
        - smbclient
        - samba-common
        - cifs-utils
        - nfs-common
        - nfs-kernel-server
      state: present

- hosts: cerealkiller
  become: yes
  tasks:
  - name: Install Samba and NFS Tools / multiple packages using apt (CEREALKILLER/DEBIAN11)
    apt:
      name:
        - samba
        - smbclient
        - samba-common
        - cifs-utils
        - nfs-common
        - nfs-kernel-server
      state: present
```
