```yaml
apiVersion: v1
kind: Service
metadata:
  name: navidrome
  namespace: default
spec:
  selector:
    app: navidrome
  ports:
  - name: http
    targetPort: 4533
    port: 4533
```