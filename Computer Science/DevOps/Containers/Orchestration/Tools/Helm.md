. Helm is the package management system for Kubernetes

. kube-state-metrics package collects data from the Kube APIService about objects like, Nodes, Deployments, Pods and ConfigMaps.
View CPU and memory usage of nodes and pods.

. seach in the Helm Hub

Initialize bitname Helm chart repo:

    helm repo add bitnami URL
    
    helm repo update --> ge thet latest version of the charts
    
    helm repo list --> check the installed repo
    
    kubectl create ns metrics
    
    helm install kube-state-metrics bitnami/kube-state-metrics -n metrics
    
    helm ls -n metrcis --> check the deployment of the chart

To see the data that kube state metrics is collecting, forward the servie from the kubernetes cluster of a port of the computer, to acces from a browser.

    kubectl port-forward svc/kube-state-metrics 8080:8080

helm show --> show information of the chart

    helm show chart bitnami/kube-state-metrics --> chart name
    
    helm show values bitnami/kube-state-metrics > values.yaml --> redirect the output to a file

--> helm provides multiple commands that allow us to inspect a third party chart from the command line.

. helm upgrade kube-state-metrics[release] bitnmae/kube-state-metrics[chart] --version[flag] 0.4.0 -n metrics --> to upgrade chart

    helm delete challenge-metrics-server -n challenge --> remove the chart

--> metrics server is essencial for collecting usage data for a cluster. And it will help montir the health of a kubernetes node and pods.

. Each helm chart contains a predictable set of diretories and files, and Helm provides a template for these, that can be generated from the command line.

    helm creates first-chart --> generates a boilerplate Helm chart template
    
    helm install first-chart . --> install chart on the current directory
    
    helm template first-chart . --> show the changes locally
    
    helm upgrade first-chart . --> apply to the cluster

. Information stored under the data map, athat string data in the secrets manifest, the data must be encoded with base 64.

    echo -n 'admin' | base64 --> encode the string
    
    helm history first-chart --> shows all the different revisions made to the chart
    
    helm roolback first-chart --> to roll back to the most recent version

To add the version number of the chart and the end of the configmap name:

    apiVersion: v1
    kind: ConfigMap
    metadata:
        name: first-chart-configmap-{{.Chart.Version}}
    data:
        port: 8080

{{}} --> template directive

The values.yaml file contains the default values for a helm chart.

. The if/else statement is a Helm directive and each part of the statement, begin and end with double curly bracers

    data:
        port: 8080
        {{if eq .Values.env "staging"}}
        allowTesting: "true"
        {{else}}
        allowTesting: "false"
        {{end}}
