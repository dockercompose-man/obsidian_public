# Install Docker and Docker Compose on Oracle Linux 9

https://github.com/LianDuanTrain/DoctorEnglishVersion/blob/master/2/2-1Install%20Docker%20on%20Oracle%20Linux%209/MD/2-1%20Install%20Docker%20and%20Docker%20Compose%20on%20Oracle%20Linux%209.md

## Topics

-   Prerequisite
-   Install Docker
-   Configure Docker Run as A Non-root User
-   Install Docker Compose

## Prerequisite

-   OS version - Oracle Linux Server release 9.0
    -   cat /etc/oracle-release

## Install Docker

#### Commands:

```bash
systemctl stop firewalld
```

```bash
sudo systemctl disable firewalld
```

```bash
sudo dnf update -y
```

```bash
sudo dnf remove -y podman buildah
```

```bash
sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```

```bash
sudo dnf install -y docker-ce
```

```bash
sudo systemctl enable docker.service
```

```bash
sudo systemctl start docker.service
```

```bash
sudo systemctl status docker.service
```

### Verify Docker

Commands:

```bash
docker info
```

```bash
docker version
```

## Configure Docker Run as A Non-root User

Commands:

```bash
sudo usermod -aG docker username
```

```bash
echo "username ALL=(ALL) NOPASSWD: /usr/bin/docker" >> /etc/sudoers
```

```bash
echo alias docker='sudo /usr/bin/docker' >> /home/username/.bash_profile
```

### Verify Non-root User Run Docker

Commands:

```bash
source .bash_profile
```

```bash
docker ps
```

```bash
docker run hello-world
```

## Install Docker Compose

Commands:

```bash
sudo dnf install -y docker-compose-plugin
```

### Verify Docker Compose

Commands:

```bash
docker compose version
```
