### Portainer Installation
#### Prerequisites

 -   Docker and Docker Compose
 -   Docker Version
 -   Docker compose Version

#### Create Portainer Volume
```bash
docker volume create portainer_stuff
```
THEN
```bash
docker run -d -p 9443:9443 -p 8000:8000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
