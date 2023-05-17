```bash
acl internal {
    192.168.0.0/24;
    192.168.50.0/24;
};

options {
    forwarders {
        8.8.8.8;
        or adguard/pihole;
    };
    allow-query { internal; };
};

zone "yourdomain.com" IN {
    type master;
    file "/etc/bind/dns-yourdomain.com";
};
```

