<span style="color: #d65d0e">Kubernetes</span> is a container orchestration technology used to orchestrate the deployment and management of hundreds and thousands of containers in a clustered environment.  

Kubernetes is supported on all public cloud services providers like GCP, Azure, and AWS and Kubernetes projects is on of the top ranked projects in GitHub.

>[!info]
><span style="color: #d65d0e">Kubernetes</span> it's an open-source platform written in Go, which was developed by Google and maintained by the <span style="color: #d65d0e">Cloud Native Computing Foundation</span> (CNCF). 

It's also known as "Kates" or K8s. Kubernetes is widely supported by leading cloud providers, many of whom now offer fully managed Kubernetes service. Kubernetes can run in any kind of server, such as on-premise data centers, public, private and hybrid cloud.

---
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
###### <strong style="color: #d79921">Container D</strong>

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

Kubernetes <strong style="color: #d79921">use YAML files as inputs for the creation of objects</strong>, such as PODs, replicas, deployments, services, etc. All of them follow similar structure.

A Kubernetes <span style="color:#d65d0e">definition file</span> <strong style="color: #d79921">always contain 4 tops level fields</strong>: apiVersion, kind, metadata and spec <span style="color: #3588E9">--></span> top level or root level properties, which are <strong style="color: #b16286">required fields</strong>. 

For any Kubernetes definition file the spec definition defines what's inside the object that will be created.

>[!example] definition.yaml
>```yaml
>apiVersion: v1
>kind: Pod
>metadata:
>  name: myapp
>  labels:
>    app: myapp
>    type: front-end
>spec:
>  containers: # List/Array
>    - name:  nginx-container # dash indicates that this is the first item in the list
>      image: nginx
>```

- <span style="color: #d65d0e">apiVersion</span> <span style="color: #3588E9">--></span> the version of the Kubernetes API that will be used the object. <strong style="color: #d79921">Some possible values are</strong>: `v1` for Pod and Service, `apps/v1` for ReplicaSet and Deployment.
- <span style="color: #d65d0e">kind</span> <span style="color: #3588E9">--></span> refers to the type of the Kubernetes object that will be created
- <span style="color: #d65d0e">metadata</span> <span style="color: #3588E9">--></span> data about the object, like its name, labels, etc. It's in the form of a dictionary.
- <span style="color: #d65d0e">spec</span> <span style="color: #3588E9">--></span> provides additional information to Kubernetes pertaining to that object, it's going to be different for different objects. It's also a dictionary, so each property must be added under it.

>[!note]
>A YAML file is used to represent data, which in Kubernetes is called Kubernetes manifests. Every manifest must define an API version to use.

<span style="color:#689d6a">object spec</span> <span style="color: #3588E9">--></span> provided by the user which dictates an object's desired state.

<span style="color:#689d6a">status</span> <span style="color: #3588E9">--></span> provided by Kubernetes, this describes the current state of the object.

<span style="color:#98971a">StatefulSet</span> <span style="color: #3588E9">--></span> object that manages stateful applications. Manages deployment and scaling of Pods, and provides guarantees about ordering and uniqueness of Pods. 
- a StatefulSet maintains a sticky identity for each Pod request and provides persistent storage volumes for the workloads
###### <strong style="color:#98971a">Pods</strong>

<span style="color:#98971a">Pod</span> <span style="color: #3588E9">--></span> single instance of an application. It's the <strong style="color: #b16286">smallest deployable compute object</strong> that can be created in Kubernetes and higher-level abstraction to run workloads.

To scale up an application in Kubernetes, a new Pod is created altogether with a new instance of the same application. Additional Pods can be deployed on a new node in the cluster. <span style="color: #3588E9">--></span> It will have a new node added to the cluster to expand the clusters physical capacity.

Pods <strong style="color: #d79921">usually have a 1 to 1 relationship with containers</strong> running an application. To scale up new Pods are created, and to scale down an existing Pod is deleted. 

>[!note]
>Additional containers <strong style="color: #d79921">are not added</strong> to an existing Pod to scale the application. 

