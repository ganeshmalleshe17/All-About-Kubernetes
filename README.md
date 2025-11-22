# What Is Kubernetes
kubernets is a opensource container orchisrtration platform designed to automate 
deployment,scaling and managment of containerised applications
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
  type: NodePort #LoadBalancer to change service type make changes only in (type:)
  ports:
  - name : http
    protocol: TCP
    port: 80

```
## ▶ How to Apply Service
```sh
kubectl apply -f service.yaml
```
## ▶ To Check Pod Service
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
       
    
