```yaml
apiVersion: v1
kind: Service
metadata:
  name: navidrome
  labels:
    app: navidrome
spec:
  type: ClusterIP
  ports:
  - port: 25565
    targetPort: 25565
    protocol: TCP
    name: http
  selector:
    app: navidrome
```