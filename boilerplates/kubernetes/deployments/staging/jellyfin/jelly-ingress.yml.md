```yaml
apiVersion: traefik.containo.us/v1alpha1
kind: IngressRoute
metadata:
  name: jellyfin
  namespace: default
  annotations:
    kubernetes.io/ingress.class: traefik-external
spec:
  entryPoints:
    - websecure
  routes:
    - match: Host(`www.jelly.domain.com`)
      kind: Rule
      services:
        - name: jellyfin
          port: 8096
    - match: Host(`jelly.domain.com`)
      kind: Rule
      services:
        - name: jellyfin
          port: 8096
      middlewares:
        - name: default-headers
  tls:
    secretName: domain-com-staging-tls
```