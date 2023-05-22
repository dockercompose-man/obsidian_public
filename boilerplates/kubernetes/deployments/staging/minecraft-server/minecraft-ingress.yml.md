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
    - match: Host(`www.your.domain.com`)
      kind: Rule
      services:
        - name: minecraft-server
          port: 25565
    - match: Host(`music.yourdomain.com`)
      kind: Rule
      services:
        - name: minecraft-server
          port: 25565
      middlewares:
        - name: default-headers
  tls:
    secretName: yourdomain-com-staging-tls
```
