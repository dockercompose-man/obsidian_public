```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: quake3-server # Name of the deployment
  namespace: default # Name of the namespace
  labels:
    app: quake3-server # Name of your application
spec:
  selector:
    matchLabels:
      app: quake3-server # Name of your application
  replicas: 2 # Number of replicas
  template:
    metadata:
      labels:
        app: quake3-server # Name of your application
    spec:
      containers:
      # Containers are the individual pieces of your application that you want
      # to run.
      - name: quake3-server # Name of the container
        image: truecharts/quake3 # The image you want to run
        resources:
          limits:
            memory: 512Mi
            cpu: "1"
          requests:
            memory: 256Mi
            cpu: "0.5"
        ports:
        # Ports are the ports that your application uses.
        - containerPort: 27960 # The port that your application uses
          protocol: UDP
        env:
        - name: SERVER_ARGS
          value: "+set fs_game cpma +exec ffa"
        - name: ADMIN_PASSWORD
          valueFrom:
            secretKeyRef:
              name: quake3-secret
              key: privateKey
        volumeMounts:
        # VolumeMounts are the volumes that your application uses.
        - mountPath: /quake3/.q3a/baseq3 # The path that your application uses
          name: nfs-k3s-quake3 # Name of the volume
      volumes:
      # Volumes are the persistent storage that your application uses.
      - name: nfs-k3s-quake3 # Name of the volume
        persistentVolumeClaim:
          claimName: nfs-k3s-quake3 # Name of the persistent volume claim
```
