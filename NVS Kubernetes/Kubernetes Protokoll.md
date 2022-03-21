---
title: NVS Kubernetes Protocol
author: Niklas Haiden - 5BHIF
date: 16.02.2022
tableofcontent: true
titlepage: true
titlepage-text-color: "000000"
logo: "logo.png"
logo-width: 100mm
toc-own-page: true
listings-disable-line-numbers: true
---
# Theory 
https://en.wikipedia.org/wiki/Kubernetes

 ## Kubernetes
 
 ### General 
 
 Kubernetes (/ˌk(j)uːbərˈnɛtɪs, -ˈneɪtɪs, -ˈneɪtiːz, -ˈnɛtiːz/, commonly stylized as K8s) is an open-source container orchestration system for automating software deployment, scaling, and management. Google originally designed Kubernetes, but the Cloud Native Computing Foundation now maintains the project.

Kubernetes works with Docker, Containerd, and CRI-O. Originally, it interfaced exclusively with the Docker runtime through a "Dockershim"; however, since 2016, Kubernetes has deprecated the shim in favor of directly interfacing with the container through Containerd, or replacing Docker with a runtime that is compliant with the Container Runtime Interface (CRI).

Amazon, Google, IBM, Microsoft, Oracle, Red Hat and VMware offer Kubernetes-based platforms or infrastructure as a service (IaaS) that deploy Kubernetes.

 ### History 
 
 Kubernetes (κυβερνήτης, Greek for "helmsman," "pilot," or "governor", and the etymological root of cybernetics) was first announced by Google in mid-2014. Ville Aikas, Joe Beda, Brendan Burns, and Craig McLuckie were the initial founders of Kubernetes, but other Google engineers, including Brian Grant and Tim Hockin, joined them shortly thereafter. Google's Borg system had a significant influence on the design and development of Kubernetes. Many of the top contributors to the project previously worked on Borg. The original codename for Kubernetes within Google was Project 7, a reference to the Star Trek ex-Borg character Seven of Nine. The seven spokes on the wheel of the Kubernetes logo are a reference to that codename. The original Borg project was entirely in C++, but Kubernetes source code is in the Go language.

Kubernetes 1.0 was released on July 21, 2015, along which Google partnered with the Linux Foundation to form the Cloud Native Computing Foundation (CNCF) and offered Kubernetes as a seed technology. In February 2016, the Helm package manager for Kubernetes was released. On March 6, 2018, Kubernetes Project reached the ninth place in the list of GitHub projects by the number of commits, and second place in authors and issues, after the Linux kernel.

Until version 1.18, Kubernetes followed an N-2 support policy, meaning that the three most recent minor versions receive security updates and bug fixes. Starting with version 1.19, Kubernetes follows an N-3 support policy.

 ### Concepts
 
 Kubernetes defines a set of building blocks ("primitives") that collectively provide mechanisms that deploy, maintain, and scale applications based on CPU, memory or custom metrics. Kubernetes is loosely coupled and extensible to meet different workloads. The internal components as well as extensions and containers that run on Kubernetes rely on the Kubernetes API. The platform exerts its control over compute and storage resources by defining resources as Objects, which can then be managed as such.

Kubernetes follows the primary/replica architecture. The components of Kubernetes can be divided into those that manage an individual node and those that are part of the control plane.

#### Control plane

The Kubernetes master is the main controlling unit of the cluster, managing its workload and directing communication across the system. The Kubernetes control plane consists of various components, each its own process, that can run both on a single master node or on multiple masters supporting high-availability clusters. The various components of the Kubernetes control plane are as follows:

