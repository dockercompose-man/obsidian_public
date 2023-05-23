```yaml
apiVersion: v1
kind: Service
metadata:
  name: quake3-server
  labels:
    app: quake3-server
spec:
  type: ClusterIP
  ports:
  - port: 27960
    targetPort: 27960
    protocol: UDP
    name: http
  selector:
    app: quake3-server
```
