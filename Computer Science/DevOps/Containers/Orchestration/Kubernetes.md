<span style="color: #d65d0e">Kubernetes</span> is a container orchestration technology used to orchestrate the deployment and management of hundreds and thousands of containers in a clustered environment.  

Kubernetes is supported on all public cloud services providers like GCP, Azure, and AWS and Kubernetes projects is on of the top ranked projects in GitHub.

>[!info]
><span style="color: #d65d0e">Kubernetes</span> it's an open-source platform written in Go, which was developed by Google and maintained by the <span style="color: #d65d0e">Cloud Native Computing Foundation</span> (CNCF). 

It's also known as "Kates" or K8s. Kubernetes is widely supported by leading cloud providers, many of whom now offer fully managed Kubernetes service. Kubernetes can run in any kind of server, such as on-premise data centers, public, private and hybrid cloud.
##### <strong style="color: #689d6a">Kubernetes Architecture</strong>

A <span style="color:#d65d0e">node</span> or minion is a machine, physical or virtual, on which Kubernetes is installed. Node is a <strong style="color: #d79921">worker machine where containers are launched</strong> by Kubernetes. In other words, user applications run on nodes. Nodes include <span style="color:#689d6a">Pods</span>, and Pods include one or more containers.

A <span style="color:#689d6a">deployment</span> of Kubernetes is called a <span style="color:#d65d0e">Kubernetes cluster</span>, which is a <strong style="color: #d79921">set of nodes grouped together</strong> that runs containerized applications - having multiple nodes helps in sharing load as well. Each cluster has one <span style="color:#d65d0e">master node</span> (the <span style="color:#98971a">Kubernetes Control Plane</span>) and at least one worker node.

The <span style="color:#d65d0e">master</span> is another node with Kubernetes installed in it, and it is configured as a Master, which watches over the nodes on the cluster and it's <strong style="color: #b16286">responsible for the actual orchestration of container on the worker nodes</strong>.

When kubernetes is being installed on a system, it's actually installing the following components: the <span style="color:#98971a">API Server</span>, <span style="color:#98971a">etcd service</span>, <span style="color:#98971a">kubelet service</span>, <span style="color:#98971a">Container Runtime</span>, <span style="color:#98971a">Controller and Schedulers</span>.

The <span style="color:#98971a">Control Plane</span> maintains the intended cluster state by making decisions about the cluster and detecting and responding to events in the cluster. Each node is <strong style="color: white">managed</strong> by the Control Plane and contains the services necessary to run applications.

<span style="color:#98971a">API Server</span> acts as the front end for Kubernetes - the users, management devices, command line interfaces, all talk to the API server to interact with the Kubernetes cluster. <strong style="color: #b16286">All the communication in the cluster utilizes this API</strong>.

<span style="color:#98971a">Etcd</span> is <strong style="color: #d79921">distributed, reliable and highly available key value store</strong> used by Kubernetes to store all data used to manage the cluster. It stores deployment configuration data, defines the state in a <span style="color:#d65d0e">Kubernetes cluster</span>, and the system works to bring the actual state to match the desired state. 

<span style="color:#98971a">Etcd</span> is responsible for implementing locks within the cluster to ensure that there are no conflicts between the master. 

>[!note]
>Kubernetes works towards <strong style="color: #b16286">matching the current state to the desired state</strong>.

The <span style="color:#98971a">kube-scheduler</span> is <strong style="color: #d79921">responsible for distributing work or containers across multiple nodes</strong>. It looks for newly created Pods and assigns them to nodes. It selects the most optimal node according to kubernetes scheduling principles, configuration options and available resources.

The <span style="color:#98971a">controllers</span> are the brain behind orchestration. They are <strong style="color: #d79921">responsible for noticing and responding when nodes, containers or endpoints goes down</strong>. The controllers make decisions to bring up new containers in such cases. 

>[!info]
>The container runtime is the underlying software that is used to run containers. Example: Docker.

<span style="color:#98971a">Kubelet</span> the most important component of a worker node. It's an <strong style="color: #b16286">agent that runs on each node</strong> in the cluster. The agent is <strong style="color: #d79921">responsible for making sure that the containers are running on the nodes as expected</strong>, by providing information about the Pod's health and status.

The <span style="color:#98971a">Kubelet</span> It's also responsible to carry out actions requested by the master on the worker nodes. All the information gathered are stored in a key value store on the master, which is based on the popular <span style="color:#98971a">etcd</span> framework.

The <span style="color:#d65d0e">worker node</span> is where the containers are hosted, like Docker containers for example. The master server has the <span style="color:#98971a">kube-api-server</span> and that is what makes it a master. All the information gathered by the <span style="color:#98971a">Kubelet</span> agent about the worker nodes are stored in <span style="color:#98971a">etcd</span> on the master node. The <strong style="color: #b16286">master also has the control manager and the scheduler</strong>.