>[!example] Multi-Container PODs
>A single pod can have multiple containers, except for the fact that they're usually not multiple containers of the same kind. 
>There are cases that it needs a helper container that might be doing some kind of supporting task for the web application, such as processing a user, enter data processing a file uploaded by the user, etc. <span style="color: #3588E9">--></span> these helper containers should live alongside the application container.
>The two containers can also communicate with each other directly by referring to each other as local host since they share the same network space, plus they can easily share the same storage space as well.

>[!example] <span style="color:#98971a">kubectl</span> - Creating Pods
>The `kubectl` command deploys a Docker container by creating a Pod. It first creates a Pod automatically and deploy an instance of the nginx Docker image.
>```shell 
>kubectl run nginx --image=nginx
>kubectl describe pod nginx  # shows information about the pod
>kubectl get pods -o wide # to check status of the pod
>```
>While the Pod name could be anything, the image name has to be the name of an image available at Docker Hub or any other container registry

The `apply` and `create` commands can be used to create a new object. The `-f` option specifies the file name.

```yaml
kubectl apply -f pod.yaml
```
###### <strong style="color:#98971a">Job</strong>

It creates Pods and track its completion process.  

>[!note]
>Jobs are retried until completed
>Deleting a Job will remove the created Pods
>Suspending a Job will delete its active Pods until the Job resumes

A Job can run several Pods in parallel, and a <span style="color:#d65d0e">cronjob</span> is regularly used to create Jobs on interactive schedule

Job it's the final way to deploy more than one Pods at a time. A Job will create one or more Pods and run the container inside of them until it has successfully completed its task.
###### <strong style="color:#98971a">Replication Controller</strong>

To prevent users from losing access to the application, it should have more than one instance or pod running at the same time.

The <span style="color: #98971a">Replication Controller</span> <strong style="color: #d79921">helps to run multiple instances of a single Pod</strong> in the Kubernetes cluster, thus providing high availability. Even if it has single pod, the replication controller can help by automatically bringing up a new pod when the existing one fails.

The Replication Controller <strong style="color: #d79921">ensures that the specified number of pods are running at all times.</strong>

Another reason to use replication controller is to create multiple ports to share the load across them. It spans across multiple nodes in the cluster.

>[!example] Replication Controller
>```yaml
>apiVersion: v1
>kind: ReplicationController
>metadata:
>  name: myapp-rc
>  labels:
>    app: myapp
>    type: front-ned
>spec:
>  template:
>    metadata:
>      # Pod configuration
>  replicas: 3 # define number of replicas
>```
>When the replication controller is created, it first creates the Pod using the pod definition template as many as required.
>```shell
>kubectl create -f rc.definition.yml
>```

>[!note]
>Replication controller is the older technology that is being replaced by replica set
###### <strong style="color:#98971a">ReplicaSets</strong>

The ReplicaSet ensures that a minimum number os replicas are available all the time. It's the new recommended way to set up replication.

The <strong style="color: #b16286">role</strong> of the <span style="color: #98971a">ReplicaSet</span> is to  <strong style="color: #d79921">monitor the pods and if any of them were to fail deploy new ones</strong>. The ReplicaSet is in fact a process that monitors the parts, and it can also manage PODs that were not created as part of the ReplicaSet creation.

The ReplicaSet <strong style="color: #b16286">monitors Pods by using labels as a filter</strong>. The same concept of labels and selectors is used in many other places throughout Kubernetes.

<strong style="color: white">Use Case:</strong>
- monitor existing PODs, if they haven't been created, the ReplicaSet will create them.

>[!example] replicaset-definition.yml
>```yaml
>apiVersion: apps/v1
>kind: ReplicaSet
>metadata:
>  name: myapp-replicaset
>  labels: 
>    app: myapp
>    type: front-end
>    
>spec:
>  template:
>    metadata:
>      name: myapp-pod
>      labels:
>        app: myapp
>        type: front-end
>    spec:
>      containers:
>      - name: nginx-controller
> 	    image: nginx
>  replicas: 3
>  selector:
>    matchLabels:
>      type: front-end
>```
>Changes made to this file are directly applied on the running configuration on the cluster as soon as the file is saved.

The ReplicaSet requires a <span style="color: #d65d0e">selector</span> definition, which helps the ReplicaSet to identify what Pods fall under it <span style="color: #3588E9">--></span> ReplicaSet can also manage Pods that were not created as part of the ReplicaSet creation.

