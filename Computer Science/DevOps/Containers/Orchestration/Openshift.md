<span style="color: #d65d0e">Openshift</span> is an enterprise-ready Kubernetes container platform built for an open hybrid cloud strategy, developed by Red Hat.

Besides container orchestration, it provides additional tooling around the complete lifecycle of applications, from build, to CI/CD, to monitoring and logs.

Just like a Fedora distribution of Linux, OpenShift is a distribution of Kubernetes, building on its foundational capabilities.

<span style="color: #3588E9">--></span> OpenShift is used as an extension of Kubernetes to provide a more robust and comprehensive platform for containerized applications.

Openshift is a premiere platform for running micro services.

It orchestrates containerized workloads.

Microservices with OpenShift can easily integrate with serverless technologies.

Benefits: Enables simplified microservices development and deployment; Enables use of third-party software to fill gaps without requiring development of an entire solution.

A <strong style="color: #b16286">Build confguration file</strong> (BuildConfig) <strong style="color: #b16286">defines</strong> the <strong style="font-weight: 600">build strategy and input sources</strong>.

- Commonly <strong style="font-weight: 600">used</strong> <strong style="color: #b16286">Build strategies</strong> are: <span style="color: #98971a">Source to Image (S2I)</span>, <span style="color: #98971a">Docker</span> and Custom.
	- <span style="color: #98971a">Source to Image (S2I)</span>
		- Is a tool for building reproducible container images
		- Injects application source into a container image to produce a ready-to-run image
		- Eliminates using a Dockerfile
		- Go from Source to Image in one step
		- OpenShift includes predefined builder images
	- Custom
		- The developer must define and create his own builder image
		- Custom builder images are Docker images that contain logic to transform inputs ino expected outputs.
		- Custom builds are only available to cluster administrators

A build input source provides content for builds. The following build inputs can be used, listed in order of precedence: Inline Dockerfile definitions, Content extracted from existing images, Git repositories, Binary (or Local) inputs, Input secrets, and External artifacts.

><strong style="color: ">Note:</strong> multiple inputs can be combined into a single build. And, an inline Dockerfile takes precedence and overwrites any external Dockerfile.

An <span style="color: #d65d0e">ImageStream</span> is an abstraction for referencing container images within OpenShift. It continuouusly creates and updates containers images, but does contain actual image data but is merely a pointer <span style="color: #3588E9">--></span> points to images stored in internal and external registries, or to other ImageStreams.

A <strong style="font-weight: 600">single</strong> ImageStream can <strong style="font-weight: 600">consist of many different tags</strong> such as <strong style="color: #b16286">latest</strong>, <strong style="color: #b16286">dev</strong> and <strong style="color: #b16286">test</strong>. And each tag points to a certain image in a registry.

<span style="color: #3588E9">--></span> An ImageStream provides a trigger capability that automatically invokes builds and deployments when a new version of an image is available.

Red Hat Marktplace --> provides a central location to try, buy, deploy and manage software certified for OpenShift environments.

<strong style="color: #d79921">Openshift Architecture</strong>:

<strong style="color: #d79921">Types of triggers</strong>:

<strong style="color: #d79921">Operators</strong>:

<strong style="color: #d79921">Istio service mesh</strong>

<strong style="color: #d79921">Deploy microservices with OpenShift</strong>:


. Red Hat Openshift is an enterprise-ready Kubernetes container platform build for an open hybrid cloud strategy. Is provides a consistent application platform to manage hybrid-cloud, multicloud, and edge deployments.

. Its build on Linux, containers and automation. It provides full-stack automation and self-service provision for efficient development and deployment.

. Kubernetes is a crucial component of Openshift.

. OpenShift is used as an extension fo kubernetes to provide a more robust and comprehensive container platform.

- openshift features: scalable, flexible, open source, portable containers, enchanced developer experience, automatred install and upgrades, automation and stremlining, edge architecture support, mini cluster management, advanced security and compliance, persistent storage, robust partner ecosystem.

. openshift rus on top of a Kubernetes cluster, with object data stored in the etcd key-value store. It has a microservices-based architecture.
services: Rest APIs and Controllers.
Rest APIs --> expose each of the core objects
Controllers --> Read REST APIs, apply changes to other objects, report status or write back ot the object, maintain the cluser desired state.

openshift features adds:
 . source code management, build, and deployments for developers
 . managing and promoting images at scale as they flow through the system
 . application management at scale
 . team and user teacking management of a large developer organization
 . networking infrastructure that supports the cluster

. In an openshift environment the kubernetes master runs on Red Hat Enterprise Linux CoreOS, while worker nodes support Enterprise Linux.

. OpenShift CLI (oc) is the most common CLI tool to perform end-to-end operations.

. Builds --> a build is the process of trasnforming inputs into a resultant object. For example, trasnforming source code to a container image.
A build requires a configuration file (BuildConfig) which defines the build strategy and input sources.

. Common used Build strategies are: Source to Image (S2I), Docker and Custom.

. Build inpust can be used, in order of precedence:
    - Inline Dockerfile definition
    - Content extracted from existing image
    - Git repositories
    - Binary (Local) inputs
    - Input secrets
    - External artifacts

. Multiple inputs can be combined into a single build
. An inline Dockerfile takes precedence and overwrites any external Dockerfile.

. An ImageStrem is an abstration for referecing container images within Openshift. It continuously creates and updates container images, but it does not contain
actual image data but is merely a pointer. Instead, points to images stored in internal and external registries or to other ImageStreams.

. A single ImageStream can consist one many different tags, such as latest, dev and test. And each tag points to a certain image in a registry.
To deploy an application we refer to the imageStram tag, rather than hardcode the registry URL and tag. If the source location changes we will update the image stream
definition, rather than individually updating all the deployments.

. Operators -->

.

The Developer perspective provides workflows specific to developer use cases, such as the ability to create and deploy applications

oc get pods --> List the Pods in this namespace

oc get buildconfigs --> get OpenShift specific objects

oc project --> View the OpenShift project that is currently in use
