# Install Docker and Docker Compose on Debian 11

#### Update the `apt` package index and install packages to allow `apt` to use a repository over HTTPS:
```bash
sudo apt-get update
```
THEN
```bash
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

#### Add Docker's official GPG key:
```bash
sudo mkdir -m 0755 -p /etc/apt/keyrings
```
THEN
```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

#### Use the following command to set up the repository:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### Install Docker Engine

##### This procedure works for Debian on x86_64 / amd64, armhf, arm64, and Raspbian.

##### Update the apt package index:
```bash
sudo apt-get update
```

##### Receiving a GPG error when running `apt-get update`?
##### Your default [umask](https://en.wikipedia.org/wiki/Umask) may be incorrectly configured, preventing detection of the repository public key file. Try granting read permission for the Docker public key file before updating the package index:

```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
THEN
```bash
sudo apt-get update
```

##### Install Docker Engine, containerd, and Docker Compose.
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### Verify that the Docker Engine installation is successful by running the `hello-world` image:
```bash
sudo docker run hello-world
```
This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits.

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
docker version
```

#### Verify Docker Compose Version
```bash
docker compose version
```

##### If you want to avoid typing `sudo` whenever you run the `docker` command, add your username to the `docker` group:
```bash
sudo usermod -aG docker ${USER}
```

##### Confirm that your user is now added to the **docker** group by typing:
```bash
id -nG
```
