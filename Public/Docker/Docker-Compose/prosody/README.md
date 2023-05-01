https://github.com/SaraSmiseth/prosody

So.. I recommend getting a 15 year SSL certificate from cloudflare to never have to worry about this.. but, place the ssl certs locally in /certs directory
You have to login to the container's shell with root via portainer or exec command in terminal and edit the prosody.cfg.lua

The following ports are exposed:

    5000: proxy65 port used for file sharing
    5222: c2s port (client to server)
    5223: c2s legacy ssl port (client to server)
    5269: s2s port (server to server)
    5347: XMPP component port
    5280: BOSH / websocket port
    5281: Secure BOSH / websocket port
    ------------------------------------------------------------------------------------
SSL Certs Folder Structure
------------------------------------------------------------------------------------
certs
├── conference.domain.tld
│   ├── fullchain.pem
│   └── privkey.pem
├── proxy.domain.tld
│   ├── fullchain.pem
│   └── privkey.pem
├── upload.domain.tld
│   ├── fullchain.pem
│   └── privkey.pem
└── domain.tld
    ├── fullchain.pem
    └── privkey.pem
------------------------------------------------------------------------------------
sudo chown 999:999 ./certs
sudo chown 999:999 ./data
------------------------------------------------------------------------------------
to install plugins and update them, shell root into the container via portainer or exec
------------------------------------------------------------------------------------
apt update -y (don't actually update)
apt install nano (if you need it)
wget https://raw.githubusercontent.com/SaraSmiseth/prosody/dev/download-prosody-modules.bash
wget https://raw.githubusercontent.com/SaraSmiseth/prosody/dev/docker-prosody-module-install.bash
chmod +x download-prosody-modules.bash
chmod +x docker-prosody-module-install.bash
./download-prosody-modules.bash
./docker-prosody-module-install.bash
------------------------------------------------------------------------------------
Setting up your DNS Records
-----------------------------------------------------------------------------------
A RECORD - yourdomain.com
A RECORD - xmpp.yourdomain.com

CNAME - upload.yourdomain.com (I believe these were all A records before)
CNAME - proxy.yourdomain.com (I believe these were all A records before)

SRV Records
yourdomain.com _xmpps-client yourdomain.com 5222
yourdomain.com _xmpps-server yourdomain.com 5269
yourdomain.com _xmpps-client yourdomain.com 5223