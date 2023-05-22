```yaml
apiVersion: v1
kind: Service
metadata:
  name: minecraft-server
  labels:
    app: minecraft-server
spec:
  type: ClusterIP
  ports:
  - port: 8096
    targetPort: 8096
    protocol: TCP
    name: http
  selector:
    app: jellyfin
```