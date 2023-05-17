### Using GPG to Encrypt Files
##### Generate your Keys, default 2048 bits, up to 4096 bits
```bash
gpg –gen-key
```

##### Set Expiry Date, and Enter User ID
```bash
realname: rtracy
```

##### Set Email
```bash
rtracy rtracy@opensuse
```
**enter a unique passphrase for the key**

#### **Keyfiles are stored in:**
**secring.gpg** – this file is the GPG **secret** **keyring**
**pubring.gpg** – this file is the GPG **public** **keyring**
**trustdb.gpg** – this file is the GPG **trust** **database**
  
##### List gpg keys
```bash
gpg –list-keys
```

**Gpg keyring** is located in **~/.gnupg/** and is named **pubring.gpg**
**Gpg configuration** file is located in **~/.gnupg**
  
##### Export Private Keys
```bash
gpg –export-secret-keys –armor key_owner_email_address > filename.asc
```

```bash
gpg –export-secret-keys –armor rtracy@opensuse rtracy-privatekey.asc
```

##### Export Public Keys
```bash
gpg –export –armor key_owner_email > public_key_filename
```
##### Example
```bash
gpg –export –armor rtracy@opensuse > gpg.pub
```

##### Encrypt a File in your Linux File System
```bash
gpg -e -r key_user_name filename
```
##### Example
```bash
gpg -e -r rtracy mytestfile.txt
```

##Copy your Public Keys to a Public Key Server
```bash
gpg –keyserver hkp://subkeys.pgp.net –send-key key_ID
```

##Show Users key_ID
```bash
gpg –fingerprint key_owner_email
```

```bash
gpg –keyserver hkp://subkeys.pgp.net –send-pkey 9DF54AB2
```

##### Securely Send Keys to Remote Computer on the Local Network
```bash
scp gpg.pub student@fedora
```
  
##### Encrypt a File in your Linux File System
```bash
gpg –output output_filename –symmetric encrypted_filename
```

##### Decrypt a File in your Linux file system
```bash
gpg –output mytestfile.txt.decrypted –decrypt mytestfile.txt.gpg
```

##### Check Fingerprint
```bash
gpg –fingerprint student@fedora
```

#### **Key Revocation Certificate (when your key is comprimised, superseeded or no longer used)**

##### Creating a Key Revocation Certificate **(not issue)**
```bash
gpg –output revoke.asc –gen-revoke key_ID
```

##### To Actually Revoke a Key
```bash
gpg –import revocation_certificate_filename
```

##### Check to make sure it’s been Revoked
```bash
gpg –list-keys key_ID
```

##### Revoke Key from Public KeyServer
```bash
gpg –keyserver public_key_server_URL –send key_ID
```
