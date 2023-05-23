```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: navidrome # Name of the deployment
  namespace: default # Name of the namespace
  labels:
    app: navidrome # Name of your application
spec:
  selector:
    matchLabels:
      app: navidrome # Name of your application
  replicas: 1 # Number of replicas
  template:
    metadata:
      labels:
        app: navidrome # Name of your application
    spec:
      containers:
      # Containers are the individual pieces of your application that you want
      # to run.
      - name: navidrome # Name of the container
        image: deluan/navidrome # The image you want to run
        resources:
          limits:
            memory: 512Mi
            cpu: "1"
          requests:
            memory: 256Mi
            cpu: "0.5"
        ports:
        # Ports are the ports that your application uses.
        - containerPort: 4533 # The port that your application uses
        volumeMounts:
        # VolumeMounts are the volumes that your application uses.
        - mountPath: /data # The path that your application uses
          name: nfs-k3s-navidata # Name of the volume
        # VolumeMounts are the volumes that your application uses.
        - mountPath: /music # The path that your application uses
          name: nfs-k3s-movies2 # Name of the volume
      volumes:
      # Volumes are the persistent storage that your application uses.
      - name: nfs-k3s-navidata # Name of the volume
        persistentVolumeClaim:
          claimName: nfs-k3s-navidata # Name of the persistent volume claim
      # Volumes are the persistent storage that your application uses.
      - name: nfs-k3s-movies2 # Name of the volume
        persistentVolumeClaim:
          claimName: nfs-k3s-movies2 # Name of the persistent volume claim
```
