```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: navidrome # Name of the ingress object
  namespace: default # Name of the namespace
spec:
  rules:
  - host: "music.yourdomain.com"  # Your hostname
    http:
      paths:
      # Path-based routing settings:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: navidrome  # The name of the service
            port:
              number: 4533 # Service Portnumber
  tls:
    - hosts:
        - music.domain.com
      secretName: domain-com-staging-tls
```
