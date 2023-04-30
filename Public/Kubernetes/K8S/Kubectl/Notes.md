Pod is the smallest unit
BUT, you are creating...
Deployment - abstraction over Pods

### Main Kubernetes Components

1. Abstraction of containers (POD)
2. Communication (SERVICE)
3. Route traffic into cluster (INGRESS)
4. External configuration (ConfigMap) & (SECRETS)
5. Data persistence (VOLUMES)
6. Pod blueprints (DEPLOYMENT / StatefulSet) ##stateful for databases


### Deployments

1. Blueprint for creating the pods
2. Most basic configuration for deployment (name and image to use)
3. Rest defaults

### Layers of Abstraction
1. Deployment manages a ...
2. ReplicaSet manages a...
3. Pod is an abstraction of...
4. Container (Docker, ect)

#### Everything BELOW Deployment is handled by Kubernetes

### YAML Configuration File in Kubernetes

#### Overview
1. The 3 parts of configuration file
2. Connecting Deployments to Service to Pods
3. Demo

### YAML Configuration 3 Parts

##### 2 configuration files (Deployment and Service)
##### nginx-deployment.yaml and nginx-service.yaml

##### NOTE: you have to look up the api version for your specific deployment

1. metadata (metadata)
2. specification (spec) **Attributes of "spec" are specific to the kind! (Deployment and Service)
3. status (Automatically generated and added by Kubernetes!)

### Status
##### Will always compared what is the Desired state or what is the Actual state (Self Healing)
##### Will update it's state automatically

##### Where does K8s get the status? Answer: etcd

##### Usual practice is to store the YAML config files with your code (Infrastructure as a code) or a Git repo for the files

### Template
1. has it's own "metadata" and "spec" section
2. applies to Pod
3. blueprint for a pod
4. port, name, image

### Connecting components (Labels & Selectors & Ports)

The way the connection is made is by using Labels and Connectors

##### metadata contains the labels
##### spec contains selectors

### Connecting Deployment to Pods

Keyvalue pair: nginx

1. Pods get the label through the template blueprint
2. This label is matched by the selector

### Connecting Services to Deployments

Selector on the Service must match the metadata's label from Deployment in our case nginx.

### Ports in Service and Pod

The Service ports targetPort should match the Deployments template containerPort

### Endpoints

MUST be the ip address of the right pods

##### get out ADDITIONAL information (WIDE)
```bash
kubectl get pod -o wide
```


where the connection actually is going

