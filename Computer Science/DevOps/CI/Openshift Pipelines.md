OpenShift pipeline is <strong style="color: #b16286">cloud-native solution designed to create, manage and optimize CI/CD workflows</strong>. 

It relies on Kubernetes objects to automate deployments. It automates building, testing and deployment of applications in the Kubernetes environment. One of the key foundations of OpenShift Pipelines is the use of [[Tekton]].

OpenShift pipelines introduce additional components and features specific to the OpenShift platform. This platform provides the abstraction layer on top of Tekton that simplify the procedure for the creation, deployment, and management of pipelines at OpenShift.
- Web Console
- Event-based triggers
- Authentication and authorization
- Integration with Openshift service
- Defining pipeline Templates

<strong style="color: white">Benefits</strong>
- seamless integration with [[Kubernetes]] tools, like [[kubectl]], helm, and operators into their CI/CD workflow.
- ability to scale and reuse
- automates the deployment processes across different platforms

<strong style="color: #d79921">Main Concepts</strong>
- include events, triggers, pipelines, tasks, and steps. These concepts form the core building blocks for defining and executing CI/CD workflows.
- introduces the following: resource, condition , pipelinerun, taskrun

<strong style="color: #d79921">GitOps patterns</strong>
- On-Cluster Resource Reconciler pattern
- External Resource Reconciler
	- The synchronization process occurs using Custom Resource Definitions or CRDs that describe the Git repositories and Kubernetes clusters to reconcile.

>[!info]
>Argo CD is a notable solution that adopts the external resource reconciler pattern for its GitOps implementation.

<span style="color: #d65d0e">Openshift GitOps</span> <span style="color: #3588E9">--></span> packaged version of Argo CD designed specifically for OpenShift, providing a seamless GitOps experience within the OpenShift platform.
- step-by-step guide:
	- 1. Install from OperatorHub
	- 2. Launch from the Openshift console
	- Log in using Openshift credentials
	- Start using ArgoCD