The <span style="color: #d65d0e">labels</span> for the Pod template and for the <span style="color: #d65d0e">matchLabels</span> <strong style="color: #b16286">must be the same</strong>. The <span style="color: #d65d0e">matchLabels</span> selector simply matches the labels specified under it to the labels on the Pod.

>[!example] ReplicaSet - kubectl commands
>```shell
># to replace or update the replica
>kubectl replace -f replicaset-definition.yml 
>
># to edit the replica set definition file
>kubectl edit replicaset replicaset_name (myapp-rs)
>``` 

To update the number of replicas:
- update the number of replicas in the definition file 
- run `kubectl scale --replicas=6 -f replicaset.definition.yml` 
- run `kubectl scale --replicas=6 replicaset(TYPE) mapp-replicaset(NAME)` 
- automatically scaling based on load

>[!note]
>Using the file name as input will not result in the number of replicas being updated automatically in the file.
###### <strong style="color:#98971a">DaemonSets</strong>

<span style="color:#98971a">DaemonSet</span> <span style="color: #3588E9">--></span> object that makes sure that Nodes run a copy of a Pod. 
- as nodes are added to a cluster, Pods are added to the nodes. Pods are garbage collected when removed form a cluster
- if a DaemonSet is deleted, all Pods are removed
- a DaemonSet is ideally used for storage, logs, and monitoring nodes

DaemonSets are like ReplicaSets, as in it helps you deploy multiple instances of pods. But it runs one copy of your pod on each node in your cluster.
Whenever a new node is added to the cluster, a replica of the pod is automatically added to that node. And when a node is removed the pod is automatically removed.

The DaemonSet ensures that one copy of the pod is always present in all nodes in the cluster.

Uses cases: 
- deploy a monitoring agent or log collector on each of your nodes in the cluster -- as it can deploy your monitoring agent in the form of a pod in all the nodes in your cluster.
- kube proxy --> can be deployed as a DaemonSet in the cluster
- networking --> Networking solutions like Vivenet requires an agent to be deployed on each node in the cluster.

Creating a DaemonSet is similar to the ReplicaSet creation process. except that the kind is a DaemonSet. 
Ensure the labels in the selector matches the ones in the pod template.
`kubectl create -f daemon-set-definition.yaml` --> create the DaemonSet
`kubectl gert daemonset` --> to view created daemon sets
`kubectl describe daemonsets monitoring-daemon` --> to view more details

From version 1.12 onwards the DaemonSet uses the default scheduler and node affinity rules to schedule pods on nodes.
###### <strong style="color:#98971a">Deployments</strong>

<span style="color:#98971a">Deployments</span> <span style="color: #3588E9">--></span> higher-level object that provides updates for Pods and ReplicaSets. Deployments run multiple replicas of an application using ReplicaSets and offer additional management capabilities on top of these ReplicaSets.

Examples of Deployments include: the deployment of a replicated application, Pod updates managed by a Deployment, or the scaling up of an application.

it can hep to perform rolling updates and rollbacks and maintain a record of revisions and record the cause of change.

kubernetes objestc that comer higher in the hirarchy. the deployment provides the capability to upgrade the underlyings instances seamslessly usin grolling updates.

The contents of the deployment definition file are exactly similar to the replica set definition file except for the kind which is now going to be deployment.

The deployment automatically creates a replica set. deployments, creates a new Kubernetes object called deployment.

>[!example] Definition - kubectl
>```shell
># to create a deployment
>kubectl create -f deployment-definition.yml
>
># to see all the created objects at once
>kubectl get all
>
># 
>kubectl apply -f deployment-definition.yml
>
>```

When you first create a deployment, it triggers a rollout. A new rollout creates a new deployment revision (revision 1). when the application is upgraded (when the container vversion is updated), a new rollout is triggered and a new deployment revision is created named Revision two. helps us keep track of the changes made to our deployment and enables us to roll back to a previous version of deployment if necessary.

`kubectl rollout status deplpyment/myapp-deployment` # show the status if the rollout

to show the revisions and history of rollout
`kubectl roolout history deplpyment/myapp-deployment`

There are two types of deployment strategies.
- recreate strategy --> destroy all instances and than deploy new ones of the applications version. This strategy (not default) let the application down and inaccessible to users. 
- rolling updates -->  upgrade instances one after the other

