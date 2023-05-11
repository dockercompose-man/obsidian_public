```bash
[npm-docker]
enabled = true
ignoreip = 127.0.0.1/8 172.16.x.0/24 YOURREALIPADDRESS
action = cloudflare-apiv4
chain = INPUT
logpath = /log/npm/default-host_access.log
          /log/npm/proxy-host-*_access.log
          /log/npm/proxy-host-*_error.log
maxretry = 1
bantime  = -1
findtime = 86400
```

```
------------------------------------------------------------------------------------
Modify the 172.16.x.0/24 to match your network.
```