etcd[31] is a persistent, lightweight, distributed, key-value data store that CoreOS has developed. It reliably stores the configuration data of the cluster, representing the overall state of the cluster at any given point of time. etcd favors consistency over availability in the event of a network partition (see CAP theorem). The consistency is crucial for correctly scheduling and operating services.
The API server serves the Kubernetes API using JSON over HTTP, which provides both the internal and external interface to Kubernetes. The API server processes and validates REST requests and updates the state of the API objects in etcd, thereby allowing clients to configure workloads and containers across worker nodes. The API server uses etcd's watch API to monitor the cluster, roll out critical configuration changes, or restore any divergences of the state of the cluster back to what the deployer declared. As an example, the deployer may specify that three instances of a particular "pod" (see below) need to be running. etcd stores this fact. If it is found that only two instances are running, this delta will be detected by comparison with etcd data, and Kubernetes will use this to schedule the creation of an additional instance of that pod.
The scheduler is the extensible component that selects on which node an unscheduled pod (the basic entity managed by the scheduler) runs, based on resource availability. The scheduler tracks resource use on each node to ensure that workload is not scheduled in excess of available resources. For this purpose, the scheduler must know the resource requirements, resource availability, and other user-provided constraints or policy directives such as quality-of-service, affinity vs. anti-affinity requirements, and data locality. The scheduler's role is to match resource "supply" to workload "demand".
A controller is a reconciliation loop that drives the actual cluster state toward the desired state, communicating with the API server to create, update, and delete the resources it manages (e.g., pods or service endpoints). One kind of controller is a Replication Controller, which handles replication and scaling by running a specified number of copies of a pod across the cluster. It also handles creating replacement pods if the underlying node fails. Other controllers that are part of the core Kubernetes system include a DaemonSet Controller for running exactly one pod on every machine (or some subset of machines), and a Job Controller for running pods that run to completion, e.g. as part of a batch job. Labels selectors that are part of the controller's definition specify the set of pods that a controller manages.
The controller manager is a process that manages a set of core Kubernetes controllers.

### Nodes

A node, also known as a worker or a minion, is a machine where containers (workloads) are deployed. Every node in the cluster must run a container runtime such as Docker, as well as the below-mentioned components, for communication with the primary for network configuration of these containers.

- Kubelet is responsible for the running state of each node, ensuring that all containers on the node are healthy. It takes care of starting, stopping, and maintaining application containers organized into pods as directed by the control plane. Kubelet monitors the state of a pod, and if not in the desired state, the pod re-deploys to the same node. Node status is relayed every few seconds via heartbeat messages to the primary. Once the primary detects a node failure, the Replication Controller observes this state change and launches pods on other healthy nodes.

- Kube-proxy is an implementation of a network proxy and a load balancer, and it supports the service abstraction along with other networking operation. It is responsible for routing traffic to the appropriate container based on IP and port number of the incoming request.
- A container resides inside a pod. The container is the lowest level of a micro-service, which holds the running application, libraries, and their dependencies. Containers can be exposed to the world through an external IP address. Kubernetes has supported Docker containers since its first version. In July 2016 the rkt container engine was added.

#### Namespaces

Kubernetes provides a partitioning of the resources it manages into non-overlapping sets called namespaces. They are intended for use in environments with many users spread across multiple teams, or projects, or even separating environments like development, test, and production.

#### Pods

The basic scheduling unit in Kubernetes is a pod, which consists of one or more containers that are guaranteed to be co-located on the same node. Each pod in Kubernetes is assigned a unique IP address within the cluster, allowing applications to use ports without the risk of conflict. Within the pod, all containers can reference each other. However, for a container within one pod to access another container within another pod, it has to use the pod IP address. Pod IP addresses are ephemeral, though. An application developer should never use hardcoded pod IP addresses because the specific pod that they are referencing may be assigned to another pod IP address on restart. Instead, they should use a reference to a service (see below), which holds a reference to the target pod at the specific pod IP address.

A pod can define a volume, such as a local disk directory or a network disk, and expose it to the containers in the pod. Pods can be managed manually through the Kubernetes API, or their management can be delegated to a controller. Such volumes are also the basis for the Kubernetes features of ConfigMaps (to provide access to configuration through the file system visible to the container) and Secrets (to provide access to credentials needed to access remote resources securely, by providing those credentials on the file system visible only to authorized containers).

