
### A Sample Teleport configuration file.
### Things to update:
###  1. license.pem: You only need a license from https://dashboard.goteleport.com
### if you are an Enterprise customer.


```yaml
version: v2
teleport:
  nodename: teleport.orangefarm.ca
  data_dir: /var/lib/teleport
  log:
    output: stderr
    severity: INFO
    format:
      output: text
  ca_pin: ""
  diag_addr: ""
auth_service:
  enabled: "yes"
  listen_addr: 0.0.0.0:3025
  proxy_listener_mode: multiplex
  cluster_name: teleport.domain.ca
  authentication:
    type: local
    second_factor: on
    webauthn:
      rp_id: teleport.orangefarm.ca
    connector_name: passwordless
ssh_service:
  enabled: "yes"
  commands:
  - name: hostname
    command: [hostname]
    period: 1m0s
proxy_service:
  enabled: "yes"
  web_listen_addr: 0.0.0.0:443
  public_addr: teleport.domain.ca
  https_keypairs: []
  acme:
    enabled: "yes"
    email: "your@email.com"
```
