```yaml
apiVersion: v1
kind: Secret
metadata:
  name: minecraft-db-secret
type: Opaque
data:
  privateKey: <base64 encoded password>
```