##### DaemonSets

Normally, the Kubernetes Scheduler decides where to run pods. For some use cases, though, there could be a need to run a pod on every single node in the cluster. This is useful for use cases like log collection, ingress controllers, and storage services. DaemonSets implement this kind of pod scheduling.

##### ReplicaSets

A ReplicaSet’s purpose is to maintain a stable set of replica pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

The ReplicaSets can also be said to be a grouping mechanism that lets Kubernetes maintain the number of instances that have been declared for a given pod. The definition of a ReplicaSet uses a selector, whose evaluation will result in identifying all pods that are associated with it.

#### Services

A Kubernetes service is a set of pods that work together, such as one tier of a multi-tier application. The set of pods that constitute a service are defined by a label selector. Kubernetes provides two modes of service discovery, using environmental variables or using Kubernetes DNS. Service discovery assigns a stable IP address and DNS name to the service, and load balances traffic in a round-robin manner to network connections of that IP address among the pods matching the selector (even as failures cause the pods to move from machine to machine). By default a service is exposed inside a cluster (e.g., back end pods might be grouped into a service, with requests from the front-end pods load-balanced among them), but a service can also be exposed outside a cluster (e.g., for clients to reach front-end pods).

#### Volumes

File systems in the Kubernetes container provide ephemeral storage, by default. This means that a restart of the pod will wipe out any data on such containers, and therefore, this form of storage is quite limiting in anything but trivial applications. A Kubernetes Volume provides persistent storage that exists for the lifetime of the pod itself. This storage can also be used as shared disk space for containers within the pod. Volumes are mounted at specific mount points within the container, which are defined by the pod configuration, and cannot mount onto other volumes or link to other volumes. The same volume can be mounted at different points in the file system tree by different containers.

#### ConfigMaps & Secrets

A common application challenge is deciding where to store and manage configuration information, some of which may contain sensitive data. Configuration data can be anything as fine-grained as individual properties or coarse-grained information like entire configuration files or JSON / XML documents. Kubernetes provides two closely related mechanisms to deal with this need: "configmaps" and "secrets", both of which allow for configuration changes to be made without requiring an application build. The data from configmaps and secrets will be made available to every single instance of the application to which these objects have been bound via the deployment. A secret and/or a configmap is only sent to a node if a pod on that node requires it. Kubernetes will keep it in memory on that node. Once the pod that depends on the secret or configmap is deleted, the in-memory copy of all bound secrets and configmaps are deleted as well. The data is accessible to the pod through one of two ways: a) as environment variables (which will be created by Kubernetes when the pod is started) or b) available on the container file system that is visible only from within the pod.

The data itself is stored on the master which is a highly secured machine which nobody should have login access to. The biggest difference between a secret and a configmap is that the content of the data in a secret is base64 encoded. Recent versions of Kubernetes have introduced support for encryption to be used as well. Secrets are often used to store data like certificates, passwords, pull secrets (credentials to work with image registries), and ssh keys.

#### StatefulSets

