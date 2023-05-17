```yaml
# yamllint disable rule:comments-indentation
---
###############################################################################
#                           Authelia Configuration                            #
###############################################################################

theme: dark #light/dark
jwt_secret: #any text or number you want to add here to create jwt Token

default_redirection_url: https://google.com/ #where to redirect for a non-existent URL

server:
  host: 0.0.0.0
  port: 9091
  path: ""
  buffers.read: 4096
  buffers.write: 4096
  enable_pprof: false
  enable_expvars: false
  disable_healthcheck: false
  tls:
    key: ""
    certificate: ""

log:
  level: debug

totp:
  issuer: yourdomain.com #your authelia top-level domain
  period: 30
  skew: 1

authentication_backend:
  password_reset:
    disable: false
  refresh_interval: 5m
  file:
    path: /config/users_database.yml #this is where your authorized users are stored
    password:
      algorithm: argon2id
      iterations: 1
      key_length: 32
      salt_length: 16
      memory: 1024
      parallelism: 8

access_control:
  default_policy: deny
  rules:
    ## bypass rule
    - domain:
        - "auth.yourdomain.com" #This should be your authentication URL
      policy: bypass
    - domain: "yourdomain.com" #example domain to protect
      policy: one_factor
    - domain: "subdomain.yourdomain.com" #example subdomain to protect
      policy: one_factor

#    - domain: "sub2.yourdomain.com" #example subdomain to protect
#      policy: one_factor
#    - domain: "*.yourdomain.com" #example to protect all subdomains under top-level domain
#      policy: one_factor
      #add or remove additional subdomains as necessary. currenlty only supports ONE top-level domain
      #any time you add a new subdomain, you will need to restart the Authelia container to recognize the new settings/>
session:
  name: authelia_session
  secret: #any text or number you want to add here to create jwt Token
  expiration: 3600 # 3 hours
  inactivity: 300 # 15 minutes
  domain: yourdomain.com # Should match whatever your root protected domain is

regulation:
  max_retries: 5
  find_time: 10m
  ban_time: 12h

storage:
  local:
    path: "/config/db.sqlite3" #this is your databse. You could use a mysql database if you wanted, but we're going to >  encryption_key: 4Nvk^EJ$zo$V7^p&sJ^b^@xEk4

  ##
  ## MySQL / MariaDB (Storage Provider)
  ##
#   mysql:
#     host: mysql
#     port: 3306
#     database: authelia
#     username: authelia
    ## Password can also be set using a secret: https://www.authelia.com/c/secrets
#     password: 
#     timeout: 5s

notifier:
  disable_startup_check: true #true/false
  smtp:
    username: your@email.com #your email address
    password: YourP@ssW0RD #your email password
    host: smtp.email.com #email smtp server
    port: 587 #email smtp port
    sender: your@email.com
    identifier: localhost
    subject: "[Authelia] {title}" #email subject
    startup_check_address: your@email.com
    disable_require_tls: false
    disable_html_emails: false
    tls:
      skip_verify: false
      minimum_version: TLS1.2
...
```
