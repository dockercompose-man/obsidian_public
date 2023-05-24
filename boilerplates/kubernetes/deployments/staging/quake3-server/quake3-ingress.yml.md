```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: quake3-server
  namespace: default
  annotations:
    # (Optional): Annotations for the Ingress Controller
    # -- ingress class is needed when traefik is not the default
    # kubernetes.io/ingress.class: traefik
    # ---
    # -- entrypoint and tls configurations
    # traefik.ingress.kubernetes.io/router.entrypoints: web, websecure
    # traefik.ingress.kubernetes.io/router.tls: "true"
    # ---
    # -- optional middlewares
    # traefik.ingress.kubernetes.io/router.middlewares:your-middleware@kubernetescrd
    # ---
spec:
  rules:
  - host: "quake3.yourdomain.com"
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: quake3-server
            port:
              number: 27960
              protocol: UDP
  # (Optional) TLS settings
  # tls:
  # - hosts:
  #   - your-hostname.com  # Your hostname
  #   secretName: your-secret  # Your TLS Secret
  # ---
```
