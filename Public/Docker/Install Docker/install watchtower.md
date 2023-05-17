#### Auto Update Docker Containers

```bash
docker run -d --name watchtower -v /var/run/docker.sock:/var/run/docker.sock --restart unless-stopped containrrr/watchtower --schedule "0 0 4 * * *" --debug --cleanup
```
