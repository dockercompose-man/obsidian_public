#### **Symmetric Encryption**
Using the exact same key to encrypt and decrypt messages. Sometimes called secret key encryption. The higher the bits, the better. 128 bits minimum.
Examples of symmetric encryption:
**Triple Data Encryption Standard (3DES)** - 3DES is commonly used by many Linux services. 3DES encrypts data in three stages. It uses either a 112-bit or a 168-bit key.
**Advanced Encryption Standard (AES)** - AES is an improved version of 3DES. It supports 128-bit, 192-bit, and 256-bit keys.
**Blowfish** - Blowfish uses variable key lengths up to 448 bits.

#### **Asymmetric Encryption**
Unlike symmetric encryption, asymmetric encryption uses **two** **keys** instead of one: the **public** **key** and the **private** **key**. Data that has been **encoded** with the **public** **key** can be **decoded** **only** with the **private** **key**. Data that has been **encoded** with the **private** **key** can **only** be **decoded** with the **public** **key**. For this reason, asymmetric encryption is frequently referred to as _**public**_ _**key**_ _**cryptography**_. Rivest Shamir Adleman (**RSA**) and the Digital Signature Algorithm (**DSA**) are examples of cryptographic standards that use asymmetric encryption.

#### A Certificate contains the following information:
The name of the organization
The public key of the organization
The expiration date of the certificate
The certificate’s serial number
The name of the CA that signed the certificate
A digital signature from the CA
  
There are **two types** of **CAs** that you need to be familiar with:
  
**Internal CA** - An internal CA is one that is **maintained** by an **organization** for **internal** **use**. On most Linux distributions, the OpenSSL package is installed automatically and is used to create a CA on your system. This CA is used to create keys and issue certificates for services running on the server. However, this CA is not a _**trusted**_ CA. If other systems connect to a service on your system via secure connection, users on a remote system will be issued a warning in their client software. This message will indicate that the certificate it received was valid but it didn’t come from a trusted CA. That’s because the certificate came from the CA on your own system. For internal communications, this doesn’t represent a serious issue. We trust ourselves. If you’re going to be dealing with external parties, however, an internal CA won’t suffice.

**External CA** - External parties need assurance from a **trusted**, objective **third** **party** that the certificates they are receiving are legitimate and that you are who you say you are. This is done by using an external CA, such as **VeriSign** or **GTECyberTrust**. These organizations perform the same functions as an internal CA. However, they are globally trusted. For example, suppose you were to access a secure website on the Internet using the Firefox web browser. If the site is using an external CA, you won’t be presented with the warning that you see when using your internal CA.

#### **OpenSSH**
**Host Key pair** locations:
**Private Key** - /etc/ssh/ssh_host_key
**Public Key** - /etc/ssh/ssh_host_key.pub

#### **SSH Client stores keys from other systems:**  
1. /etc/ssh/ssh_known_hosts
2. ~/.ssh/known_hosts
  
#### **OpenSSH Version 2**
**Host Key pair** locations:
/**etc/ssh/ssh_host_rsa_key** and **/etc/ssh_ssh_host_dsa_key** files are used along with their associated public keys **instead** of **/etc/ssh/ssh_host_key**
  
**Configuring OpenSSH**
Configuring the server: **/etc/ssh/sshd_config**
Configuring the client: **~/.ssh/ssh_config**

#### **Tunneling Traffic Through SSH**

**How you can use SSH to tunnel POP3 traffic:**
**1.** Make sure the **ssh** client is **installed** on the local system where the e-mail client will run.
**2.** Make sure the **sshd** daemon is installed and **running** on the POP3 server.
**3.** Ensure IP **port** **22** is **open** on the server where sshd is running.
**4.** On the system where sshd is running, switch to **root** and **edit** the **/etc/ssh/sshd_config** file.
**5.** Locate the **AllowTcpForwarding** parameter, **uncomment** it if necessary, and then set it to a value of **yes**.
An example is shown here:
```bash
AllowTcpForwarding yes
```

**6.** **Save** your changes to the **file** and **exit** the editor.
**7.** **Restart** the **sshd** daemon by entering **systemctl restart sshd** at the shell prompt (as root).
**8.** **Switch** to the **client** **system**.

**9.** Create a local ssh tunnel from a local high IP port (in this example, port **2345**) to **port 110** on the **POP3** **server** using the following command (enter the remote user’s password when prompted):
```bash
ssh -f -N -L 2345:pop3_host_address:110 user_name@pop3_host_address
```

The options specified in this command do the following:
**–N and –f -** Tell ssh **not** to **execute** a **command** **remotely** on the server and to **run** **in** the **background** after prompting for the remote user’s password**–L -** Specifies three things:  
The **local** **port** to be used for the client end of the tunnel (in this case, **2345**)

The **hostname** or **IP address** of the remote **POP3** **server**
The **port** on the **remote** **server** that will be used for the server **end** of the **tunnel** (in this case, **110**)
You don’t have to use port 2345. You can use the same port on both ends if desired.  
**10.** With the tunnel established, **configure** the **local** **e-mail** **client** program to retrieve mail from the local system on the **port** you **configured** for the client end of the SSH tunnel. In this example, you would configure it to get mail from the local system’s IP address on port **2345**.

#### **Configuring Evolution to use an SSH tunnel**

##### Test the Tunnel you created
```bash
telnet localhost client_tunnel_port
```
  
#### **Configure Remote X Client WITHOUT encryption**

On the **remote X client**, enter **xhost +**_**X_server_hostname**_. This tells the client to **accept** **connections** from the **X server**.
```bash
xhost +X_server_hostname
```

On the **X server**, enter **DISPLAY=**_**X_client_hostname**_**:0.0** and then enter **export DISPLAY**. This tells the **X server** to **display** its **output** on the **remote** **X client**.
```bash
DISPLAY=X_client_hostname:0.0
```
THEN
```bash
export DISPLAY
```

From the **X client**, use the **ssh client** to access the shell prompt on the X server and then run the graphical application you want displayed on the X client. For example, you could enter **gedit** at the shell prompt to remotely display the gedit text editor. You could also enter **office** at the shell prompt to remotely display the OpenOffice.org suite.
```bash
gedit
```

```bash
office
```

This procedure works, but all the X traffic is transmitted unencrypted. This isn’t good. Instead, you should use SSH to tunnel the X server traffic between the X server and the X client. You can do this using one of the following options:
Use the **–X** option with the ssh client program
Set the **ForwardX11** option to a value of **yes** in the **/etc/ssh/ssh_config** file on the **X** **client** **system**.
Once this is done, you then need to set the **X11Forwarding** option to **yes** in the **/etc/ssh/sshd_config** file on the X server system.

