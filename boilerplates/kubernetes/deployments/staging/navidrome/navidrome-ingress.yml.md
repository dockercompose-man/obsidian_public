```yaml
apiVersion: traefik.containo.us/v1alpha1
kind: IngressRoute
metadata:
  name: navidrome
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
        - name: navidrome
          port: 4533
    - match: Host(`music.yourdomain.com`)
      kind: Rule
      services:
        - name: navidrome
          port: 4533
      middlewares:
        - name: default-headers
  tls:
    secretName: yourdomain-com-staging-tls
```
