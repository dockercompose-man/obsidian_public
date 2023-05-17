```yaml
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8880:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  jenkins/jenkins
```

```yaml
version: '3'

services:
  jenkins:
    image: jenkins/jenkins
    container_name: jenkins-blueocean
    restart: on-failure
    environment:
      DOCKER_HOST: tcp://docker:2376
      DOCKER_CERT_PATH: /certs/client
      DOCKER_TLS_VERIFY: 1
    ports:
      - "8880:8080"
      - "50000:50000"
    volumes:
      - /portainer/Files/AppData/Config/jenkins/jenkins-data:/var/jenkins_home
      - /portainer/Files/AppData/Config/jenkins/jenkins-docker-certs:/certs/client:ro
    networks:
      - jenkins

networks:
  jenkins:

volumes:
  jenkins-data:
  jenkins-docker-certs:
```
