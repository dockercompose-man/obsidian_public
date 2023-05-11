```yaml
version: '3.7'

services:
  server:
    image: sarasmiseth/prosody:latest
    restart: unless-stopped
    ports:
      - "5000:5000"
      - "5222:5222"
      - "5223:5223"
      - "5269:5269"
      - "5281:5281"
    environment:
      DOMAIN: "orangefarm.ca"
      ALLOW_REGISTRATION: true
      DOMAIN_HTTP_UPLOAD: "upload.yourdomain.ca"
      DOMAIN_MUC: "xmpp.yourdomain.ca"
      DOMAIN_PROXY: "proxy.yourdomain.ca"
      DOMAIN_PUBSUB: "pubsub.yourdomain.ca"
      E2E_POLICY_CHAT: "required"
      E2E_POLICY_MUC: "optional"
      E2E_POLICY_WHITELIST: ""
      DB_DRIVER: SQLite3
      DB_DATABASE: prosody.sqlite
#      LOG_LEVEL: INFO
      C2S_REQUIRE_ENCRYPTION: true
      S2S_REQUIRE_ENCRYPTION: true
      S2S_SECURE_AUTH: true
      SERVER_CONTACT_INFO_ABUSE: "xmpp:mike@.ca, xmpp:james@.ca"
      SERVER_CONTACT_INFO_ADMIN: "xmpp:mike@.ca, xmpp:james@.ca"
      SERVER_CONTACT_INFO_FEEDBACK: "xmpp:mike@.ca, xmpp:james@.ca"
      SERVER_CONTACT_INFO_SALES: "xmpp:mike@.ca, xmpp:james@.ca"
      SERVER_CONTACT_INFO_SECURITY: "xmpp:mike@.ca, xmpp:james@.ca"
      SERVER_CONTACT_INFO_SUPPORT: "xmpp:mike@.ca, xmpp:james@.ca"
      PROSODY_ADMINS: "xmpp:mike@.ca, xmpp:james@.ca"

    volumes:
      - ./certs:/usr/local/etc/prosody/certs
      - ./data:/usr/local/var/lib/prosody
```