<span style="color:#98971a">kubectl</span> <span style="color: #3588E9">--></span> is the Kubernetes command line interface (CLI), stands for <span style="color:#d65d0e">Kube Command Line Tool</span>. It's <strong style="color: #d79921">used to deploy and manage applications on a Kubernetes cluster</strong> to get cluster information, to get status of other nodes in the cluster, inspect and manage cluster resources, view logs, and more. Key commands types: Imperative commands, Imperative object configuration and Declarative object configuration.
- <code style="color:#98971a">kubectl [<span style="color:#689d6a">command</span>] [<span style="color:#689d6a">type</span>] [<span style="color:#689d6a">name</span>] [<span style="color:#689d6a">flags</span>]</code>
	- [<span style="color:#689d6a">command</span>] <span style="color: #3588E9">=</span> any operation to be performed (create, get, apply, delete)
	- [<span style="color:#689d6a">type</span>] <span style="color: #3588E9">=</span> resource type (pod, deployment, replica set)
	- [<span style="color:#689d6a">name</span>] <span style="color: #3588E9">=</span> resource name (if applicable)
	- [<span style="color:#689d6a">flags</span>] <span style="color: #3588E9">=</span> special options or modifiers that override default values
- <strong style="color: #d79921">Imperative commands</strong>:
	- Allows to create, update and delete objects directly. Operations should be specified as arguments or flags.
	- They don't provide an audit trail. They also don't use templates, and they can't integrate with change review processes.
	- <span style="color: #3588E9">--></span> ideal for development and test environments.
	- <code><span style="color:#98971a">$ kubectl</span> <span style="color:#689d6a">run</span></code> <span style="color: #3588E9">--></span> used to deploy an application on the cluster. Ex: kubectl run hello-minikybe
	- <code style="color:#689d6a">kubectl cluster-info</code> <span style="color: #3588E9">--></span> to view information about the cluster
	- <code style="color:#689d6a">kubectl get nodes</code> <span style="color: #3588E9">--></span> to list all the nodes of the cluster
	- <code style="color:#689d6a">kubectl get deployments</code>
	- <code style="color:#689d6a">kubectl get pods</code>
	- $ kubectl get po -A --> check the running pods
- <strong style="color: #d79921">Imperative object configuration</strong>:
	- The kubectl command specifies required operations, optional flags, and at least one file name.
	- The specified configuration file specified must contain a full definition of the objects in YAML or JSON format.
	- <code><span style="color:#98971a">$ kubectl <span style="color:#689d6a">create -f pod-definition.yaml</span></span></code>
	- Configuration templates help replicate identical results.
- <strong style="color: #d79921">Declarative object configuration</strong>:
	- Stores configuration data in files.
	- Operations are identified by <code style="color:#98971a">kubectl</code> not the user.
	- Works on directories or individual files
	- <code><span style="color:#98971a">$ kubectl <span style="color:#689d6a">apply -f nginx/</span></span></code>
	- The user isn't required to perform any operations, since they are performed by the system automatically.
	- Configuration files define desired state, and Kubernetes actualizes the state.
	- <span style="color: #3588E9">--></span> ideal method for production system.

>[!example] Creating a Resource
> <code style="color:#98971a">$ kubectl <span style="color:#689d6a">apply -f nginx.yaml</span></code>
> <code style="color:#98971a">$ kubectl <span style="color:#689d6a">get deployment my-dep</span></code>

>[!info]
>A <code style="color:#98971a">kubectl</code> <strong style="color: white">context</strong> is a <strong style="color: #b16286">group of access parameters</strong>, including a cluster, a user, and a namespace.
###### Container D

Kubernetes introduced an interface called <span style="color:#d65d0e">Container Runtime Interface</span> (CRI), which allowed any vendor to work as a container runtime for Kubernetes as long as they adhere to the OCI standards. 

<span style="color:#d65d0e">OCI</span> stands for <span style="color:#d65d0e">Open Container Initiative</span>, and it consist of an image spec and a runtime spec.
- <span style="color:#98971a">image spec</span> <span style="color: #3588E9">--></span> specification on how an image should be built
- <span style="color:#98971a">runtime spec</span>  <span style="color: #3588E9">--></span> defines the standards in how any container runtime should be developed

>[!note]
>In version 1.24 Kubernetes removed the support for Docker.

<strong style="color: #b16286">Container D is CRI compatible</strong> and can work directly with kubernetes as all other runtime, which can be used as a runtime on its own, separate from Docker.

`ctr` <span style="color: #3588E9">--></span> command line tool for Container D, made for debugging container D.
- `ctr images pull docker.io/library/redis:alpine redis` --> to pull images
- `ctr run docker.io/library/redis:alpine redis` to run a container 

`nerdctl` <span style="color: #3588E9">--></span> node control tool (CTL) which is better alternative for Container D than ctr. It's very similar to Docker, and supports all of the options that Docker supports.
- `nerdctl run` <span style="color: #3588E9">--></span> name redis redis:alpine
- `nerdcl run` <span style="color: #3588E9">--></span> name webserver -p 80:80 -d nginx

