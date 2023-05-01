Turn Server (Voice and Video for XMPP) - https://registry.hub.docker.com/r/coturn/coturn
made my own docker compose via help of chatgpt.. you must create a directory, and inside create cert and conf directories..
place your turnserver.conf inside conf and place your ssl certs in cert named "turn_server_cert.pem"
in the turnserver.conf I used localhost as an ip and relay, plus for the ssl keys, use the container address, not your local machine.. example
/etc/turnserver/cert/turn_server_cert.pem
/etc/turnserver/cert/turn_server_pkey.pem