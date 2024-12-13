<span style="color: #d65d0e">Kubernetes</span> is a container orchestration technology used to orchestrate the deployment and management of hundreds and thousands of containers in a clustered environment.  

Kubernetes is supported on all public cloud services providers like GCP, Azure, and AWS and Kubernetes projects is on of the top ranked projects in GitHub.

>[!info]
><span style="color: #d65d0e">Kubernetes</span> it's an open-source platform written in Go, which was developed by Google and maintained by the <span style="color: #d65d0e">Cloud Native Computing Foundation</span> (CNCF). 

It's also known as "Kates" or K8s. Kubernetes is widely supported by leading cloud providers, many of whom now offer fully managed Kubernetes service. Kubernetes can run in any kind of server, such as on-premise data centers, public, private and hybrid cloud.

<strong style="color: #689d6a">Kubernetes Architecture</strong>

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

<span style="color:#98971a">Kubelet</span> the most important component of a worker node. It's an <strong style="color: #b16286">agent that runs on each node</strong> in the cluster. The agent is <strong style="color: #d79921">responsible for making sure that the containers are running on the nodes as expected</strong>, by providing information about bout the Pod's health and status.

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

>[!info]
>A <code style="color:#98971a">kubectl</code> <strong>context</strong> is a <strong style="color: #b16286">group of access parameters</strong>, including a cluster, a user, and a namespace.


[[ minikube ]]<span style="color: #3588E9"> --></span> is a software that allows developers to run a Kubernetes cluster on the local machine. It's a very useful tool that helps in the process of learning Kubernetes.

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

<strong style="color: #689d6a">Kubernetes Concepts</strong>