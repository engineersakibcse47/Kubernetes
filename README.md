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

<img width="504" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/144ec77a-a2d0-46cd-8118-603a582e4f7b">

Kubernetes cluster is made up with at least one masternode / control panel and then connected to it couple of worker nodes(mostly known as Nodes), each node has cubelet process running on it and cublet is actually a kubernetes process that makes it possible for cluster to talk to each other to communicate to each other and actually execute some task on those nodes like- running application processes, each worker node has containers of different applications and deployed on it, so worker nodes are where the actual work is happening, so we can say, On Worker nodes your applications are running. 

**Now, question is what is running on masternode?**

Masternode actually runs several kubernetes processes that are absolutely need to run and manage the cluster properly, all such processes are following-

<img width="471" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/da288cb4-61a3-4fe0-9880-49949c700d4f">

API Server: It's also is a container, that actually is the **entry point to the kubernetes cluster** Through this channel different kubernetes clients will talk like-
  
  - UI:  If youre using kubernetes dashboard.
  - API: If you're using scripts and automating technologies.
  - CLI: Command line tools.
So, all of above these will talk to API Server.

<img width="472" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/0c61693b-39c4-401c-85f9-d27111bf80e0">

Controller Manager: Keeps track of whats happening in the cluster, wheather something need to be repair or container died and need to be restarted etc.

<img width="472" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/6a7e0147-8b36-4c30-8887-e944bf7d1462">

Scheduler: Ensures Pods placement. Scheduler decides on which worker Node, new Pod should be scheduled based on worload and the available server resources on each worker node. So, its an intelligent process that decides on which worker node the next Pod should be scheduled.

<img width="472" alt="image" src="https://github.com/engineersakibcse47/Kubernetes/assets/108215990/64dde985-9899-47bb-b8a1-30d09385e4d5">

etcd: Kubernetes backing store.You can recover the whole cluster state using the etcd.

**Virtual Network:**
It's a very important component of kubernetes which help those nodes, worker nodes and masternodes to talk to each other.

In short, Kubernetes Nodes- 
 - Worker Nodes: Higher workload, bacause they are running the applications on inside of it. Usually much bigger 
                 and more resouces because they will be running hundreds of containers inside of them.
 - Master Node: Will be running master process. Its much more important than individual worker nodes because, for example- if we loase a masternode access, you won't be able to access clustser anymore. Keep in mind to backup masternodes anytime(at least 2 masternode preferable).



  

