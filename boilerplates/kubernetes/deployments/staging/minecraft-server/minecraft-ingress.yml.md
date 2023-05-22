```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: minecraft-server # Name of the ingress object
  namespace: default # Name of the namespace
spec:
  rules:
  - host: "mc.yourdomain.com"  # Your hostname
    http:
      paths:
      # Path-based routing settings:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: minecraft-server  # The name of the service
            port:
              number: 25565  # Service Portnumber
  tls:
    - hosts:
        - mc.yourdomain.com
      secretName: yourdomain-com-staging-tls
```