`crictl` <span style="color: #3588E9">--></span> command line tool used to interact with CRI compatible container runtime. It's maintained and developed by the kubernetes community. It works across all the different container runtimes and it's used to inspect and debug container runtime Obs: no ideally used to create container unlike Docker or the `nerdctl`.
- `crictl pull busybox`
- `crictl images`
- `crictl ps -a`
- `crictl ecec -t <tag> ls`
- `crictl logs`
- `crictl pods `
##### <strong style="color: #689d6a">Kubernetes Concepts</strong>

Kubernetes does not deploy containers directly on the worker nodes, containers are encapsulated into a Kubernetes object known as pods.

>[!info]
><span style="color:#d65d0e">Kubernetes objects</span> are persistent entities. Examples: Pod, Namespace, Replica Sets and Deployments. They consist of two main fields: object spec and status.
###### <strong style="color:#98971a">PODs</strong>

<span style="color:#98971a">Pod</span> <span style="color: #3588E9">--></span> single instance of an application. It's the <strong style="color: #b16286">smallest deployable compute object</strong> that can be created in Kubernetes and higher-level abstraction to run workloads.

To scale up an application in Kubernetes, a new Pod is created altogether with a new instance of the same application. Additional Pods can be deployed on a new node in the cluster. <span style="color: #3588E9">--></span> It will have a new node added to the cluster to expand the clusters physical capacity.

Pods <strong style="color: #d79921">usually have a 1 to 1 relationship with containers</strong> running an application. To scale up new Pods are created, and to scale down an existing Pod is deleted. 

>[!note]
>Additional containers <strong style="color: #d79921">are not added</strong> to an existing Pod to scale the application. 

>[!example] Multi-Container PODs
>A single pod can have multiple containers, except for the fact that they're usually not multiple containers of the same kind. 
>There are cases that it needs a helper container that might be doing some kind of supporting task for the web application, such as processing a user, enter data processing a file uploaded by the user, etc. <span style="color: #3588E9">--></span> these helper containers should live alongside the application container.
>The two containers can also communicate with each other directly by referring to each other as local host since they share the same network space, plus they can easily share the same storage space as well.

<span style="color:#98971a">minikube</span> <span style="color: #3588E9">--></span> is a software (utility) that allows developers to run a Kubernetes cluster on the local machine. It's a very useful tool that helps in the process of learning Kubernetes.
- all the basic operations can be done on a <span style="color:#98971a">minikube</span> cluster
- it uses the <span style="color:#98971a">kubectl</span> tool to manage the cluster
- <code style="color:#689d6a">minikube start --driver=virtualbox</code>
- <code style="color:#689d6a">minikube status</code>

>[!example] <span style="color:#98971a">kubectl</span> - Creating Pods
>The `kubectl` command deploys a Docker container by creating a Pod. It first creates a Pod automatically and deploy an instance of the nginx Docker image.
>```shell 
>kubectl run nginx --image=nginx
>kubectl describe pod nginx  # shows information about the pod
>kubectl get pods -o wide # to check status of the pod
>```
>While the Pod name could be anything, the image name has to be the name of an image available at Docker Hub or any other container registry
###### <strong style="color:#98971a">ReplicaSets</strong>
###### <strong style="color:#98971a">Deployments</strong>

Kubernetes uses <span style="color: #d65d0e">YAML files</span> as inputs for the <strong style="color: #b16286">creation of objects</strong> such as pods, replicas, deployments, services, etc. All of these follow a similar structure. A Kubernetes definition file <strong style="color: #b16286">always contains four top level fields</strong>: <span style="color: #d65d0e">apiVersion, kind, medata and spec.</span>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myaapp-pod
  labels:
    app: myapp
    tier: front-end
spec:
  containers: # List/Array 
    - name: nginx-container # dash indicates that this is the first item in the list
      image: nginx
```

> Note: A YAML file is used to represent data, which in Kubernetes is called Kubernetes manifests. Every manifest must define an API version to use.

- <span style="color: #d65d0e">apiVersion</span> <span style="color: #3588E9">--></span> the version of the Kubernetes API that will be used the object. <strong style="color: #d79921">Some possible values are</strong>: `v1` for Pod and Service, `apps/v1` for ReplicaSet and Deployment.
- <span style="color: #d65d0e">kind</span> <span style="color: #3588E9">--></span> refers to the type of the Kubernetes object that will be created
- <span style="color: #d65d0e">metadata</span> <span style="color: #3588E9">--></span> data about the object, like its name, labels, etc. It's in the form of a dictionary.
- <span style="color: #d65d0e">spec</span> <span style="color: #3588E9">--></span> provides additional information to Kubernetes pertaining to that object, it's going to be different for different objects. It's also a dictionary, so each property must be added under it

> For any Kubernetes definition file the spec definition defines what's inside the object that will be created.

