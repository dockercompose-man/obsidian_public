```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: jellyfin # Name of the ingress object
  namespace: default # Name of the namespace
spec:
  rules:
  - host: "jelly.orangefarm.ca"  # Your hostname
    http:
      paths:
      # Path-based routing settings:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: jellyfin  # The name of the service
            port:
              number: 8096  # Service Portnumber
  tls:
  - hosts:
    - jelly.yourdomain.com
    secretName: nginx1-ca-secret
```
