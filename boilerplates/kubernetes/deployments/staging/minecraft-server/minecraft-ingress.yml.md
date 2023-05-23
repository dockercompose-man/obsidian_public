```yaml
apiVersion: traefik.containo.us/v1alpha1
kind: IngressRoute
metadata:
  name: minecraft-server
  namespace: default
  annotations:
    kubernetes.io/ingress.class: traefik-external
spec:
  entryPoints:
    - websecure
  routes:
    - match: Host(`www.mc.domain.com`)
      kind: Rule
      services:
        - name: minecraft-server
          port: 25565
    - match: Host(`mc.domain.com`)
      kind: Rule
      services:
        - name: minecraft-server
          port: 25565
      middlewares:
        - name: default-headers
  tls:
    secretName: domain-com-staging-tls
```
