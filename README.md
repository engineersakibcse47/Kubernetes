### Official Defination of Kubernetes

- Open source container orchestation tool.
- Developed by Google.
- Helps mange containerized applications in different deployment environments ( like- physical machine, virtual machine or cloud or hybrid deployment) across different server.

As kubernetes deploy containerized applications and therefore it use specific container runtime. 

Supported container runtime in kubernetes such as- **Docker, CRI-O, Containerd**.


### What features do orchestration tool offer?

- High Availability or no downtime.
- Scalability or high performance.
- Disaster recovery - backup and restore.

### Kubernetes Architecture

<img width="400" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/144ec77a-a2d0-46cd-8118-603a582e4f7b">

Kubernetes cluster is made up with at least one masternode / control panel and then connected to it couple of worker nodes(mostly known as Nodes), each node has cubelet process running on it and cublet is actually a kubernetes process that makes it possible for cluster to talk to each other to communicate to each other and actually execute some task on those nodes like- running application processes, each worker node has containers of different applications and deployed on it, so worker nodes are where the actual work is happening, so we can say, On Worker nodes your applications are running. 

**Now, question is what is running on masternode?**

Masternode actually runs several kubernetes processes that are absolutely need to run and manage the cluster properly, all such processes are following-

<img width="471" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/da288cb4-61a3-4fe0-9880-49949c700d4f">

- API Server: It's also is a container, that actually is the **entry point to the kubernetes cluster** Through this channel different kubernetes clients will talk like-
  
  - UI:  If youre using kubernetes dashboard.
  - API: If you're using scripts and automating technologies.
  - CLI: Command line tools.

So, all of above these will talk to API Server.

<img width="472" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/0c61693b-39c4-401c-85f9-d27111bf80e0">

- Controller Manager: Keeps track of whats happening in the cluster, wheather something need to be repair or container died and need to be restarted etc.

<img width="472" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/6a7e0147-8b36-4c30-8887-e944bf7d1462">

- Scheduler: Ensures Pods placement. Scheduler decides on which worker Node, new Pod should be scheduled based on worload and the available server resources on each worker node. So, its an intelligent process that decides on which worker node the next Pod should be scheduled.

<img width="472" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/64dde985-9899-47bb-b8a1-30d09385e4d5">

- etcd: Etcd holds the current status of any K8s components. From etcd kubernets get status data of components to upate status continously. So, it's a kubernetes backing store. You can recover the whole cluster state using the etcd.
  - Cluster Brain, Key Value Store.

**Virtual Network:**
It's a very important component of kubernetes which help those nodes, worker nodes and masternodes to talk to each other.

In short, Kubernetes Nodes- 

 - Worker Nodes / Node: Higher workload, bacause they are running the applications on inside of it. Usually much bigger 
                 and more resouces because they will be running hundreds of containers inside of them.
 - Master Node: Will be running master process. Its much more important than individual worker nodes because, for example- if we loase a masternode access, you won't be able to access clustser anymore. Keep in mind to backup masternodes                          anytime(at least 2 masternode preferable).

### Kubernetes Components

- POD:
  - Smallest unit in kubernetes, and containers are created inside of the pods(Abstraction over container).
  - Usually 1 application per pod, in exception case multiple containers can work together inside single pod as a helper container of main application container. So, all containers inside single pod- shared volumes and shared ip address. 
  - Each pod gets it's IP address, and they can communicate with each other using that IP address(not public ip, it's an internal ip). 
  - Pods are ephemeral, which means pods can die any time. When new one will created in it's place it will get a new IP-address on recreation which obviously inconvenient because you're have to adjusted every time pods restart, because of that        another component comes in kubernetes world called- **Service**.

<img width="600" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/4fb09f49-dd28-461a-9ea0-cbe797168749">

- Service:
  - It's basically a static or parmanent ip address that belongs to each pod. So, every pod will have it's own service.
  - Lifecyle of Pod and Service not connected, so even if the pod dies the service and ip address will be reamin same, so you don't have to change that anymore.
  - Extrnal Service: App should be accessible through browser, an dexternal services a service that opens the communication from external soources.
  - Internal Service: One thing, definetly you wouldn't want your dtabase to be open to the public requests, and for that you will create something called Internal Service. So, this is a type of service that you specify on creation.  

- Ingress: As an end product usually you want your url to look like this (www.abc.com) not (124.89.101.2:3000), if you want to talk to your application with a secure protocol and domain name and for that another component of kubernetes called               ingress so, insted of **service** request goes first to ingress and it does the forwarding then to the service. 

- ConfigMap: External configuration of your application, so configmap usually contain configuration data like- urls of database or other services that you use and, in kubernetes you just connect it to the pod so that pod actually gets data that               configmap contains, and now if you change the name of the service or the end point of the service (for example- rename database service url) you will just adjust the configmap and thats it. Your don't have to build a new image and                have to go through this whole cycle.

- Secret: ConfigMap is for non-confidential data only!!!! So, for confidential data kubernetes has another component called secret. So, secret is just like ConfigMAp but the difference that-
  
  - It's used to store secret data credentials for example- its store not in a plain text format but in base 64      encoded format and Kubernetes dosen't encrypt them by default for that you can deploy separate third-party       tools deploy on     kubernetes to encrypt your secret. so,just like configmap you connect it to your pod so that     pod can actually read from the secret as environment variables or properties file.

