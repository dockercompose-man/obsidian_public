```yaml
[master]
172.16.16.x
[crashoverride]
172.16.16.x
[acidburn]
172.16.16.x
[cerealkiller]
172.16.16.x

[master:vars]
ansible_ssh_user=
#add once ssh public key has been sent and host checking disabled
ansible_ssh_private_key_file=/home/eugene/.ssh/ansible_id_rsa

#remove once ssh public key has been sent
#ansible_ssh_pass=
#ansible_become_pass=

[crashoverride:vars]
ansible_ssh_user=
#add once ssh public key has been sent and host checking disabled
ansible_ssh_private_key_file=/home/eugene/.ssh/ansible_id_rsa

#remove once ssh public key has been sent
#ansible_ssh_pass=
#ansible_become_pass=

[acidburn:vars]
ansible_ssh_user=
#add once ssh public key has been sent and host checking disabled
ansible_ssh_private_key_file=/home/eugene/.ssh/ansible_id_rsa

#remove once ssh public key has been sent
#ansible_ssh_pass=
#ansible_become_pass=

[cerealkiller:vars]
ansible_ssh_user=
#add once ssh public key has been sent and host checking disabled
ansible_ssh_private_key_file=/home/eugene/.ssh/ansible_id_rsa

#remove once ssh public key has been sent
#ansible_ssh_pass=
#ansible_become_pass=
```