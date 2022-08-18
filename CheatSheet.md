# Cheatsheet

## Concepts
  - A Kubernetes **Pod** is a group of one or more Containers, tied together for the purposes of administration and networking. The containers inside the 
  pod share storage, ip address 
  - A Kubernetes Deployment checks on the health of your Pod and restarts the Pod's Container if it terminates. 
  - Service a logical set of pods that have external connectivity. Services match a set of Pods using labels and selectors. You can specify four different ways to expose a pod:
  
  
        - ClusterIP. You can only reach the cluster from inside the cluster (default).
        - NodePort. Exposes the Service on the same port of each selected Node in the cluster using NAT.
        - LoadBalancer. Creates an external load balancer in the current cloud (if supported) and assigns a fixed, external IP to the Service. 
        - ExternalName. Maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value.
        
  - The Control Plane coordinates the cluster
  - Nodes are the workers that run applications (vm or an actual computer). If a node dies so do the pods.
  - Kubelet, a process responsible for communication between the Kubernetes control plane and the Node; it manages the Pods and the containers running on a machine.
  - Clusters: group of nodes controlled by the control panel
  - ReplicaSet: A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.
  - Labels are key/value pairs that are attached to objects, such as pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system
  - Scaling is accomplished by changing the number of replicas in a Deployment
  
  

## Commands

### General options and commands
  - with -l you can specify the label, ex. get pods -l app=foo
  - with -n you can specify the namespace, ex -n development

### Deployments
  - Create deployment with a pod from a single docker image: kubectl create deployment hello-node --image=k8s.gcr.io/echoserver:1.4
  - Get deployments: kubectl get deployments (this commands shows the NAME, READY (shows the ratio of CURRENT/DESIRED replicas), UP-TO-DATE (how many replicas))
  are up to date), AVAILABLE and AGE)
  - To connect to your deployment without making a service you can use **kubectl proxy** to set up a proxy that has connectivity to the deployment.
  You can query your application by **curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/**
  
  

### Pods

  - Get pods: kubectl get pods
  - Get detailed info on all pods: kubectl describe pods
  - Get info from a container in a pod: kubectl logs podNAME
  - Execute a command in a container inside a pod: kubectl exec podNAME -- command
  - Get a bash from a container inside a pod: kubectl exec -ti $POD_NAME -- bash
  - Apply a new label to the pod: kubectl label pods $POD_NAME version=v1
  
### Replica sets
  - Get replicas set for a deployment: kubectl get rs
  - Scale replicas for a given deployment: kubectl scale deployments/kubernetes-bootcamp --replicas=4
  - 

### Services
  - Expose deployment (open ports) and create service: kubectl expose deployment hello-node --type=LoadBalancer --port=8080
  - Delete services: kubectl delete service -l app=kubernetes-bootcamp
  - Get services: kubectl get services
  
## Nodes
  - get nodes: kubectl get nodes
  
  
## Clusters
  - Check cluster info: kubectl cluster-info
  - 
  
### Add ons

  - List add ons: minikube addons list
  - Enable an add on: minikube addons enable metrics-server
  
## MISC

  - Get the name of a pod export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
  - 
