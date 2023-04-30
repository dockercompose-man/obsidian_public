### CRUD commands

##### Create deployment
```bash
kubectl create depolyment [name]
```
##### Example
```bash
kubectl create deployment NAME --image=image [--dry-run] [options]
```
##### Example Nginx Deployment
```bash
kubectl create deployment nginx-depl --image=nginx
```
##### Check if it's running
```bash
kubectl get deployment
```
AND
```bash
kubectl get pods
```

### Replica Set
#### (automatically handled by kubernetes)
```bash
kubectl get replicaset
```
##### will show pod name with prefix of deployment and replica set ID then it's own ID (you will never have to deal with the replicaset directly)
```bash
nginx-depl-7d9447675c-j9j8k
```

##### Edit deployment
```bash
kubectl edit deployment [name]
```

##### Example
```bash
kubectl edit deployment nginx-depl
```
##### We get an Auto-generated configuration file with default values
##### After you make your changes, check that the pod is terminating and the other is running
```bash
kubectl get pod
```

### Create another deployment, MongoDB
```bash
kubectl create deployment mongo-depl --image=mongo
```

```bash
kubectl logs mongo-depl-67f895857c-fkspm
```

```bash
kubectl get pod
```
##### get additional information from Pod
```bash
kubectl describe pod [pod name]
```

##### get out ADDITIONAL information (WIDE)
```bash
kubectl get pod -o wide
```

##### get additional information from Service
```bash
kubectl describe service [service name]
```
##### Example
```bash
kubectl describe service nginx-service
```

### Status that Kubernetes automatically generated
```bash
kubectl get deployment [deployment name] -o yaml
```
##### Example (gives you updated confiruation of your Deployment) **resides in the etcd**
```bash
kubectl get deployment nginx-deployment -o yaml
```
##### If you want to save it into a file
```bash
kubectl get deployment nginx-deployment -o yaml > nginx-deployment-result.yaml
```



##### open an interactive terminal
```bash
kubectl exec -it [pod name] -- bin/bash
```
##### Example (and now we are root user)
```bash
kubectl exec -it mongo-depl-67f895857c-fkspm -- bin/bash 
```

##### Delete deployment
```bash
kubectl delete depolyment [name]
```
##### Example
```bash
kubectl get deployment
```

```bash
kubectl get pod
```

```bash
kubectl delete deployment mongo-depl
```
##### make sure everything is gone
```bash
kubectl get pod
```
AND
```bash
kubectl get replicaset
```

### Configuration Files
##### applying configuration files
```bash
kubectl apply -f [file name]
```
##### Example
```bash
kubectl apply -f nginx-deployment.yaml
```
##### deleting configuration files
```bash
kubectl delete -f [file name]
```

### Status of different K8s components
```bash
kubectl get nodes | pod | services | replicaset | deployment
```

### Debugging pods

##### Log to console
```bash
kubectl logs [pod name]
```
##### example
```bash
kubectl logs mongo-depl-67f895857c-fkspm
```

##### Get Interactive Terminal
```bash
kubectl exec -it [pod name] -- bin/bash
```

##### Get status of node
```bash
kubectl get nodes
```

##### Get status of services
```bash
kubectl get services
```
