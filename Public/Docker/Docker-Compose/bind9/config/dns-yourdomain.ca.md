```bash
$TTL 2d

$ORIGIN yourdomain.com.

@               IN      SOA     ns.yourdomain.com. your.email.com. (
                                2023022400      ; serial
                                12h             ; refresh
                                15m             ; retry
                                3w              ; expire
                                2h              ; minimum ttl
                                )

                IN      NS      ns.yourdomain.com.

ns              IN      A       192.168.*.*

; -- add dns records below

srv-prod-1      IN      A       192.168.*.*
srv-prod-2      IN      A       192.168.*.*

; -- demo servers

srv-demo-2      IN      A       192.168.*.*
*.srv-demo-2    IN      A       192.168.*.*
```

