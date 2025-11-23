# What Is Kubernetes
kubernets is a opensource container orchisrtration platform designed to automate 
deployment,scaling and managment of containerised applications
## kubernetes clusters
1) Kubeadm  
2) Minikube(local/ec2)
3) KIND cluster
4) EKS/AKS/GKE
#### Command for connect your local system (kubectl) to an EKS (Elastic Kubernetes Service) cluster in AWS.
```sh
aws eks update-kubeconfig --region <Region-Name> --name <Cluster-Name>
```
## What is Pod in  k8s
- pod is a smallest deplyoable unit in kubernetes
- it act as a wrapper around one or more containers that must run togather
- all containers in pod shares same network (ip address),storage volume and lifecycle

## Pod YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ganesh-pod
spec:
  containers:
  - name: my-cont1
    image: nginx
    ports:
    - containerPort: 80
```
## ▶ How to Apply Pod
```sh
kubectl apply -f pod.yaml
```
## ▶ Check Pod Status
```sh
kubectl get pods
kubectl get poess
```
## ▶ View Pod Logs
```sh
kubectl log my-pod
```
## What is Service 
- A service in kubernetes is an object that provides a stable ip Address , DNS Name and LoadBalancing to access a group of pods
- A service in kubernetes is used is used to expose and provide stable networking to pods
 ### Types of Services
 #### 1) cluster ip (default) 
         - Expose the service inside the cluster only
         - Not accessible from outside
         - Used for internel communication
 #### 2) Node port
         - Node port expose the application outside the cluster through a port on the Node
 #### 3) LoadBalancer
         - Provides external access using cloud provider LoadBalancer 
         - it provide DNS
         - it will distribute trafic over multiple node

####  4) External Name 
         - Externel Service is used to access to access externel DNS based services
####  5) Headless Service
         - Headless service is used when application need direct pod to pod communication 
## Service YAML example
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort # to change service type make changes only in (type:LoadBalancer)
  ports:
  - name : http
    protocol: TCP
    port: 80

```
## ▶ How to Apply Service
```sh
kubectl apply -f service.yaml
```
## ▶ How To Check Service
```sh
kubectl get service
kubectl get svc
```

## What Is NameSpace 
 A NameSpace In kubernetes is way to divide a cluster into small virtual groups so the resources can be orginised and managed saperately
 #### Initial Namespaces
     1) default
     2) kube-node-lease
     3) kube-public
     4) kubesystem
## Namspace YAML Example
```
apiVersion: v1
kind: Namespace
metadata:
  name: ganesh-namespace
  labels:
    name: devops
```
## ▶ How to Apply Namespace
```sh
kubectl apply -f ns.yaml
```
## ▶ How To Check namespace
```sh
kubectl get namespace
kubectl get ns
```
## What is Deployement
   - a deployement is a kubernetes object that manages pods it maintain the desired number od pod replicas and allow easy updates,rollback,and scaling
   - uses replicaset internally
   - support rolling updates
   - Easy Rollback
### Deployment strategies 
1) Rolling Update
   - updates the pod one by one with zero downtime
2) Receate
   - all pods are deleted first then new pods are create
3) Blue-green
   - Run to envirements at the same time Blue=current version Green= new version switches traffic when green is ready
4) canary Deployement
    - a small partiation of users get new version for testing if it is good incress traffic to new version pods
5) progressive delivery
    - combines canary or blue green with manintaning an auto roll back 
6) A/B testing
   - diffrent user groups see diffrent versions to test feature or user behavior
7) Shadow
    - The new versions recives a copy of real traffic but doesnt imapct users
## Deployment YAML Example
```yaml
apiVersion: apps/v1
kind: Deployment
metadata: 
  name: my-deploy
spec:
  replicas: 5
  selector:
    matchLabels:
      app: ganesh
  template:
    metadata:
      name: my-pod12
      labels:
        app: ganesh
    spec:
      containers:
      - name : my-cont1
        image: httpd
        ports:
        - containerPort: 8080
 ```
## ▶ How to Apply Deployement
```sh
kubectl apply -f deplyment.yaml
```
## ▶ How To Check Deployement
```sh
kubectl get deployment
kubectl get deploy
```
## coomand to scale up and scale down pods
```sh
kubectl scale deployment/<deployment name> -- replicas=5
```
## command to change the image in deployment file
```sh
kubectl set image deployment <deployment name> <container name>=image
```
## What is Replietcaset
 - replicaset keeps the desired number of pods running but does not manage updates
 - it maintain pod count
 - No update or roll back feature
 - used internaly by deployments
## ReplicaSet YAML Example 
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-ganesh
spec:
  replicas: 4
  selector:
    matchLabels:
      app: ganeshsm
  template:
    metadata:
      name: ganesh-pod
      labels:
        app: ganeshsm
    spec:
      containers:
      - name: my-cont
        image: httpd
        ports:
        - containerPort: 80
```
##  ▶ How to Apply ReplicaSet
      ```sh
      kubectl apply -f rs.yaml
      ```
##  ▶ How To Check ReplicaSet
      ```sh
      kubectl get replicaset
      kubectl get rs
      
      
