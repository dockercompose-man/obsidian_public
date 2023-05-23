```yaml
apiVersion: traefik.containo.us/v1alpha1
kind: IngressRoute
metadata:
  name: quake3-server
  namespace: default
  annotations:
    kubernetes.io/ingress.class: traefik-external
spec:
  entryPoints:
    - websecure
  routes:
    - match: Host(`www.quake3.domain.com`)
      kind: Rule
      services:
        - name: quake3-server
          port: 27960
    - match: Host(`quake3.domain.com`)
      kind: Rule
      services:
        - name: quake3-server
          port: 27960
      middlewares:
        - name: default-headers
  tls:
    secretName: domain-com-staging-tls
```
