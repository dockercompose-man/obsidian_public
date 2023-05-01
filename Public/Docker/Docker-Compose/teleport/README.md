#### Create users once Teleport is running
##### run this from your shell to the docker container shell

```bash
docker exec -it teleport tctl users add xcad --roles=editor --logins=root,xcad,user1,user2,user3
```