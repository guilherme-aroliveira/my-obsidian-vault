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
