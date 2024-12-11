<span style="color:#98971a">Kubernetes</span> it's an open-source platform written in Go, which was developed by Google and maintained by the <span style="color: #d65d0e">Cloud Native Computing Foundation</span> (CNCF) that allows to manage containerized applications.  It can run in any kind of server, such as on-premise data centers, public, private and hybrid cloud.

<span style="color: #3588E9">--></span>  It's also kwon as "Kates" or K8s. Kubernetes is widely supported by leading cloud providers, many of whom now offer fully managed Kubernetes service.

[[ minikube ]]<span style="color: #3588E9"> --></span> is a software that allows developers to run a Kubernetes cluster on the local machine. It's a very useful tool that helps in the process of learning Kubernetes.

[[Kubectl]]<span style="color: #3588E9">--></span> is the Kubernetes command line interface (CLI), stands for Kube Command Tool Line. Its used to deploy and manage applications on a Kubernetes cluster to get cluster information, to get status of other nodes in the cluster, inspect and manage cluster resources, view logs, and more. Key commands types: Imperative commands, Imperative object configuration and Declarative object configuration.

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

<strong style="color: #d79921">Kubernetes Architecture</strong>