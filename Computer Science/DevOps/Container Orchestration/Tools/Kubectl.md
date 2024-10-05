. Sevice biding manages configuration and credentuals for back-end services while protecting sensitive data. In addition, it makes Service credentiasl available automatically as a Secret.

. Sevice biding consumes the external Service by biding the application to a deployment. Then, the appliation code uses the credentials from the biding and calls the corresponding Service.

    kubectl get secrets ==namespace=default --> shows all the secrets in the kubernetes cluster

        kubectl expose deployment/hello-world --> In order to access the application, we have to expose it to the internet via a Kubernetes Service. This creates a service of type ClusterIP.

    Cluster IPs are only accesible within the cluster. To make this externally accessible, we will create a proxy.

        kubectl proxy

    Ping the application:

        curl -L localhost:8001/api/v1/namespaces/sn-labs-$USERNAME/services/hello-world/proxy

    List images in Container Registry:

        ibmcloud cr images

    Update the deployment to use this version instead:

        kubectl set image deployment/hello-world hello-world=us.icr.io/$MY_NAMESPACE/hello-world:2


kops --> best tool to setup kubernetes on AWS, has AWS integrations automatically
kubeadm --> is an alternative approach, kops is still recommendend (on AWS)

kops --> stands for Kubernetes Operations, it allows to do production grade Kubernetes installations, upgrades and management
only work with mac and linux
