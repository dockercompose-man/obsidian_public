```yaml
apiVersion: v1
kind: Service
metadata:
  name: minecraft-server
  labels:
    app: minecraft-server
spec:
  type: LoadBalancer
  ports:
  - port: 25565
    targetPort: 25565
    protocol: TCP
    name: http
  selector:
    app: minecraft-server
```