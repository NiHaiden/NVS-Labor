---
title: NVS Docker & Tomcat Protokoll
author: Niklas Haiden - 5BHIF
date: 19.01.2022
tableofcontent: true
titlepage: true
titlepage-text-color: "000000"
logo: "logo.png"
logo-width: 100mm
toc-own-page: true
listings-disable-line-numbers: true
---
# Theory 
## Docker
### Overview
Source: https://www.redhat.com/en/topics/containers/what-is-docker

The word "Docker" refers to several things, including an open source community project; tools from the open source project; Docker Inc., the company that primarily supports that project; and the tools that company formally supports. The fact that the technologies and the company share the same name can be confusing.

Here's a brief explainer:

-   The IT software "Docker” is containerization technology that enables the creation and use of [Linux® containers](https://www.redhat.com/en/topics/containers).
-   The [open source Docker community](https://forums.docker.com/) works to improve these technologies to benefit all users.
-   The company, [Docker Inc.](https://www.docker.com/), builds on the work of the Docker community, makes it more secure, and shares those advancements back to the greater community. It then supports the improved and hardened technologies for enterprise customers.

With Docker, you can treat containers like extremely lightweight, modular virtual machines. And you get flexibility with those containers&mdash;you can create, deploy, copy, and move them from environment to environment, which helps [optimize your apps for the cloud](https://www.redhat.com/en/topics/cloud-native-apps).

### Inner workings 

The Docker technology uses the [Linux kernel](https://www.redhat.com/en/topics/linux/what-is-the-linux-kernel) and features of the kernel, like [Cgroups](https://www.redhat.com/en/blog/world-domination-cgroups-rhel-8-welcome-cgroups-v2) and [namespaces](https://lwn.net/Articles/528078/), to segregate processes so they can run independently. This independence is the intention of containers—the ability to run multiple processes and apps separately from one another to make better use of your infrastructure while [retaining the security](https://www.redhat.com/en/topics/security) you would have with separate systems.

Container tools, including Docker, provide an image-based deployment model. This makes it easy to share an application, or set of services, with all of their dependencies across multiple environments. Docker also automates deploying the application (or combined sets of processes that make up an app) inside this container environment.

These tools built on top of Linux containers—what makes Docker user-friendly and unique—gives users unprecedented access to apps, the ability to rapidly deploy, and control over versions and version distribution.

![Architecture](Pasted image 20220118231615.png)

Although sometimes confused, Docker is not the same as a traditional Linux container. Docker technology was initially built on top of the [LXC](https://linuxcontainers.org/) technology—which most people associate with "traditional" Linux containers—though it’s since moved away from that dependency. LXC was useful as lightweight [virtualization](https://www.redhat.com/en/topics/virtualization), but it didn’t have a great developer or user experience. The Docker technology brings more than the ability to run containers—it also eases the process of creating and building containers, shipping images, and versioning of images, among other things.
Traditional Linux containers use an init system that can manage multiple processes. This means entire applications can run as one. The Docker technology encourages applications to be broken down into their separate processes and provides the tools to do that. This granular approach has its advantages.

### Advantages

#### Modularity

The Docker approach to containerization focuses on the ability to take down a part of an application to update or repair, without having to take down the whole app. In addition to this microservices-based approach, you can share processes among multiple apps in much the same way [service-oriented architecture](https://en.wikipedia.org/wiki/Service-oriented_architecture) (SOA) does.

#### Layers and image version control

Each Docker image file is made up of a series of layers that are combined into a single image. A layer is created when the image changes. Every time a user specifies a command, such as _run_ or _copy_, a new layer gets created.

Docker reuses these layers to build new containers, which accelerates the building process. Intermediate changes are shared among images, further improving speed, [size](http://developers.redhat.com/blog/2016/03/09/more-about-docker-images-size/), and efficiency. Also inherent to layering is version control: Every time there’s a new change, you essentially have a built-in changelog, providing you with full control over your container images.

#### Rollback

Perhaps the best part about layering is the ability to roll back. Every image has layers. Don’t like the current iteration of an image? Roll it back to the previous version. This supports an agile development approach and helps make [continuous integration and deployment (CI/CD)](https://www.redhat.com/en/topics/devops/what-is-ci-cd) a reality from a tools perspective.

#### Rapid deployment

Getting new hardware up, running, provisioned, and available used to take days, and the level of effort and overhead was burdensome. Docker-based containers can reduce deployment to seconds. By creating a container for each process, you can quickly share those processes with new apps. And, since an operating system doesn’t need to boot to add or move a container, deployment times are substantially shorter. Paired with shorter deployment times, you can easily and cost-effectively create and destroy data created by your containers without concern.

So, Docker technology is a more granular, controllable, microservices-based approach that places greater value on efficiency.


### Container

https://docs.docker.com/get-started/overview/#docker-architecture
A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.

A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.

##### Example `docker run` command

The following command runs an `ubuntu` container, attaches interactively to your local command-line session, and runs `/bin/bash`.

```
$ docker run -i -t ubuntu /bin/bash
```

When you run this command, the following happens (assuming you are using the default registry configuration):

1.  If you do not have the `ubuntu` image locally, Docker pulls it from your configured registry, as though you had run `docker pull ubuntu` manually.
    
2.  Docker creates a new container, as though you had run a `docker container create` command manually.
    
3.  Docker allocates a read-write filesystem to the container, as its final layer. This allows a running container to create or modify files and directories in its local filesystem.
    
4.  Docker creates a network interface to connect the container to the default network, since you did not specify any networking options. This includes assigning an IP address to the container. By default, containers can connect to external networks using the host machine’s network connection.
    
5.  Docker starts the container and executes `/bin/bash`. Because the container is running interactively and attached to your terminal (due to the `-i` and `-t` flags), you can provide input using your keyboard while the output is logged to your terminal.
    
6.  When you type `exit` to terminate the `/bin/bash` command, the container stops but is not removed. You can start it again or remove it.

### Image

https://docs.docker.com/get-started/overview/#docker-architecture
An _image_ is a read-only template with instructions for creating a Docker container. Often, an image is _based on_ another image, with some additional customization. For example, you may build an image which is based on the `ubuntu` image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a _Dockerfile_ with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

### Registries

https://docs.docker.com/get-started/overview/#docker-architecture
A Docker _registry_ stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry.

When you use the `docker pull` or `docker run` commands, the required images are pulled from your configured registry. When you use the `docker push` command, your image is pushed to your configured registry.

## Docker Compose

https://docs.docker.com/compose/
Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see [the list of features](https://docs.docker.com/compose/#features).

Compose works in all environments: production, staging, development, testing, as well as CI workflows. You can learn more about each case in [Common Use Cases](https://docs.docker.com/compose/#common-use-cases).

Using Compose is basically a three-step process:

1.  Define your app’s environment with a `Dockerfile` so it can be reproduced anywhere.
    
2.  Define the services that make up your app in `docker-compose.yml` so they can be run together in an isolated environment.
    
3.  Run `docker compose up` and the [Docker compose command](https://docs.docker.com/compose/cli-command/) starts and runs your entire app. You can alternatively run `docker-compose up` using the docker-compose binary.
    

A `docker-compose.yml` looks like this:

```
version: "3.9"  # optional since v1.27.0
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
      - logvolume01:/var/log
    links:
      - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

For more information about the Compose file, see the [Compose file reference](https://docs.docker.com/compose/compose-file/).

Compose has commands for managing the whole lifecycle of your application:

-   Start, stop, and rebuild services
-   View the status of running services
-   Stream the log output of running services
-   Run a one-off command on a service

### Features

#### Multiple isolated environments on a single host

Compose uses a project name to isolate environments from each other. You can make use of this project name in several different contexts:

-   on a dev host, to create multiple copies of a single environment, such as when you want to run a stable copy for each feature branch of a project
-   on a CI server, to keep builds from interfering with each other, you can set the project name to a unique build number
-   on a shared host or dev host, to prevent different projects, which may use the same service names, from interfering with each other

The default project name is the basename of the project directory. You can set a custom project name by using the [`-p` command line option](https://docs.docker.com/compose/reference/) or the [`COMPOSE_PROJECT_NAME` environment variable](https://docs.docker.com/compose/reference/envvars/#compose_project_name).

The default project directory is the base directory of the Compose file. A custom value for it can be defined with the `--project-directory` command line option.

#### Preserve volume data when containers are created

Compose preserves all volumes used by your services. When `docker-compose up` runs, if it finds any containers from previous runs, it copies the volumes from the old container to the new container. This process ensures that any data you’ve created in volumes isn’t lost.

If you use `docker-compose` on a Windows machine, see [Environment variables](https://docs.docker.com/compose/reference/envvars/) and adjust the necessary environment variables for your specific needs.

#### Only recreate containers that have changed

Compose caches the configuration used to create a container. When you restart a service that has not changed, Compose re-uses the existing containers. Re-using containers means that you can make changes to your environment very quickly.

#### Variables and moving a composition between environments

Compose supports variables in the Compose file. You can use these variables to customize your composition for different environments, or different users. See [Variable substitution](https://docs.docker.com/compose/compose-file/compose-file-v3/#variable-substitution) for more details.

You can extend a Compose file using the `extends` field or by creating multiple Compose files. See [extends](https://docs.docker.com/compose/extends/) for more details.

## Docker Swarm

https://docs.docker.com/engine/swarm/key-concepts/

### What is Swarm? 

The cluster management and orchestration features embedded in the Docker Engine are built using [swarmkit](https://github.com/docker/swarmkit/). Swarmkit is a separate project which implements Docker’s orchestration layer and is used directly within Docker.

A swarm consists of multiple Docker hosts which run in **swarm mode** and act as managers (to manage membership and delegation) and workers (which run [swarm services](https://docs.docker.com/engine/swarm/key-concepts/#services-and-tasks)). A given Docker host can be a manager, a worker, or perform both roles. When you create a service, you define its optimal state (number of replicas, network and storage resources available to it, ports the service exposes to the outside world, and more). Docker works to maintain that desired state. For instance, if a worker node becomes unavailable, Docker schedules that node’s tasks on other nodes. A _task_ is a running container which is part of a swarm service and managed by a swarm manager, as opposed to a standalone container.

One of the key advantages of swarm services over standalone containers is that you can modify a service’s configuration, including the networks and volumes it is connected to, without the need to manually restart the service. Docker will update the configuration, stop the service tasks with the out of date configuration, and create new ones matching the desired configuration.

When Docker is running in swarm mode, you can still run standalone containers on any of the Docker hosts participating in the swarm, as well as swarm services. A key difference between standalone containers and swarm services is that only swarm managers can manage a swarm, while standalone containers can be started on any daemon. Docker daemons can participate in a swarm as managers, workers, or both.

In the same way that you can use [Docker Compose](https://docs.docker.com/compose/) to define and run containers, you can define and run [Swarm service](https://docs.docker.com/engine/swarm/services/) stacks.

Keep reading for details about concepts relating to Docker swarm services, including nodes, services, tasks, and load balancing.

### Key Highlights 

https://docs.docker.com/engine/swarm/

Current versions of Docker include _swarm mode_ for natively managing a cluster of Docker Engines called a _swarm_. Use the Docker CLI to create a swarm, deploy application services to a swarm, and manage swarm behavior.

Docker Swarm mode is built into the Docker Engine. Do not confuse Docker Swarm mode with [Docker Classic Swarm](https://github.com/docker/classicswarm) which is no longer actively developed.

-   **Cluster management integrated with Docker Engine:** Use the Docker Engine CLI to create a swarm of Docker Engines where you can deploy application services. You don’t need additional orchestration software to create or manage a swarm.
    
-   **Decentralized design:** Instead of handling differentiation between node roles at deployment time, the Docker Engine handles any specialization at runtime. You can deploy both kinds of nodes, managers and workers, using the Docker Engine. This means you can build an entire swarm from a single disk image.
    
-   **Declarative service model:** Docker Engine uses a declarative approach to let you define the desired state of the various services in your application stack. For example, you might describe an application comprised of a web front end service with message queueing services and a database backend.
    
-   **Scaling:** For each service, you can declare the number of tasks you want to run. When you scale up or down, the swarm manager automatically adapts by adding or removing tasks to maintain the desired state.
    
-   **Desired state reconciliation:** The swarm manager node constantly monitors the cluster state and reconciles any differences between the actual state and your expressed desired state. For example, if you set up a service to run 10 replicas of a container, and a worker machine hosting two of those replicas crashes, the manager creates two new replicas to replace the replicas that crashed. The swarm manager assigns the new replicas to workers that are running and available.
    
-   **Multi-host networking:** You can specify an overlay network for your services. The swarm manager automatically assigns addresses to the containers on the overlay network when it initializes or updates the application.
    
-   **Service discovery:** Swarm manager nodes assign each service in the swarm a unique DNS name and load balances running containers. You can query every container running in the swarm through a DNS server embedded in the swarm.
    
-   **Load balancing:** You can expose the ports for services to an external load balancer. Internally, the swarm lets you specify how to distribute service containers between nodes.
    
-   **Secure by default:** Each node in the swarm enforces TLS mutual authentication and encryption to secure communications between itself and all other nodes. You have the option to use self-signed root certificates or certificates from a custom root CA.
    
-   **Rolling updates:** At rollout time you can apply service updates to nodes incrementally. The swarm manager lets you control the delay between service deployment to different sets of nodes. If anything goes wrong, you can roll back to a previous version of the service.

### Nodes

https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/

A **node** is an instance of the Docker engine participating in the swarm. You can also think of this as a Docker node. You can run one or more nodes on a single physical computer or cloud server, but production swarm deployments typically include Docker nodes distributed across multiple physical and cloud machines.

To deploy your application to a swarm, you submit a service definition to a **manager node**. The manager node dispatches units of work called [tasks](https://docs.docker.com/engine/swarm/key-concepts/#services-and-tasks) to worker nodes.

Manager nodes also perform the orchestration and cluster management functions required to maintain the desired state of the swarm. Manager nodes elect a single leader to conduct orchestration tasks.

**Worker nodes** receive and execute tasks dispatched from manager nodes. By default manager nodes also run services as worker nodes, but you can configure them to run manager tasks exclusively and be manager-only nodes. An agent runs on each worker node and reports on the tasks assigned to it. The worker node notifies the manager node of the current state of its assigned tasks so that the manager can maintain the desired state of each worker.

#### Manager Node

Manager nodes handle cluster management tasks:

-   maintaining cluster state
-   scheduling services
-   serving swarm mode [HTTP API endpoints](https://docs.docker.com/engine/api/)

Using a [Raft](https://raft.github.io/raft.pdf) implementation, the managers maintain a consistent internal state of the entire swarm and all the services running on it. For testing purposes it is OK to run a swarm with a single manager. If the manager in a single-manager swarm fails, your services continue to run, but you need to create a new cluster to recover.

To take advantage of swarm mode’s fault-tolerance features, Docker recommends you implement an odd number of nodes according to your organization’s high-availability requirements. When you have multiple managers you can recover from the failure of a manager node without downtime.

-   A three-manager swarm tolerates a maximum loss of one manager.
-   A five-manager swarm tolerates a maximum simultaneous loss of two manager nodes.
-   An `N` manager cluster tolerates the loss of at most `(N-1)/2` managers.
-   Docker recommends a maximum of seven manager nodes for a swarm.

#### Worker Node

Worker nodes are also instances of Docker Engine whose sole purpose is to execute containers. Worker nodes don’t participate in the Raft distributed state, make scheduling decisions, or serve the swarm mode HTTP API.

You can create a swarm of one manager node, but you cannot have a worker node without at least one manager node. By default, all managers are also workers. In a single manager node cluster, you can run commands like `docker service create` and the scheduler places all tasks on the local Engine.

To prevent the scheduler from placing tasks on a manager node in a multi-node swarm, set the availability for the manager node to `Drain`. The scheduler gracefully stops tasks on nodes in `Drain` mode and schedules the tasks on an `Active` node. The scheduler does not assign new tasks to nodes with `Drain` availability.

Refer to the [`docker node update`](https://docs.docker.com/engine/reference/commandline/node_update/) command line reference to see how to change node availability.


### Services and Tasks

A **service** is the definition of the tasks to execute on the manager or worker nodes. It is the central structure of the swarm system and the primary root of user interaction with the swarm.

When you create a service, you specify which container image to use and which commands to execute inside running containers.

In the **replicated services** model, the swarm manager distributes a specific number of replica tasks among the nodes based upon the scale you set in the desired state.

For **global services**, the swarm runs one task for the service on every available node in the cluster.

A **task** carries a Docker container and the commands to run inside the container. It is the atomic scheduling unit of swarm. Manager nodes assign tasks to worker nodes according to the number of replicas set in the service scale. Once a task is assigned to a node, it cannot move to another node. It can only run on the assigned node or fail.

### Load Balancing

The swarm manager uses **ingress load balancing** to expose the services you want to make available externally to the swarm. The swarm manager can automatically assign the service a **PublishedPort** or you can configure a PublishedPort for the service. You can specify any unused port. If you do not specify a port, the swarm manager assigns the service a port in the 30000-32767 range.

External components, such as cloud load balancers, can access the service on the PublishedPort of any node in the cluster whether or not the node is currently running the task for the service. All nodes in the swarm route ingress connections to a running task instance.

Swarm mode has an internal DNS component that automatically assigns each service in the swarm a DNS entry. The swarm manager uses **internal load balancing** to distribute requests among services within the cluster based upon the DNS name of the service.

# Practice 
## Installing Docker on the Server
I'm installing Docker on the server was done using my own script. It installs necessary dependencies to to add the Docker Repository, adds the repository and the required GPG Key and then installs the needed Docker Packages. At the end, it also installs Docker-Compose. 

```Bash
root@u2004-5bhif-6:/usr/lib/cgi-bin# curl https://raw.githubusercontent.com/NiHaiden/convenience-scripts/main/docker-install-ubuntu.sh | bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   987  100   987    0     0   3312      0 --:--:-- --:--:-- --:--:--  3312
Removing any existing remainder of Docker Components
Reading package lists... Done
Building dependency tree
[...]
Installing Docker-Compose and making it executable
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   633  100   633    0     0   1701      0 --:--:-- --:--:-- --:--:--  1706
100 11.6M  100 11.6M    0     0  3733k      0  0:00:03  0:00:03 --:--:-- 5013k
```

I'm adding the docker group to the schueler user so I don't have to run docker commands as root. 

```Bash
root@u2004-5bhif-6:/usr/lib/cgi-bin# usermod -aG docker schueler
```

## Tomcat
### Run Tomcat via Docker, without Mgmt-Interface
Using docker run without the downloaded image will first pull it from docker hub and then run it on the local server, making it accessible from port 8888. 
```Bash
root@u2004-5bhif-6:/usr/lib/cgi-bin# docker run -it --rm -p 8888:8080 tomcat:9.0
Unable to find image 'tomcat:9.0' locally
9.0: Pulling from library/tomcat
647acf3d48c2: Pull complete
b02967ef0034: Pull complete
e1ad2231829e: Pull complete
5576ce26bf1d: Pull complete
26518d6c686a: Pull complete
cdb1f4e0dbfd: Pull complete
1d872b5136cc: Downloading [=====================>                             ]  85.34MB/203.1MB
0b9db4d94c97: Download complete
576f01df8837: Download complete
1d872b5136cc: Pull complete
0b9db4d94c97: Pull complete
576f01df8837: Pull complete
044820f6a913: Pull complete
Digest: sha256:db8ac6f67c9865d634dc767ea3c3726beb7ca58998f4295b3bab8eee1410b58c
Status: Downloaded newer image for tomcat:9.0
Using CATALINA_BASE:   /usr/local/tomcat
Using CATALINA_HOME:   /usr/local/tomcat
Using CATALINA_TMPDIR: /usr/local/tomcat/temp
Using JRE_HOME:        /usr/local/openjdk-11
Using CLASSPATH:       /usr/local/tomcat/bin/bootstrap.jar:/usr/local/tomcat/bin/tomcat-juli.jar
Using CATALINA_OPTS:
NOTE: Picked up JDK_JAVA_OPTIONS:  --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.util.concurrent=ALL-UNNAMED --add-opens=java.rmi/sun.rmi.transport=ALL-UNNAMED
24-Nov-2021 14:05:25.440 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server version name:   Apache Tomcat/9.0.55
24-Nov-2021 14:05:25.482 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server built:          Nov 10 2021 08:26:45 UTC
24-Nov-2021 14:05:25.484 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server version number: 9.0.55.0
```

Testing the fresh installed Tomcat. 

![Tomcat Test](Pasted image 20211124151601.png)

### Run Tomcat with the Mgmt-Interface
For this to work we need a user with a few pre-defined roles to log in to. 
We need to define the `manager-gui` and `manager-script` role first in the XML. 
After that we define the user with a username and a password and assign him all the roles so we can later deploy WAR-Apps using the Management-Interface.
The Content of below get's saved in a file called `tomcat-users.xml`.

```XML
<tomcat-users>
<role rolename="manager-gui"/> 
<role rolename="manager-script"/> 
<user username="tomcat" password="s3cret" roles="manager-gui,manager-script"/> 
</tomcat-users>
```

Since the manager isn't enabled by default, we need to enable it using `context.xml` File. 

```XML 
<Context antiResourceLocking="false" privileged="true" >
<!-- 
<Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> --> <Manager sessionAttributeValueClassNameFilter="java\.lang\.(?:Boolean|Integer|Long|Number|String)|org\.apache\.catalina\.filters\.CsrfPreventionFilter\$LruCache(?:\$1)?|java\.util\.(?:Linked)?HashMap"/> </Context>
```

To finally enable the Manager and the respective User for it, we need to mount the users and context file with a docker volume. The command we pass with `/bin/bash` will move the existing webapps folder to webapps2. The command after that copies the manager from the webapps.dist directory to webapps. After that, the `context.xml` get copied over from the `/tmp` folder. The same goes for the users-file. After that the catalina.sh script get's executed, to start Tomcat.

```Bash 
sudo docker run \ 
--name tomcat \ 
-it \ 
-p 8080:8080 \ 
-v /home/schueler/tomcat-users.xml:/usr/local/tomcat/conf/tomcat-users.xml \ 
-v /home/schueler/context.xml:/tmp/context.xml \ 
tomcat:9.0 \ 
/bin/bash -c "mv /usr/local/tomcat/webapps /usr/local/tomcat/webapps2; mv /usr/local/tomcat/webapps.dist /usr/local/tomcat/webapps; cp /tmp/context.xml /usr/local/tomcat/webapps/manager/META-INF/context.xml; catalina.sh run"
```

![Tomcat Manager Test](Pasted image 20211124160635.png)

## Creating a war application
We were asked to deply a Demo App to the Tomcat Container. So I created a demo REST API with Spring.

### Application setup in intellij 
Following options were used in the IntelliJ Setup:
- Selected JDK: 11 
- WAR App Format for deploying later on

![Application Setup in IJ](Pasted image 20211124160928.png)

### Test Application
This is the code for the test app. It's a simple test REST API with one endpoint which sends out "Hello World" when a user goes to it.

```Java
package dev.nhaiden.nvstest;  
  
import org.springframework.boot.SpringApplication;  
import org.springframework.boot.autoconfigure.SpringBootApplication;  
import org.springframework.web.bind.annotation.GetMapping;  
import org.springframework.web.bind.annotation.RestController;  
  
@RestController  
@SpringBootApplication  
public class NvstestApplication {  
  
    public static void main(String[] args) {  
        SpringApplication.run(NvstestApplication.class, args);  
 }  
  
    @GetMapping("/hello")  
    public String hello() {  
        return "Hello World from Tomcat app!";  
 }  
  
}
```

I built the Java App with the WAR Packaging Option, which is necessary for it to be deployed to Tomcat:

![Building the Java App](Pasted image 20211124161620.png)

### Deploy App 
Select File in Windows Explorer

![Selecting file in Windows Explorer](Pasted image 20211124161721.png)

Clicking on "Installieren" will deploy the WAR File.

![Click on Installieren](Pasted image 20211124161735.png)

You can see in the Tomcat Manager that the application was successfully deployed to the server.

![Successfully deployed, woowza](Pasted image 20211124161941.png)

Opening the Application and going to the defined endpoint brings up the text we programmed into the application:

![Testing the endpoint](Pasted image 20211124161953.png)

## Nginx App

We have a endpoint which is only accesible with a IP and Port Number. We want to use an SSL Certificate and have a nice URL / Domain for our web app. So that's why we use Nginx as a reverse proxy to serve the Tomcat App to us.

### Install nginx 
We install nginx with apt like so: 

```Bash
-> html sudo apt install nginx
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
  nginx
0 upgraded, 1 newly installed, 0 to remove and 49 not upgraded.
Need to get 3620 B of archives.
After this operation, 45.1 kB of additional disk space will be used.
Get:1 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 nginx all 1.18.0-0ubuntu1.2 [3620 B]
Fetched 3620 B in 0s (33.0 kB/s)
Selecting previously unselected package nginx.
(Reading database ... 119102 files and directories currently installed.)
Preparing to unpack .../nginx_1.18.0-0ubuntu1.2_all.deb ...
Unpacking nginx (1.18.0-0ubuntu1.2) ...
Setting up nginx (1.18.0-0ubuntu1.2) ...
```

#### Check if nginx is running 

With the help of systemctl we check if Nginx has started correctly. 

```Bash
-> html sudo systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2021-12-01 13:00:05 UTC; 5min ago
       Docs: man:nginx(8)
   Main PID: 56578 (nginx)
      Tasks: 2 (limit: 2279)
     Memory: 6.2M
     CGroup: /system.slice/nginx.service
             ├─56578 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             └─56579 nginx: worker process

Dec 01 13:00:05 u2004-5bhif-6 systemd[1]: Starting A high performance web server and a reverse proxy server...
Dec 01 13:00:05 u2004-5bhif-6 systemd[1]: Started A high performance web server and a reverse proxy server.
```

### Creating a new config
This is the config for the reverse proxy. I've written it in the default file. Every request that goes to port 80 will be redirected to the HTTPS version of the site, as indicated by the first `server` block. I used the same certificates from the previous Apache Protocol, for my public address. We redirect the traffic to our app running on port 8080 so that endusers never see the Tomcat Homepage or Tomcat Manager, as indicated by the `location` block. 

```Bash
-> sites-enabled cat default
server {
    listen 80;
    return 301 https://$host$request_uri;
}

server {

    listen 443;
    server_name niklas-public.nvs.lan;

    ssl_certificate           /etc/ssl/certs/niklas-public.nvs.lan.crt;
    ssl_certificate_key       /etc/ssl/private/niklas-public.nvs.lan.key;

    ssl on;
    ssl_session_cache  builtin:1000  shared:SSL:10m;
    ssl_protocols  TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers HIGH:!aNULL:!eNULL:!EXPORT:!CAMELLIA:!DES:!MD5:!PSK:!RC4;
    ssl_prefer_server_ciphers on;

    access_log            /var/log/nginx/jenkins.access.log;

    location / {

      proxy_set_header        Host $host;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        X-Forwarded-Proto $scheme;

      # Fix the “It appears that your reverse proxy set up is broken" error.
      proxy_pass          http://niklas-public.nvs.lan:8080/nvstest-0.0.1-SNAPSHOT/hello;
      proxy_read_timeout  90;

      proxy_redirect      http://niklas-public.nvs.lan:8080/nvstest-0.0.1-SNAPSHOT/hello https://niklas-public.nvs.lan;
    }
  }
```

![Testing the HTTPS Config](Pasted image 20211201143643.png)

## Docker Image 
Until now we had to mount or config files and run a command to access the manager interface. This all changes now, we'll create a image that will include the config files right out of the box and will perform the necessary commands right at the image compile time.

### Create custom Dockerfile
To build a image, we need a Dockerfile. It's a specific set of instructions that tell Docker what do and how to do it when building an image. In this `Dockerfile` we use the Tomcat Image from Dockerhub as our base image. With the `COPY` directive we copy the necessary config files into the correct folders, right in the docker image. After that, with the `RUN` directive, we run the necessary docker commands to get our setup working. 
With the `EXPOSE` Keyword we define the port on which the container will expose Tomcat if we want to have outside access later on. 

`CMD` tells the image what to do when we run a container with this specific image. 

```Dockerfile
FROM tomcat:9.0

COPY ./tomcat-users.xml /usr/local/tomcat/conf/tomcat-users.xml
COPY ./context.xml /tmp/context.xml

RUN mv /usr/local/tomcat/webapps /usr/local/tomcat/webapps2
RUN mv /usr/local/tomcat/webapps.dist /usr/local/tomcat/webapps
COPY nvstest-0.0.1-SNAPSHOT.war /usr/local/tomcat/webapps
RUN cp /tmp/context.xml /usr/local/tomcat/webapps/manager/META-INF/context.xml

EXPOSE 8080

CMD ["catalina.sh", "run"]
```

### Build Image from Dockerfile
To build the container, we use the Docker Container Build System. With `t` we specify a custom tag and version for the container. With `.` we just say that docker should use the Dockerfile named `Dockerfile` in the current folder. Naming the Dockerfile `Dockerfile` will result in the automatic pickup from the docker daemon.

```Bash
-> ~ docker build -t niklashaiden/customtomcat:0.0.1 .
Sending build context to Docker daemon  12.02MB
Step 1/9 : FROM tomcat:9.0
 ---> 76206e3ba4b1
Step 2/9 : COPY ./tomcat-users.xml /usr/local/tomcat/conf/tomcat-users.xml
 ---> Using cache
 ---> 93d706da2136
Step 3/9 : COPY ./context.xml /tmp/context.xml
 ---> Using cache
 ---> 2f67872e79b1
Step 4/9 : RUN mv /usr/local/tomcat/webapps /usr/local/tomcat/webapps2
 ---> Using cache
 ---> a5157a54a912
Step 5/9 : RUN mv /usr/local/tomcat/webapps.dist /usr/local/tomcat/webapps
 ---> Using cache
 ---> 2acfb5b3c56a
Step 6/9 : COPY nvstest-0.0.1-SNAPSHOT.war /usr/local/tomcat/webapps
 ---> 3f114b49045a
Step 7/9 : RUN cp /tmp/context.xml /usr/local/tomcat/webapps/manager/META-INF/context.xml
 ---> Running in fdd2cb6bd154
Removing intermediate container fdd2cb6bd154
 ---> 65885b2aaa8f
Step 8/9 : EXPOSE 8080
 ---> Running in b9df62160a5a
Removing intermediate container b9df62160a5a
 ---> 2e5cde04aad9
Step 9/9 : CMD ["catalina.sh", "run"]
 ---> Running in b671825da623
Removing intermediate container b671825da623
```

### Run Container with custom Image
After we completed our image building, it's time to run the container. Now we don't need the hundreds of volume mounts and run commands in the run command since we defined them in the dockerfile and they were already run. All we need to do right now is to run the image. We expose Port 8080 on 8080 on the host for simplicity purposes.

```Bash
-> ~ sudo docker run -it -p 8080:8080 niklashaiden/customtomcat:0.0.1
Using CATALINA_BASE:   /usr/local/tomcat
Using CATALINA_HOME:   /usr/local/tomcat
Using CATALINA_TMPDIR: /usr/local/tomcat/temp
Using JRE_HOME:        /usr/local/openjdk-11
Using CLASSPATH:       /usr/local/tomcat/bin/bootstrap.jar:/usr/local/tomcat/bin/tomcat-juli.jar
Using CATALINA_OPTS:
NOTE: Picked up JDK_JAVA_OPTIONS:  --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.util.concurrent=ALL-UNNAMED --add-opens=java.rmi/sun.rmi.transport=ALL-UNNAMED
01-Dec-2021 14:37:19.538 INFO
[...]
```

Tomcat is running on the new image: 

![Tomcat Manager with new image](Pasted image 20211201155748.png)

After deploying the application also works normally: 

![Deployed app on container with custom image](Pasted image 20211201155834.png)

# Dockerize Nginx 

## Docker-Compose  

We first define the network in which the containers will run, then the we define the services. 
The services are the container that will be run by Docker-Compose when first starting up. Customtom is the tomcat image we built earlier. It listens on port 8080, which we define below, but with this definition, we don't expose the port to the outside network, only to the network, in which the container is in. nginx is the second service which gets started. 
We use the alpine image since it's lightweight and we don't need the extra tools included in other images. 
We mount the nginx.conf file to the conf.d directory in the container so it gets picked up by nginx and loaded. 
We also mount the cert folder with the key and certificate file we need for ssl. 
At last we define that port 80 and 443 should be open to the network so we can access it.

```yaml
version: "3"
    
networks:
 niklas-public:
    
 services:
   tomcat:
    image: niklashaiden/customtomcat:0.0.1
    container_name: customtom
    restart: always
    networks:
     - niklas-public
    ports:
     - "8080"
   reverse_proxy:
    image: nginx:1.20.2-alpine
    container_name: reverse_proxy_customtom
    restart: always
    networks:
     - niklas-public
    ports:
     - "80:80"
     - "443:443"
    
    volumes:
     - "/home/schueler/nginx-dockerized/config/nginx.conf:/etc/nginx/conf.d/nginx.conf"
     - "/home/schueler/nginx-dockerized/certs:/etc/nginx/certs"
```

### Nginx Config
to access the container, we use the name we defined earlier, since we don't know the IP adress that docker assigns to the tomcat container in our network. The only change I have done from the previous config file was the names for the proxying and the path for the certificate file. 

```Nginx
server {
    listen 80;
    return 301 https://$host$request_uri;
}

server {

    listen 443;
    server_name niklas-public.nvs.lan;

    ssl_certificate           /etc/nginx/certs/niklas-public.nvs.lan.crt;
    ssl_certificate_key       /etc/nginx/certs/niklas-public.nvs.lan.key;

    ssl on;
    ssl_session_cache  builtin:1000  shared:SSL:10m;
    ssl_protocols  TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers HIGH:!aNULL:!eNULL:!EXPORT:!CAMELLIA:!DES:!MD5:!PSK:!RC4;
    ssl_prefer_server_ciphers on;
    client_max_body_size 300M;
    access_log            /var/log/nginx/jenkins.access.log;

    location / {

      proxy_set_header        Host $host;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        X-Forwarded-Proto $scheme;

      # Fix the “It appears that your reverse proxy set up is broken" error.
      proxy_pass          http://customtom:8080/;
      proxy_read_timeout  90;

      proxy_redirect      http://customtom:8080/ https://niklas-public.nvs.lan;
    }
  }
```

### Running the setup

```bash
-> nginx-dockerized docker-compose up

Starting customtom ... done

Starting reverse_proxy_customtom ... done

Attaching to reverse_proxy_customtom, customtom

customtom | NOTE: Picked up JDK_JAVA_OPTIONS: --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.util.concurrent=ALL-UNNAMED --add-opens=java.rmi/sun.rmi.transport=ALL-U

NNAMED

reverse_proxy_customtom | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration

reverse_proxy_customtom | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/

reverse_proxy_customtom | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh

reverse_proxy_customtom | 10-listen-on-ipv6-by-default.sh: info: IPv6 listen already enabled

reverse_proxy_customtom | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh

reverse_proxy_customtom | /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh

reverse_proxy_customtom | /docker-entrypoint.sh: Configuration complete; ready for start up

reverse_proxy_customtom | 2021/12/11 16:26:35 [warn] 1#1: the "ssl" directive is deprecated, use the "listen ... ssl" directive instead in /etc/nginx/conf.d/nginx.conf:14

reverse_proxy_customtom | nginx: [warn] the "ssl" directive is deprecated, use the "listen ... ssl" directive instead in /etc/nginx/conf.d/nginx.conf:14

reverse_proxy_customtom | 2021/12/11 16:26:35 [notice] 1#1: using the "epoll" event method

reverse_proxy_customtom | 2021/12/11 16:26:35 [notice] 1#1: nginx/1.20.2

reverse_proxy_customtom | 2021/12/11 16:26:35 [notice] 1#1: built by gcc 10.3.1 20210424 (Alpine 10.3.1_git20210424)

reverse_proxy_customtom | 2021/12/11 16:26:35 [notice] 1#1: OS: Linux 5.4.0-88-generic

reverse_proxy_customtom | 2021/12/11 16:26:35 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576

reverse_proxy_customtom | 2021/12/11 16:26:35 [notice] 1#1: start worker processes

reverse_proxy_customtom | 2021/12/11 16:26:35 [notice] 1#1: start worker process 24

customtom | 11-Dec-2021 16:26:37.338 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server version name: Apache Tomcat/9.0.55
[...]
```

After deploying the test application in the same manner as before: 

![Deployed App on dockerized stack](Pasted image 20211211172847.png)


# Docker Swarm 
## Export Docker and send to Dominik Weber Image 

To use the same image on both Swarm Servers (Manager and Worker) we have to send Dominik Weber, which is the worker in this case, my image so I can use it to scale up the Containers on both nodes. We could also upload the image to Docker Hub but this would be too much of a hassle, so we sent a exported tar version of the docker image via the scp command instead.

```Bash
schueler in u2004-5bhif-6 in ~/tomcatimage
> docker save -o customtom.tar niklashaiden/customtomcat:0.0.1


schueler in u2004-5bhif-6 in ~/tomcatimage took 4s
> scp customtom.tar schueler@10.139.0.15:/home/schueler/customtom.tar
schueler@10.139.0.15's password:
customtom.tar                                                                                       100%  677MB  13.1MB/s   00:51
```


## Initialize Docker Swarm
With Docker Swarm init, we initialize and activate the swarm mode for the Docker Engine. The current Server on which this is done is now the manager. The user is presented with a command for other servers to join in.
```Bash
schueler in u2004-5bhif-6 in ~/nginx-dockerized took 5m53s
> docker swarm init
Swarm initialized: current node (njlm7u8hpkdua7dg9rl403c8n) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-43kjccyib7bbrwmj0aogdc9drzkadrhudtjfteiuzk8xo1msza-cwvuwa36abc6xmpl3tly39yk1 10.139.0.87:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

### Checking connected nodes before other members

This was done before a member joined.

```Bash
schueler in u2004-5bhif-6 in ~/nginx-dockerized
> docker node ls
ID                            HOSTNAME        STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
njlm7u8hpkdua7dg9rl403c8n *   u2004-5bhif-6   Ready     Active         Leader           20.10.11
```

### Dominik Weber joins
Now that Dominik Weber joined my cluster, we have 2 nodes to run containers on in our Swarm network. `u2004-5bhif-18` is the server of Dominik Weber. He joined via the provided command from above. 

```Bash
schueler in u2004-5bhif-6 in ~/nginx-dockerized
> docker node ls
ID                            HOSTNAME         STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
njlm7u8hpkdua7dg9rl403c8n *   u2004-5bhif-6    Ready     Active         Leader           20.10.11
nhp5nqd7zea83tf0f2qc3ib93     u2004-5bhif-18   Ready     Active                          20.10.11
```

### create service
To run a container, we need to create a service. This is done with `docker service create`.  We give the service a name with `--name` and we define the ports on which the should run, with `--publish`. In this case 8081 was chosen since 8080 was used by another container from before. This container is now run on my manager node only. 
```Bash
> docker service create --publish 8081:8080 --name tomcat niklashaiden/customtomcat:0.0.1
image niklashaiden/customtomcat:0.0.1 could not be accessed on a registry to record
its digest. Each node will access niklashaiden/customtomcat:0.0.1 independently,
possibly leading to different nodes running different
versions of the image.

7t3nzeopj9shq3muifu48aots
overall progress: 1 out of 1 tasks
1/1: running   [==================================================>]
verify: Service converged
```

### scale up to 2 containers per node 

To scale up and run the container on both servers, we need to use the `scale` command and provide a container name and the number of containers. In this case, 2 nodes and 4 containers are used, so every nodes gets 2 containers running in parallel.

```Bash
> docker service scale tomcat=4
tomcat scaled to 4
overall progress: 4 out of 4 tasks
1/4: running   [==================================================>]
2/4: running   [==================================================>]
3/4: running   [==================================================>]
4/4: running   [==================================================>]
verify: Service converged
```

Looking at the running containers on my manager node:

```Bash
schueler in u2004-5bhif-6 in ~/tomcatimage
> docker node ps
ID             NAME       IMAGE                             NODE            DESIRED STATE   CURRENT STATE                ERROR     PORTS
p91izb8wfadc   tomcat.1   niklashaiden/customtomcat:0.0.1   u2004-5bhif-6   Running         Running about a minute ago
ujgywdb2fwck   tomcat.2   niklashaiden/customtomcat:0.0.1   u2004-5bhif-6   Running         Running 20 seconds ago

```

Looking at the running containers on the manager node (Dominik Weber):

```Bash
schueler in u2004-5bhif-6 in ~/tomcatimage
> docker node ps u2004-5bhif-18
ID             NAME       IMAGE                             NODE             DESIRED STATE   CURRENT STATE            ERROR     PORTS
zpd1to6ry8r5   tomcat.3   niklashaiden/customtomcat:0.0.1   u2004-5bhif-18   Running         Running 48 seconds ago
d4hsfeajg02j   tomcat.4   niklashaiden/customtomcat:0.0.1   u2004-5bhif-18   Running         Running 48 seconds ago
```

Testing the Swarm Tomcat: 

![Swarm Tomcat running](Pasted image 20211215155041.png)
