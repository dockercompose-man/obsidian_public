#### **Configuring SSH to use Public Key Authentication**
##Generate RSA or DSA key pairs
```bash
ssh-keygen -t rsa or ssh-keygen -t dsa
```

#### Private Keys will be saved in **~/.ssh/id_rsa** or **~/.ssh_id_dsa**

#### Public Keys will be saved in **~/.ssh/id_rsa.pub** or **~/.ssh/id_dsa.pub**
  
##### Copy Public Key to SSH server (saved to home directory of user)
```bash
scp ~/.ssh/key_name.pub user_name@address_of_ssh_server:filename
```
##### Example
```bash
scp ~/.ssh/key/id_rsa.pub username@remote_server:/home/username/
```

##### Send to a Different Port than 22
```bash
scp -P 3838 /the/source/file username@server.com:/destination/file
```
##### Example
```bash
scp -P 2222 id_rsa.pub pi@192.168.50.209:/home/pi
```

##### Log into the SSH server and append the contents of keyfile to the end of ~/.ssh/authorized_keys
```bash
cat keyfile >> ~/.ssh/authorized_keys
```

##### Eliminate the need to Enter the Passphrase everytime you establish an SSH connection
```bash
ssh-add ~/.ssh/id_rsa or ssh-add ~/.ssh/id_dsa
```

##### You may need to change the permissions of id_rsa.pub
```bash
sudo chmod 600 id_rsa.pub
```
THEN
```bash
ssh-add id_rsa.pub
```
  
##### If the ssh-agent is fucked up.. run this
```bash
eval `ssh-agent -s
```
THEN
```bash
ssh-add
```
