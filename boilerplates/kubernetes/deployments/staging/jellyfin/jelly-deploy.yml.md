```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: jellyfin # Name of the deployment
  namespace: default # Name of the namespace
  labels:
    app: jellyfin # Name of your application
spec:
  selector:
    matchLabels:
      app: jellyfin # Name of your application
  replicas: 1 # Number of replicas
  template:
    metadata:
      labels:
        app: jellyfin # Name of your application
    spec:
      containers:
      # Containers are the individual pieces of your application that you want
      # to run.
      - name: jellyfin # Name of the container
        image: jellyfin/jellyfin # The image you want to run
        resources:
          limits:
            memory: 2048Mi
            cpu: "1"
          requests:
            memory: 1024Mi
            cpu: "1"
        ports:
        # Ports are the ports that your application uses.
        - containerPort: 8096 # The port that your application uses
        volumeMounts:
        # VolumeMounts are the volumes that your application uses.
        - mountPath: /config # The path that your application uses
          name: nfs-k3s-jellydata # Name of the volume
        - mountPath: /cache # The path that your application uses
          name: nfs-k3s-jellydata # Name of the volume
        - mountPath: /transcode # The path that your application uses
          name: nfs-k3s-jellydata # Name of the volume
        - mountPath: /jellyfin-web # The path that your application uses
          name: nfs-k3s-jellydata # Name of the volume
        - mountPath: /jellyfin1 # The path that your application uses
          name: nfs-k3s-movies1 # Name of the volume
        - mountPath: /jellyfin2 # The path that your application uses
          name: nfs-k3s-movies2 # Name of the volume
      volumes:
      # Volumes are the persistent storage that your application uses.
      - name: nfs-k3s-jellydata # Name of the volume
        persistentVolumeClaim:
          claimName: nfs-k3s-jellydata # Name of the persistent volume claim
      - name: nfs-k3s-movies1 # Name of the volume
        persistentVolumeClaim:
          claimName: nfs-k3s-movies1 # Name of the persistent volume claim
      - name: nfs-k3s-movies2 # Name of the volume
        persistentVolumeClaim:
          claimName: nfs-k3s-movies2 # Name of the persistent volume claim
```
