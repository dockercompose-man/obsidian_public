```yaml
apiVersion: traefik.containo.us/v1alpha1
kind: IngressRoute
metadata:
  name: nginx
  namespace: default
  annotations:
    kubernetes.io/ingress.class: traefik-external
spec:
  entryPoints:
    - websecure
  routes:
    - match: Host(`www.new.domain.com`)
      kind: Rule
      services:
        - name: nginx
          port: 80
    - match: Host(`new.domain.com`)
      kind: Rule
      services:
        - name: nginx
          port: 80
      middlewares:
        - name: default-headers
  tls:
    secretName: domain-com-staging-tls
```