##### Update your Linux System
```bash
sudo apt update
```

##### Upgrade your Linux System
```bash
sudo apt upgrade
```

##### Download the official Docker Setup Script
```bash
curl -sSL https://get.docker.com | sh
```

##### Add the user pi to group docker so you don't have to run sudo all the time
```bash
sudo usermod -aG docker pi
```

##### Install Docker Compose
```bash
sudo apt install docker-compose-plugin
```

##### Make sure to logout for groups to apply
```bash
groups
```

##### Run a test image
```bash
docker run hello-world
```

##### Docker Version
```bash
docker version
```

##### Docker Compose version
```bash
docker compose version
```