the difference betweem each atrategy can be seen when view the deployent in detail.

if a strategy is not specified while creating a deployment, it will assume it to be rolling updates (default deployment strategy.


A new rollout is triggered and a version of the deployment is created an apply is executed.

Another way to update the container image of a deployment:
`kubectl set image deployemtm/myapp-deployemnt nginx \ nginx-container=nginx:1.9.1`
Obs: will result in the deployment definition file having a different configuration.

upgrades
when a new deployment is created, if first create a replica set automatically, which ins turn creates the number of pods required to meet the number of replicas. When an application is upgraded, the kubernetes deployment objetct creates a new replcia set under the hood, and start deploying the container there, at the same time taking down the pods in the old replcia set, following a rolling update strategy.

control groups are used to constrain resources that are allocated to different processes running on your on your machine.

both Kubelet as well as the container runtime actually need to interface with these control groups to enforce various resource management for pods. So think of things like setting the CPU and memory requests and limits. These are all things that need to be kind of communicated to the cgroups.

if you are using a systemd init system you have to use the systemd cgroup driver.

ps -p 1

Update the deployment to use this version instead:

`kubectl set image deployment/hello-world hello-world=us.icr.io/$MY_NAMESPACE/hello-world:2`
###### <strong style="color:#98971a">Services</strong>

service can be used to expose and application to other applications or users for external access.
a service is only required if the application has some kind of process or database service or web service the needs to be exposed.

. Sevice biding manages configuration and credentuals for back-end services while protecting sensitive data. In addition, it makes Service credentiasl available automatically as a Secret.

. Sevice biding consumes the external Service by biding the application to a deployment. Then, the application code uses the credentials from the biding and calls the corresponding Service.

Cluster IPs are only accesible within the cluster. To make this externally accessible, we will create a proxy.

ClusterIP

kubectl expose deployment/hello-world --> In order to access the application, we have to expose it to the internet via a Kubernetes Service. This creates a service of type ClusterIP.

###### <strong style="color:#98971a">Namespaces</strong>

<span style="color:#98971a">Namespaces</span> <span style="color: #3588E9">--></span> provides a mechanism for isolating group of resources within a single cluster. They isolate and manage applications and services.
- they are ideal when the number of cluster users is large, and it also provides a scope for the names of objects
- each object must have a unique name for the resource type within a namespace
- the default namespace is created automatically by Kubernetes when the cluster is first set up.
- kubernetes creates a set of pods and services for its internal purpose, and to isolate them from the user, kubernetes creates them under the at the kube-system namespace.  
- kupe-public --> a third namespace created automatically by Kubernetes
	- where where resources that should be made available to all users are created.
In a small environment namespace is not necessary, but in case it grows or for productions purposes it should be used. 
Each of these name spaces can have its own set of policies that define who can do what.
You can also assign quota of resources to each of these name spaces. That way, each name space is guaranteed a certain amount and does not use more than its allowed limit.
Example: for the web pod in the default name space to connect to the database in the dev environment or namespace use the servicename.namespace.svc.cluster.local format. --> `mysql.connect("db-service.dev.svc.cluster.local")`

kubectl get pods --namespace=kube-system --> To list pods in another name space
kubectl create -f pods.definition.yaml --namespace=dev --> To create the pod in another name space

ex:
```yaml
apiVersion: v1
kind: Pod
metadata: 
	name: myapp-pod
	namespace: dev
```
good way to ensure your resources are always created in the same name space
a new namesapcae is created like any other object
```yaml
apiVersion: v1
kind: Namespace
metadata: 
	name: dev
```
kubectl create -f namespace.dev.yaml
kubectl create namespace dev
kubectl config  set-context $(kubectl config current-context) --namespace=dev --> to switch to the dev name space permanently - set the name space in the current context to dev.
kubectl get pods --all-namespace --> to view pods in all name spaces

To limit resources in a name space, create a resource quota.
```yaml
apiVersion: v1
kind: ResourceQuota
metadata: 
	name: compute-quota
	namescape: dev
spec:
	hard:
		pods: "10"
		requests.cpu "4"
		requests.memory: 5Gi
		limits.cpu: "10"
		limits.memomry: 10Gi
```


##### <strong style="color: #689d6a">Kubernetes Tools</strong>

###### <span style="color:#98971a">minikube</span>

<span style="color:#98971a">minikube</span> <span style="color: #3588E9">--></span> is a software (utility) that allows developers to run a Kubernetes cluster on the local machine. It's a very useful tool that helps in the process of learning Kubernetes.
- all the basic operations can be done on a <span style="color:#98971a">minikube</span> cluster
- it uses the <span style="color:#98971a">kubectl</span> tool to manage the cluster
- <code style="color:#689d6a">minikube start --driver=virtualbox</code>
- <code style="color:#689d6a">minikube status</code>
###### <span style="color:#98971a">kubectl</span>

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
	- <code><span style="color:#98971a">$ kubectl</span> <span style="color:#689d6a">run</span></code> <span style="color: #3588E9">--></span> used to deploy an application on the cluster.
		-  Ex: `kubectl run hello-minikybe`
	- <code style="color:#689d6a">kubectl cluster-info</code> <span style="color: #3588E9">--></span> to view information about the cluster
	- kubectl get all --> to list all objects
	- <code style="color:#689d6a">kubectl get nodes</code> <span style="color: #3588E9">--></span> to list all the nodes of the cluster
	- <code style="color:#689d6a">kubectl get deployments</code>
	- <code style="color:#689d6a">kubectl get pods</code>
	- <code style="color:#689d6a">kubectl get secrets</code> --> shows all the secrets in the kubernetes cluster
		- Ex: `kubectl get secrets -n database`
		- `kubectl get secrets -n database <secret_name> -o yaml`
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
>
###### <span style="color:#98971a">kubeadm</span>

<span style="color:#98971a">kubeadm</span> <span style="color: #3588E9">--></span> tool that helps to set up a Multi-node cluster using Kubernetes best practices. 
- it needs to have multiple system or VMs provisioned
- one node must be designated as the master and the rest as worker nodes
- it needs a container runtime on the hosts (can be container D)
- the kubeadm tool must be installed on all the nodes
###### <span style="color:#98971a">kops</span>

kops --> stands for Kubernetes Operations, it allows to do production grade Kubernetes installations, upgrades and management

kops --> best tool to setup kubernetes on AWS, has AWS integrations automatically kops is still recommendend (on AWS)
##### <strong style="color: #689d6a">Kubernetes Networking</strong>

<span style="color:#98971a">Ingress</span> <span style="color: #3588E9">--></span> <span style="color: #d65d0e">API object</span> that when combined with a Controller, provides routing rules to manage external users access to multiple services in a Kubernetes cluster. 
- in production, Ingress exposes applications to the internet via port 80 (HTTP) or port 443 (HTTPS).
##### <strong style="color: #689d6a">Scheduling</strong>

Every pod has a field called Node Name that, by default, is not set. Added automatically by Kubernetes. The scheduler goes through all the pods and looks for those that do not have this property set.

It then identifies the right node for the pod by running the scheduling algorithm.
Once identified, it schedules the pod on the node by setting the node name property to the name of the node by creating a binding object.

If there is no scheduler to monitor and schedule nodes, The pods continue to be in a pending state.

without a scheduler, the easiest way to schedule a pod is to simply set the node name field to the name of the node in your pod specification file while creating the pod.

another way to assign a node to an existing pod is to create a binding object and send a POST request to the pod's binding API.

```yaml
apiVersion: v1
kind: Biding
metadata:
	name: nginx
target:
	apiVersion: v1
	kind: node
	name: node02 # name of the node
```

```shell
curl --header "Content-Type:application/json" --request POST --data '{"apiVersion": "v1", "kind": "Biding" ...}'
```

<span style="color:#689d6a">labels</span> <span style="color: #3588E9">--></span> key/value pairs attached to objects. The are intended for identification of objects, which can have the same labels.
- <span style="color: #3588E9">--></span> Labels and selectors are the core grouping method in Kubernetes. They are used to link services and Pods together.

filter and view different objects by different categories, such as to group objects by their type or view objects by application or by their functionality.
stand methods to group thing together. you can group and select objects
using labels and selectors.
For each object, attach labels as per your needs,
like app, function, et cetera.
Then, while selecting, specify a condition to filter specific objects.
For example, app equals app one. app = App1, function = Front-end
```yaml
apiVersion: v1
kind: Pod
metadata:
	name: simple-webapp
	lables:
		app: App1
		function: Front-End
```
pod
select pods with labels --> `kubectl get pods --selector app=App1`
Kubernetes objects use labels and selectors internally to connect different objects together.
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: simple-webapp
  # Labels of the replica set
  labels: 
    app: App1
    function: Front-End
  annotations:
    buildVersion: 1.34
spec: 
  replicas: 3
	# Match the labels defined on the pod
    selector:  
	  matachLabels:
	    app: App1
	template:
	  metadata:
	    labels:
	      app: App1
	      function: Fron-End
```
replica set
Example: When a service is created, it uses the selector defined in the service definition file to match the labels set on the pods in the replica set definition file.

Annotations: annotations are used to record other details for informatory purpose. For example, tool details like name, version, build information, et cetera, or contact details, phone numbers, email IDs, et cetera that may be used for some kind of integration purpose.

Taints and tolerations are used to set restrictions on what pods can be scheduled on a node. taints are set on nodes and tolerations are set on pods.
`kubeclt taint nodes node-name key=value:taint-effect` --> to taint a node
The taint effect defines what would happen to the pods if they do not tolerate the taint.The taint effect defines what would happen to the pods if they do not tolerate the taint.
- noSchedule --> pods will not be scheduled on the node
- PreferNoSchedule --> the system will try to avoid placing a pod on the node, but that is not guaranteed
- NoExecute --> new pods will not be scheduled on the node and existing pods on the node, if any, will be evicted if they do not tolerate the taint.

example: `kubectl taint node1 app=blue:NoSchedule`

To add a toleration to a pod,
```yaml
apiVersion: v1
kind: Pod
metadata:
	name: myapp-pod
spec: 
  containers:
  ...
  tolerations:
  - key: "app"
    operator: "Equal"
    value: "blue"
    effrect: "NoSchedule"
```
all of these values need to be encoded in double codes.

When the pods are now created or updated with the new tolerations, they are either
not scheduled on nodes or evicted from the existing nodes depending on the effect set.

Remember taints and tolerations are only meant to restrict nodes from accepting certain pods.

taints and tolerations does not tell the pod to go to a particular node. Instead, it tells the node to only accept pods with certain tolerations.

best practice is to not deploy application workloads on a master server.
to see this taint --> `kubectl describe noe kubemaster | grep Taint`

node selectors: 
To limit this pod to run on the larger node, we add a new property called node selector. 
```yaml
apiVersion: v1
kind: Pod
metadata:
	name: myapp-pod
spec: 
  containers:
  ...
  nodeSelector: 
    size: Large
```
The key value pair of size and large are in fact labels assigned to the nodes.
The scheduler uses these labels to match and identify the right node to place the pods on.
Obs: To use labels in a node selector like this, you must have first labeled your nodes prior to creating this pod.
to label nodes: `kubectl nodes <node-name> <label-key>=<label-value>`
example: `kubectl label nodes node-1 size=Large`
limitations: We used a single label and selector to achieve our goal here.

node affinity --> to restrict a pod to certain nodes,
The primary purpose of node affinity feature is to ensure that pods are hosted on particular nodes.
provides us with advanced capabilities to limit pod placement on specific nodes.
```yaml
apiVersion: v1
kind: Pod
metadata:
	name: myapp-pod
spec: 
  containers:
  ...
  affinity:
    nodeAffinity: 
      # type of node affinity.
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: In
            values:
            - Large
            - Medium
```

The in operator ensures that the pod will be placed on a node whose label size has any value in the list of values specified.
NotIn operator --> node affinity will match the nodes with a size not set to the defined size.
Exists --> check if the label size exists on the nodes

The type of node affinity defines the behavior of the scheduler with respect to node affinity and the stages in the life cycle of the pod.
There are currently two types of node affinity available
During scheduling is the state where a pod does not exist and is created for the first time.

During execution is the state where a pod has been running and a change is made in the environment that affects node affinity, such as a change in the label of a node.

, a combination of taints, and tolerations, and node affinity rules can be used together to completely dedicate nodes for specific pods.

Resource and requirements
every pod requires a set of resources to run.

If nodes have no sufficient resources available, the scheduler avoids placing the pod on those nodes and instead places the pod on one where sufficient resources are available.

specify the amount of CPU and memory required for a pod --> resource request for a container
Now one count of CPU is equivalent to one vCPU.

Now similarly with memory, you could specify 256 Mi or specify the same value in memory like this 268435456  (whole number).

```yaml
apiVersion: v1
kind: Pod
metadata:
	name: myapp-pod
spec: 
  containers:
  - name:
    resources:
      requests: 
        memory: "4Gi" # Gibibyte
        cpu: 1
      limits:
        memory: "2Gi"
        cpu: 2
```
So when the scheduler gets a request to place this pod, it looks for a node that has this amount of resources available.

1 Ki (Kibibyte) = 1,024 bytes
By default, a container has no limit to the resources it can consume on a node.

Is possible to set a limit for the resource usage on these pods.

A container can use more memory resources than its limit. So if a pod tries to consume more memory than its limit constantly, the pod will be terminated
OOM --> Out of Memory

So by default, Kubernetes does not have a CPU or memory request or limit set.
So this means that any pod can consume as much resources as required on any node and suffocate other pods or processes that are running on the node of resources.

Limit ranges --> ensure that every pod created has come default set, 
define default values to be set for containers in pods that are created without a request or limit specified in the pod-definition files. Its an object
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name:
spec:
  limits:
  - defaults:
    cpu: 500m
    defaultRequest:
      cpu: 500m
    max:
      cpu: "1"
    min:
      cpu: 100m
    type: Container
```

So if you create or change a limit range, it does not affect existing pods.
It'll only affect newer pods that are created after the limit range is created or updated. And finally, is there any way to restrict the

resource quota--> way to restrict the total amount of resources that can be consumed by applications deployed in a Kubernetes cluster
So a resource quota is a namespace level object that can be created to set hard limits for requests and limits.
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: my-resource-quota
spec:
  hard:
    requests.cpu: 4
    requests.memory: 4Gi
    limits.cpu: 10
    limits.memory: 10Gi
```

##### <strong style="color: #689d6a">Logging & Monitoring</strong>

Heapster was one of the original projects that enabled monitoring and analysis features for Kubernetes. Deprecated

Metrics Server slimmed-version of Heapster
You can have one Metrics Server per Kubernetes cluster.
retrieves metrics from each of the Kubernetes nodes and pods, aggregates them, and stores them in memory.

Note that the Metrics Server is only an in-memory monitoring solution
and does not store the metrics on the disk. And as a result, you cannot see historical performance data.

kubelet --> is responsible for receiving instructions from the Kubernetes API master server and running pods on the nodes. The kubelet also contains a sub component
known as the cAdvisor or Container Advisor.

cAdvisor is responsible for retrieving performance metrics from pods and exposing them through the kubelet API to make the metrics available for the Metrics Server.

`minikube addons enable metric-server`
`kubectl create -f deploy/1.8+` -->  deploys a set of pods, services, and roles
to enable Metrics Server to pull for performance metrics from the nodes in the cluster.
`kubectl top node` --> cluster performance can be viewed
`kubectl top node` --> to view performanc metri of pods
`kubectl logs -f event-simulator-pod` -->  view the logs

##### <strong style="color: #689d6a">Cluster Maintenance</strong>
##### <strong style="color: #689d6a">Security</strong>
##### <strong style="color: #689d6a">Storage</strong>

Two ways to handle data storage in Kubernetes:
	- connect the application with a database that is running outside the cluster
	- use Kubernetes <span style="color:#d65d0e">Persistent Volume</span>

app
the redis database is accessed by the voting app and the worker app
the voting app save the vote to the rediz database, and the work app read the vote from the redis database
the worker PostgreSQL database is accessed by the worker app to update it with the total count of votes, and it's also accessed by the result- pap to read the total count of votes to be deployed in the resulting web page in the browser.
the voting app s accessed by the external users, and te result app is alo accessed by the external users to view the results.
The worker app simply read the count of votes from the database and then updates the total count of votes on the PostgreSQL database.
voting app --> python web server - port 80
result app --> node JS server - port 80
redis service - port 6379
PostgreSQL service - port 5432
worker app has no services
these services are not to be accessed outside the cluster, type Cluster IP

vagrant status
vagrant up
vagrant ssh kubemaster