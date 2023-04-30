# Install Docker and Docker Compose on Rocky Linux 8/9

#### Install updates and reboot
```bash
sudo dnf update -y
```
THEN
```bash
sudo reboot now
```

#### Configure Docker Repository & Install Docker

##### Before starting docker installation, please make sure podman and buildah are removed from your rocky linux otherwise you will get errors. Run following command to remove them:
```bash
sudo dnf remove podman buildah -y
```

##### After the removal of podman and buildah, configure docker official package repository using the following command:
```bash
sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```

##### Now run following dnf command to install docker:
```bash
sudo dnf install -y docker-ce
```

##### Note: In case you are getting container.io error while installing docker-ce package then run following command:
```bash
sudo dnf install docker-ce --allowerasing -y
```

#### Start and enable docker service
```bash
sudo systemctl start docker
```
THEN
```bash
sudo systemctl enable docker
```

##### To verify the status of docker run:
```bash
sudo systemctl status docker
```

#### Verify Docker Version
```bash
sudo docker version
```

#### Install Docker Compose
```bash
sudo dnf install docker-compose-plugin -y
```

#### Verify Docker Compose Version
```bash
sudo docker compose version
```

##### If you wish to allow local user to mange and run docker commands with sudo, then add the user to docker group using beneath command:
```bash
sudo usermod -aG docker $USER
```
THEN
```bash
newgrp docker
```