Scaling stateless applications is only a matter of adding more running pods. Stateful workloads are harder, because the state needs to be preserved if a pod is restarted. If the application is scaled up or down, the state may need to be redistributed. Databases are an example of stateful workloads. When run in high-availability mode, many databases come with the notion of a primary instance and secondary instances. In this case, the notion of ordering of instances is important. Other applications like [Apache Kafka](https://en.wikipedia.org/wiki/Apache_Kafka "Apache Kafka") distribute the data amongst their brokers; hence, one broker is not the same as another. In this case, the notion of instance uniqueness is important.

StatefulSets are controllers (see above) that enforce the properties of uniqueness and ordering amongst instances of a pod and can be used to run stateful applications.

#### Replication controllers and deployments

A _ReplicaSet_ declares the number of instances of a pod that is needed, and a Replication Controller manages the system so that the number of healthy pods that are running matches the number of pods declared in the ReplicaSet (determined by evaluating its selector).

Deployments are a higher level management mechanism for ReplicaSets. While the Replication Controller manages the scale of the ReplicaSet, Deployments will manage what happens to the ReplicaSet - whether an update has to be rolled out, or rolled back, etc. When deployments are scaled up or down, this results in the declaration of the ReplicaSet changing - and this change in declared state is managed by the Replication Controller.

#### Labels & Selectors

Kubernetes enables clients (users or internal components) to attach keys called "labels" to any API object in the system, such as pods and nodes. Correspondingly, "label selectors" are queries against labels that resolve to matching objects. When a service is defined, one can define the label selectors that will be used by the service router/load balancer to select the pod instances that the traffic will be routed to. Thus, simply changing the labels of the pods or changing the label selectors on the service can be used to control which pods get traffic and which don't, which can be used to support various deployment patterns like [blue-green deployments](https://en.wikipedia.org/wiki/Blue-green_deployment "Blue-green deployment") or [A-B testing](https://en.wikipedia.org/wiki/A-B_testing "A-B testing"). This capability to dynamically control how services utilize implementing resources provides a loose coupling within the infrastructure.

For example, if an application's pods have labels for a system `tier` (with values such as `front-end`, `back-end`, for example) and a `release_track` (with values such as `[canary]`, `production`, for example), then an operation on all of `back-end` and `canary` nodes can use a label selector, such as:

> `tier=back-end AND release_track=canary`

Just like labels, field selectors also let one select Kubernetes resources. Unlike labels, the selection is based on the attribute values inherent to the resource being selected, rather than user-defined categorization. `metadata.name` and `metadata.namespace` are field selectors that will be present on all Kubernetes objects. Other selectors that can be used depend on the object/resource type.

#### Addons 

Add-ons operate just like any other application running within the cluster: they are implemented via pods and services, and are only different in that they implement features of the Kubernetes cluster. The pods may be managed by Deployments, ReplicationControllers, and so on. There are many add-ons, and the list is growing. Some of the more important are:

-   DNS: All Kubernetes clusters should have cluster DNS; it is a mandatory feature. Cluster DNS is a DNS server, in addition to the other DNS server(s) in your environment, which serves DNS records for Kubernetes services. Containers started by Kubernetes automatically include this DNS server in their DNS searches.
-   Web UI: This is a general purpose, web-based UI for Kubernetes clusters. It allows users to manage and troubleshoot applications running in the cluster, as well as the cluster itself.
-   Container Resource Monitoring: Providing a reliable application runtime, and being able to scale it up or down in response to workloads, means being able to continuously and effectively monitor workload performance. Container Resource Monitoring provides this capability by recording metrics about containers in a central database, and provides a UI for browsing that data. The cAdvisor is a component on a slave node that provides a limited metric monitoring capability. There are full metrics pipelines as well, such as Prometheus, which can meet most monitoring needs.
-   Cluster-level logging: Logs should have a separate storage and lifecycle independent of nodes, pods, or containers. Otherwise, node or pod failures can cause loss of event data. The ability to do this is called cluster-level logging, and such mechanisms are responsible for saving container logs to a central log store with search/browsing interface. Kubernetes provides no native storage for log data, but one can integrate many existing logging solutions into the Kubernetes cluster.

#### Storage

Containers emerged as a way to make software portable. The container contains all the packages you need to run a service. The provided file system makes containers extremely portable and easy to use in development. A container can be moved from development to test or production with no or relatively few configuration changes.

Historically Kubernetes was suitable only for stateless services. However, many applications have a database, which requires persistence, which leads to the creation of persistent storage for Kubernetes. Implementing persistent storage for containers is one of the top challenges of Kubernetes administrators, DevOps and cloud engineers. Containers may be ephemeral, but more and more of their data is not, so one needs to ensure the data's survival in case of container termination or hardware failure. When deploying containers with Kubernetes or containerized applications, companies often realize that they need persistent storage. They need to provide fast and reliable storage for databases, root images and other data used by the containers.

In addition to the landscape, the Cloud Native Computing Foundation (CNCF), has published other information about Kubernetes Persistent Storage including a blog helping to define the container attached storage pattern. This pattern can be thought of as one that uses Kubernetes itself as a component of the storage system or service.

More information about the relative popularity of these and other approaches can be found on the CNCF's landscape survey as well, which showed that OpenEBS from MayaData and Rook - a storage orchestration project - were the two projects most likely to be in evaluation as of the Fall of 2019.

Container Attached Storage is a type of data storage that emerged as Kubernetes gained prominence. The Container Attached Storage approach or pattern relies on Kubernetes itself for certain capabilities while delivering primarily block, file, object and interfaces to workloads running on Kubernetes.

Common attributes of Container Attached Storage include the use of extensions to Kubernetes, such as custom resource definitions, and the use of Kubernetes itself for functions that otherwise would be separately developed and deployed for storage or data management. Examples of functionality delivered by custom resource definitions or by Kubernetes itself include retry logic, delivered by Kubernetes itself, and the creation and maintenance of an inventory of available storage media and volumes, typically delivered via a custom resource definition.

### Kubernetes API 

A key component of the Kubernetes control plane is the API Server, which exposes an HTTP API that can be invoked by other parts of the cluster as well as end users and external components. This API is a [REST](https://en.wikipedia.org/wiki/REST "REST") API and is declarative in nature. There are two kinds of API resources. Most of the API resources in the Kubernetes API are objects. These represent a concrete instance of a concept on the cluster, like a pod or namespace. A small number of API resource types are "virtual". These represent operations rather than objects, such as a permission check, using the "subjectaccessreviews" resource. API resources that correspond to objects will be represented in the cluster with unique identifiers for the objects. Virtual resources do not have unique identifiers.

#### Operators

Kubernetes can be extended using Custom Resources. These API resources represent objects that are not part of the standard Kubernetes product. These resources can appear and disappear in a running cluster through dynamic registration. Cluster administrators can update Custom Resources independently of the cluster.

Custom Controllers are another extension mechanism. These interact with Custom Resources, and allow for a true declarative API that allows for the lifecycle management of Custom Resource that is aligned with the way that Kubernetes itself is designed. The combination of Custom Resources and Custom Controllers are often referred to as an (Kubernetes) Operator. The key use case for Operators are to capture the aim of a human operator who is managing a service or set of services and to implement them using automation, and with a declarative API supporting this automation. Human operators who look after specific applications and services have deep knowledge of how the system ought to behave, how to deploy it, and how to react if there are problems. Examples of problems solved by Operators include taking and restoring backups of that application's state, and handling upgrades of the application code alongside related changes such as database schemas or extra configuration settings.

#### Cluster API 

The same API design principles have been used to define an API to programmatically create, configure, and manage Kubernetes clusters. This is called the Cluster API. A key concept embodied in the API is using [Infrastructure as Software](https://en.wikipedia.org/wiki/Infrastructure_as_Software "Infrastructure as Software"), or the notion that the Kubernetes cluster infrastructure is itself a resource / object that can be managed just like any other Kubernetes resources. Similarly, machines that make up the cluster are also treated as a Kubernetes resource. The API has two pieces - the core API, and a provider implementation. The provider implementation consists of cloud-provider specific functions that let Kubernetes provide the cluster API in a fashion that is well-integrated with the cloud-provider's services and resources.

Cluster API was originally proposed in 2017 by Jacob Beacham, Kris Nóva, and Robert Bailey.

### Uses

Kubernetes is commonly used as a way to host a microservice-based implementation, because it and its associated ecosystem of tools provide all the capabilities needed to address key concerns of any [microservice architecture](https://en.wikipedia.org/wiki/Microservices#A_comparison_of_platforms "Microservices"). It is available in three forms: open source, commercial, and managed. Open source distributions include the original Kubernetes, Amazon EKS-D, [Red Hat OpenShift](https://en.wikipedia.org/wiki/OpenShift "OpenShift"), VMware Tanzu, Mirantis Kubernetes Engine, and D2iQ Kubernetes Platform. Managed offerings include GKE, Oracle Container Engine for Kubernetes, [Amazon Elastic](https://en.wikipedia.org/wiki/Amazon_Elastic_Compute_Cloud "Amazon Elastic Compute Cloud") Kubernetes Service, IBM Kubernetes Service, and Platform9 Managed Kubernetes.
# Practice
## Installing Minikube
I did the install on my personal Fedora 35 Laptop since it did not work well on the provided server. A simple `minikube start` with KVM Dependencies installed was enough to get minikube up and running. 
```bash
-> ~ minikube start 
 minikube v1.25.1 on Fedora 35
 Automatically selected the kvm2 driver
 Starting control plane node minikube in cluster minikube
 Creating kvm2 VM (CPUs=2, Memory=6000MB, Disk=20000MB) ...
 Preparing Kubernetes v1.23.1 on Docker 20.10.12 ...
    ▪ kubelet.housekeeping-interval=5m
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
 Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
 Enabled addons: storage-provisioner, default-storageclass
 Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```
	
Checking the status of the Minikube Cluster: 
```bash
-> ~ minikube status 
+minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured


```

## Deploying a demo app

### Installing Kompose
```Bash
-> ~ curl -L https://github.com/kubernetes/kompose/releases/download/v1.26.0/kompose-linux-amd64 -o kompose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   656  100   656    0     0   2328      0 --:--:-- --:--:-- --:--:--  2334
100 20.7M  100 20.7M    0     0  10.3M      0  0:00:02  0:00:02 --:--:-- 12.1M
-> ~ chmod +x kompose
-> ~ sudo mv ./kompose /usr/local/bin/kompose
```

### Convert Docker-Compose file to Kubernetes Deployment Files
Following tutorial was used: 
https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes/

The yaml file describe a few services: 
- It starts a Redis Server
- A backend server which communicates with the Redis Container 
- A simple frontend guestbook

Ports are mapped to random ports on the outside to access.

```yaml
version: "2"

services:

  redis-master:
    image: k8s.gcr.io/redis:e2e
    ports:
      - "6379"

  redis-slave:
    image: gcr.io/google_samples/gb-redisslave:v3
    ports:
      - "6379"
    environment:
      - GET_HOSTS_FROM=dns

  frontend:
    image: gcr.io/google-samples/gb-frontend:v4
    ports:
      - "80:80"
    environment:
      - GET_HOSTS_FROM=dns
    labels:
      kompose.service.type: LoadBalancer

```

We can't use the compose file in Kubernetes, tho. To convert it we can use an nice tool named `kompose` that converts the files for us so that we can later use them. Kompose automatically detects the compose file in the folder and creates the Kubernetes YAML for us.

```Bash
-> kubernetes kompose convert
INFO Kubernetes file "frontend-tcp-service.yaml" created 
INFO Kubernetes file "redis-master-service.yaml" created 
INFO Kubernetes file "redis-slave-service.yaml" created 
INFO Kubernetes file "frontend-deployment.yaml" created 
INFO Kubernetes file "redis-master-deployment.yaml" created 
INFO Kubernetes file "redis-slave-deployment.yaml" created 
```

### Deploying the Demo Guestbook to Cluster

After converting we are ready to deploy the services to the cluster in the Minikube VM. 

You use `kubectl apply -f <FILES>` for this step.

```Bash
-> kubernetes kubectl apply -f frontend-tcp-service.yaml,frontend-deployment.yaml,redis-master-deployment.yaml,redis-master-service.yaml,redis-slave-deployment.yaml,redis-slave-service.yaml
service/frontend-tcp created
deployment.apps/frontend created
deployment.apps/redis-master created
service/redis-master configured
deployment.apps/redis-slave created
service/redis-slave configured
```

The deployment is configured successfully. We can now print some information to get an idea where we need to go to access the deployed geustbook app. 

We can first list all the services we have with `kubectl get svc`. This won't tell us the endpoint we need to connect, tho.
```Bash
-> kubernetes kubectl get svc 
NAME           TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
frontend       LoadBalancer   10.104.204.12    <pending>     80:30870/TCP   20m
frontend-tcp   LoadBalancer   10.105.238.210   <pending>     80:32510/TCP   55s
kubernetes     ClusterIP      10.96.0.1        <none>        443/TCP        36m
redis-master   ClusterIP      10.101.103.105   <none>        6379/TCP       20m
redis-slave    ClusterIP      10.110.27.57     <none>        6379/TCP       20m
```

To get the endpoint we need for the SSH Tunnel we need to "describe" a service, meaning we need to print out some debug information about it. This is done with `kubectl describe svc frontend-tcp` in our case. 

```Bash
-> kubernetes kubectl describe svc frontend-tcp 
Name:                     frontend-tcp
Namespace:                default
Labels:                   io.kompose.service=frontend-tcp
Annotations:              kompose.cmd: kompose convert
                          kompose.service.type: LoadBalancer
                          kompose.version: 1.26.0 (40646f47)
Selector:                 io.kompose.service=frontend
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.105.238.210
IPs:                      10.105.238.210
Port:                     80  80/TCP
TargetPort:               80/TCP
NodePort:                 80  32510/TCP
Endpoints:                172.17.0.3:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

### Connecting to the deployed App

To get the IP for the needed SSH tunnel I need to find out the IP of the VM I'm running minikube on. I did this by connecting to the Minikube VM via SSH and then filtering the output for the ethernet interface. 

```Bash
-> kubernetes minikube ssh 
                         _             _            
            _         _ ( )           ( )           
  ___ ___  (_)  ___  (_)| |/')  _   _ | |_      __  
/' _ ` _ `\| |/' _ `\| || , <  ( ) ( )| '_`\  /'__`\
| ( ) ( ) || || ( ) || || |\`\ | (_) || |_) )(  ___/
(_) (_) (_)(_)(_) (_)(_)(_) (_)`\___/'(_,__/'`\____)

$ ip a | grep eth0  
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    inet 192.168.39.197/24 brd 192.168.39.255 scope global dynamic eth0
```

To access the Guestbook App, we need to forward a port to the local machine. The simplest way to do this is via an SSH Tunnel. Port 5000 is mapped to the Endpoint we gathered earlier. Default user is `docker` and password for this user is `tcuser`, in the case of a Minikube VM.

```Bash
-> kubernetes ssh -L 5000:172.17.0.3:80 docker@192.168.39.197
The authenticity of host '192.168.39.197 (192.168.39.197)' can't be established.
ED25519 key fingerprint is SHA256:Zm6g1g9r+hjfUO9XTsww3ODPOzt/TvdTghAkrMh9AxM.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.39.197' (ED25519) to the list of known hosts.
docker@192.168.39.197's password: 
                         _             _            
            _         _ ( )           ( )           
  ___ ___  (_)  ___  (_)| |/')  _   _ | |_      __  
/' _ ` _ `\| |/' _ `\| || , <  ( ) ( )| '_`\  /'__`\
| ( ) ( ) || || ( ) || || |\`\ | (_) || |_) )(  ___/
(_) (_) (_)(_)(_) (_)(_)(_) (_)`\___/'(_,__/'`\____)

$ 

```

Running app: 
![Guestbook App running](Pasted image 20220216021444.png)