```yaml
resources:
  - apiVersion: v1
    kind: PersistentVolumeClaim
    name: nfs-k3s-data
    namespace: default
  - apiVersion: v1
    kind: PersistentVolumeClaim
    name: nfs-k3s-movies2
    namespace: default
env:
  ND_LOGLEVEL: error
  ND_MUSICFOLDER: /MUSIC
```