<img width="600" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/32fd60b6-9ddd-442c-b8b2-0de83a343b28">

- Volume: Basically, it attaches a physical storage on a hard drive belogs to pod and that storage could be either on local machine on the same server node where pod running or it could be on a remote storage outside of the K8s cluster which is            not part of the kubernetes cluster. Just imagine storage as an exteral hard drive plugged in into the kubernetes cluster because Kubernetes cluster dosen't manage any data persistance which means you as a kubernetes user or an                    administrator are responsible for backing up the data, replicate and managing it.

<img width="600" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/2d172823-b00d-4835-bcd5-ee0332da609c">
 
-  Deployment: For stateLess applications. Here, you will define blueprint for Pods, specify how many replicas you want to have of that     particular pod and this component or blueprint is called deployment. In practice you would not be working                with pods or you would not be creating pods, you would be creating deployments because there you can specify how many replicas and you can also scale up or down the number of replicas of pods that you need. So, with Pod we said                   that pod is a layer of abstraction on top of containers and deployment is another abstraction on top of pods which makes it ,ore convenient to interact with pods and replicte them and do some other configuration. So, in practice                  you would mostly work with deploymnets not with pods.

- STATEFULSET: Database can't be replicated vai deployment!! beacuse database has state which meaning that if we have cloens or replicas of the database they all needs to access the same shared data storage and there you would need some kind of                 mechanisam that manages which pods are currently writing to the storage or which pods are reading from the storage in order to avoid data inconsitencies that mechanisam in addition to replicating feature is offered by another                     kubernetes component called STATEFULSET. This component use in specifically for application(STATEFUL apps) like databases. So, MySql, mongoDB or any others stateful applications or databases should be cretaed using STATEFULSET not                Deployment.
  - Deploying Statefulset applications not easy. A common practice, database are often hosted outside of kubernetes cluster and just have the deployments or stateless applications that replicate and scale with no problem inside of the kubernetes     cluster and communicate with external databases. 

### Main Kubernetes Components summarized

<img width="500" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/fa0ccde2-5a0a-4066-b408-83f43da2596b">

<img width="500" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/8bafba76-9536-4e21-87d5-532e5ff69cd7">

<img width="500" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/fdc7e961-314b-4b8e-9ea8-9fd98f055fed">

<img width="500" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/63998321-4785-4c18-aeac-add3b9c87cad">

Just using these components you can actually build pretty powerful K8s Clusters.

### Kubernetes Configuration

Each configuration file has 3 parts, metadata, specification and status. Status generated and added atumatically by kubernetes. 

### What is Minikube?

<img width="600" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/a379feb7-a180-4500-9f4e-db77f48a9b3c">

Basically one node cluster where Master Node and Worker Nodes processes both run on ONE Machine with Docker runtime pre-installed.  

### What is kubectl?

<img width="600" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/e64a02bd-c90b-4aa8-8db3-7e9cb5a217e0">

After setup minikube cluster, you need some way to interact with that cluster so you need a way to create pods and other kubernetes components on the node and the way to do it using kubectl, which is **Command line tool** for K8s Cluster. 

Lets talk, how actaully it works, as we know minikube runs master and work node process, so one of the master node process called **API Server** is actually the main entrypoint into the kubernetes cluster, so if you want to do anything inside cluster you first have to talk to the API Server and way to talk to the API Server is through different clients like- UI, API, CLI etc. KUBECTL(CLI) is the most powerful of 3 clients. 

### Main Kubectl Commands - K8s CLI

### install hyperhit and minikube
`brew update`

`brew install hyperkit`

`brew install minikube`

`kubectl`

`minikube`

### create minikube cluster
`minikube start --vm-driver=hyperkit`

`kubectl get nodes`

`minikube status`

`kubectl version`

### delete cluster and restart in debug mode
`minikube delete`

`minikube start --vm-driver=hyperkit --v=7 --alsologtostderr`

`minikube status`

### kubectl commands
`kubectl get nodes`

`kubectl get pod`

`kubectl get services`

`kubectl create deployment nginx-depl --image=nginx`

`kubectl get deployment`

`kubectl get replicaset`

`kubectl edit deployment nginx-depl`

### debugging
`kubectl logs {pod-name}`

`kubectl exec -it {pod-name} -- bin/bash`

### create mongo deployment
`kubectl create deployment mongo-depl --image=mongo`

`kubectl logs mongo-depl-{pod-name}`

`kubectl describe pod mongo-depl-{pod-name}`

### delete deplyoment
`kubectl delete deployment mongo-depl`

`kubectl delete deployment nginx-depl`

### create or edit config file
`vim nginx-deployment.yaml`

`kubectl apply -f nginx-deployment.yaml`

`kubectl get pod`

`kubectl get deployment`

### delete with config
`kubectl delete -f nginx-deployment.yaml`

#Metrics

`kubectl top` The kubectl top command returns current CPU and memory usage for a cluster’s pods or nodes, or for a particular pod or node if specified.







The End!!!!




























