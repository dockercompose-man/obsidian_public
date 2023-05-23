```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: quake3-server # Name of the ingress object
  namespace: default # Name of the namespace
spec:
  rules:
  - host: "quake3.domain.com"  # Your hostname
    http:
      paths:
      # Path-based routing settings:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: quake3-server  # The name of the service
            port:
              number: 27960 # Service Portnumber
  tls:
    - hosts:
        - quake3.domain.ca
      secretName: yourdomain-com-staging-tls
```
