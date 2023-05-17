##### Create Network
```bash
docker network create --subnet=172.16.0.0/24 --gateway=172.16.0.1 my-network
```

##### List all Docker images on your system
```bash
docker images
```

##### Remove a Docker image
```bash
docker rmi [docker image]
```

#####  List all Running Docker container
```bash
docker ps
```

##### Stop a running Docker container
```bash
docker stop [docker container]
```

##### Remove a Docker container
```bash
docker rm [docker container]
```

##### Build a Docker image from a Dockerfile
```bash
docker build -t [myapp] .
```

##### Use to run a command inside a running container
```bash
docker exec
```
##### Example
##### Use to run an Interactive Terminal to run a command inside a running container
```bash
docker exec -it [my container] bash
```

##### Start a set of services defined in a Docker Compose file
```bash
docker compose up
```

##### Start the services defined in the docker-compose.yml file in detached mode
```bash
docker compose up -d
```

##### Stop the services defined in the docker-compose.yml file
```bash
docker compose down
```
