```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: minecraft-server
  namespace: default
  labels:
    app: minecraft-server
spec:
  selector:
    matchLabels:
      app: minecraft-server
  replicas: 2
  template:
    metadata:
      labels:
        app: minecraft-server
    spec:
      containers:
      - name: minecraft-server
        image: itzg/minecraft-server
        resources:
          limits:
            memory: 512Mi
            cpu: "1"
          requests:
            memory: 256Mi
            cpu: "0.5"
        env:
        - name: EULA
          value: "TRUE"
        - name: ENABLE_RCON
          value: "true"
        - name: RCON_PASSWORD
          valueFrom:
            secretKeyRef:
              name: minecraft-rcon-secret
              key: privateKey
        - name: RCON_PORT
          value: "28016"
        - name: REPLACE_ENV_VARIABLES
          value: "TRUE"
        - name: CFG_DB_HOST
          value: "http://rcon:3306"
        - name: CFG_DB_NAME
          value: "minecraft"
        - name: CFG_DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: minecraft-db-secret
              key: privateKey
        ports:
        - containerPort: 25565
      - name: rcon
        image: itzg/rcon
        ports:
        - containerPort: 4326
        - containerPort: 4327
        env:
        - name: RWA_PASSWORD
          valueFrom:
            secretKeyRef:
              name: minecraft-rcon-secret
              key: privateKey
        volumeMounts:
        - mountPath: /mc # The path that your application uses
          name: nfs-k3s-mcdata # Name of the volume
      volumes:
      - name: nfs-k3s-mcdata
        persistentVolumeClaim:
          claimName: nfs-k3s-mcdata
```
