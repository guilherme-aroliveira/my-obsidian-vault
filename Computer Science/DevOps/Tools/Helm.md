<span style="color:#98971a">Helm</span> is the package management system for Kubernetes, it simplifies micro services management on K8s.

<strong style="color: #d79921">Helm components:</strong>

- <span style="color:#d65d0e">Chart</span> <span style="color: #3588E9">--></span> a Helm package which contains all of the recourse definitions necessary to run an application, tool, or service inside of a kubernetes cluster.
	- it contains the template and configuration which is required for the kubernetes resource execution --> templates are converted into YAML files
	- when helm chart is executed, Helm executes the resource on the Kubernetes cluster.
	- instead of writing separate yaml files for each application, the user can simply create a helm chart and let Helm deploy the application to the cluster.
	- it can be customized when deploying it on different kubernetes cluster.
	- Helm CLI commands can be executes on helm charts
- <span style="color:#d65d0e">Repository</span> <span style="color: #3588E9">--></span> the place where charts can be collected and shared.
- <span style="color:#d65d0e">Release</span> <span style="color: #3588E9">--></span> an instance of chart running in a Kubernetes cluster. One chart can often be installed many times into the same cluster. And each time it is installed, a new release is created.

<strong style="color: #d79921">Helm Workflow</strong>
- <span style="color:#d65d0e">Load Charts and Dependencies</span> <span style="color: #3588E9">--></span> <span  style="color: #689d6a">Parse the Values to yaml file</span> <span style="color: #3588E9">--></span> <span style="color:#98971a">Generate the yamls</span> <span style="color: #3588E9">--></span> <span style="color: #d79921">Parse yaml to Kube Object & Validate</span> <span style="color: #3588E9">--></span> <span style="color: #b16286">Send Validates yamls to K8s</span>

<span style="color: #3588E9">--></span> When a helm command is triggered, it  downloads the chart which have the templates.

>[!example] custom values - YAML file
>```yaml
>auth:
>  database: "helm_training"
>  password: "Test1234"
>  username: "custom_usr"
>  rootPassword: "RootPass123"
>```
>To supply values to a helm chart:
>```shell
>helm install -n database --values values.yaml my-mariadb chart --version 11.4.0
>```
###### <span style="color: #d79921">Helm commands</span>

- `helm repo list` -->  check the installed repo
- `helm repo add <name> <url>` --> add helm repository
- `helm repo update` --> get the latest version of the charts
- `helm repo remove <name>` --> deletes a helm repository
- `helm search repo <name>` --> search for a repository
- `helm search hub <name>` -->  search for the artifact
- `helm show` --> show information of the chart
	- helm show chart bitnami/kube-state-metrics --> chart name
	- helm show values bitnami/kube-state-metrics > values.yaml --> redirect the output to a file
- `helm lint <chart_name>` --> validate the helm chart
- `helm delete challenge-metrics-server -n challenge` --> remove the chart
- `helm install <name> <chart>` --> install a deployment
	- `.` --> to install on the current directory
	- `-n` --> to inform the namespace name
	- `--dry-run` --> execute the four stages of the deployment workflow. It helps to validate the configuration before deploy to the cluster.
	- `--wait` --> wait for the successful installation of the Pod
	- `--timeout` --> override the default timeout
- `helm lint` --> to validate a chart
- `helm ls -n metrics` --> check the deployment of the chart
- `helm templates` --> generates the yaml files for each kubernetes object
- `helm list` --> show the number of deployments
	- `--a-namespace` or `A` --> show deployments across the namespace
- `helm status <deployment_name>` --> show the deployment details
- `helm get` --> get more details about a kubernetes object
	- `--revision` --> to show a specific revision
	- Ex: `helm get nodes my-mariadb`
- `helm history` --> show the history of a revision
	- Ex: `helm history my-mariadb -n database`
- `helm upgrade` --> upgrades a chart, apply to the cluster.
	- `--atomic` --> automatically rollback a previous version of a deployment
- `helm uninstall` --> removes a deployment
	- `--keep-history` --> to keep the previous release (maintain the secrets)
- `helm rollback` --> restore a revision
	- Ex: `helm rollback mymariadb 3 -n database`
###### <span style="color: #d79921">Custom charts</span>

Each Helm Chart contains a predictable set of directories and files, and Helm provides a basic template for these, that can be generated from the command line.

```shell
# To generate a boilerplate Helm chart template
helm create <chart_name>
```

The custom Helm charts have the following directory structure:

```text
my_chart
├── Chart.yaml
├── charts/ 
├── templates/   
│	├── Notes.txt
│	├── _helpers.tpl
│	├── deployment.yaml
│	├── hpa.yaml
│	├── service.yaml
│	└── tests/
└── values.yaml
```

`Chart.yaml` <span style="color: #3588E9">--></span> chart that defines the structure of the chart, contains the metadata of the deployment. 

>[!example] Chart.yaml
>```yaml
>apiVersion: v2
>name: climas-front
>description: A Helm chart for Kubernetes
>home:  home address of the engine site
>source: 
>keywords:
>  - "a"
>  - "b"
>maintainers:
>  - name: ""
>  - email: ""
>type: application
>```
>The fields home, source, keywords and maintainers aren't default fields, but are good to be added to the yaml file.
>
>The type `library` chart is basically used for the utility or reusable code (libraries), and it can't be directly deployable. The `library` chart won't contain the templates, but only the reusable code functions.

`charts/` <span style="color: #3588E9">--></span> charts which will be implement at runtime 

`templates/` <span style="color: #3588E9">--></span> contain the YAML files which define the resources that will be deployed on the Kubernetes cluster.
- `_helper.tpl` <span style="color: #3588E9">--></span> contains the functions that the template files use to generate the values within the YAML files for the kubernetes. These functions are used by the yaml files to generate the final deployable YAML on the Kubernetes.
- `deployment.yaml` <span style="color: #3588E9">--></span> main file of the chart, which will deploy all the Kubernetes resources. It uses a template syntax, driven by the go language.

>[!example] deployment.yaml
>```yaml
>apiVersion: apps/v1 # static content
>kind: Deployment
>metadata:
>  name: {{ include "my-chart.fullname" . }} # dynamic content
>```
>`{{ }}` <span style="color: #3588E9">--></span> template actions, the content within these are dynamic, which will be resolved at a runtime

`values.yaml` --> provides the dynamic values for the custom chart. It contain the default values for a helm chart. This file will supply the value to the template.
- The variables of the template will be resolved at runtime from the content which are defined within the `values.yaml` file.
- `image` --> contain the data that will be deployed as a part of a pod.

>[!example] values.yaml
>```yaml
>image:
>  repository: nginx
>  pullPolicy: IfNotPresent 
>```
>IfNotPresent --> if the image isn't present on the kubernetes cluster, than the image won'þ be pulled.  
>
>Always --> every time that a deployment is executed, it will download the image and run it.

To package the custom chart:

>[!example] 
>```shell
>helm package my-chart/ -d /root/ # the package will be deployable on all environments without any dependency
>```
>`-d` --> to save the chart in another location
>`-u` --> chart will download the latest version of the dependencies.
>

Every time when a deployment is upgraded, Helm will restore the previous state data (revision history) in a secret in Kubernetes. It creates a new secret for each revision that are stored in the encoded format.

If a deployment is uninstalled, it will also delete all the previous revisions --> it's important to keep history of the deployments. Helm can restore (rollback) the application from any state if the release history is available.

Obs: always use atomic with your upgrade

To rollback to the most recent version:

```shell
helm rollback first-chart
```
###### <span style="color: #d79921">Helm Templates</span>

To write a custom template, it must use the same template language, but it doesn't have to be the go language. 

To execute the template without deploying resources:

```shell
helm template <char_name>
```

`{{ - include }}` --> include the function in the action, if the function is being called inside the template yaml it uses `include`
`{{ .Values.replicaCount }}` --> include the values files in the action, if the things are being red from values, it uses `Values`.
`{{ . }}` --> to call any object in the template
`{{ .Values.replicaCount }}` --> `replicaCount` is a direct child of the Values. 
`{{ .Chart.keywords}}` --> calling values from the `Chart.yaml` file
`{{ | }}` --> pipe function, used to chain the functions available in the go and it supply the first function output as the input to the next function. 
`{{ default }}` --> go function

If you want to chain multiple functions, you can use the pipe and the output of the left hand side will be the input for the right hand side function.

`{{ nindent 4 }}` --> provide a new line and indentation to the defined argument.
helm template function list --> to search for functions

Conditions logic syntax:
```yaml
{{- if .Values.customBlock.author.name }}
{{"Custom Value is present" | nindent 4}}
{{- else}}
{{"Custom value boolean is false" | nindent 4}}
{{- end}}

{{- if not .Values.autoscaling.enabled }}
replicas: {{ .Values.replicaCount }}
{{- end }}
```

Typecast
```yaml
metadata:
# convert the object into yaml
  {{- with .Values.podAnnotations }}
  annotations:
    {{ - toYaml . | nintend 8 }}
    # with -> also supports else conditions
    {{- else}}
    {{"Hi, I am without with Block" | nindent 4}}
  {{- end }}
```

variables
```ymal
{{ $myvar := true }}
{{- if $myVar }}
{{"Hi, i am with Variable True"}}
```

range will iterate over the value.
```shell
{{- range .Values.customBlock.author.name }}
author:
  - {{ . }}
{{- end }}

images:
{{- range $key,$value := .Values.image}}
  {{$key}}: {{$value | quote}}
{{- end }}
```

Adding dependencies - `Chart.yaml`
```yaml
dependencies:
  - name: mysql # chart
    version: 9.4.5
    repository: "https://..." # complete URL
```
Every chart has a version
the helm install will download and install the dependency. So you can add a number of dependency.
`helm dependency update <chart_name>` --> update the dependencies
`helm install <template_name> /root/HELM/create_charts/my-chart` --> to install the dependencies and the application





. kube-state-metrics package collects data from the Kube APIService about objects like, Nodes, Deployments, Pods and ConfigMaps.
View CPU and memory usage of nodes and pods.

Initialize bitname Helm chart repo:
    
    helm repo list --> check the installed repo
    
    kubectl create ns metrics
    
    helm install kube-state-metrics bitnami/kube-state-metrics -n metrics
    
To see the data that kube state metrics is collecting, forward the servie from the kubernetes cluster of a port of the computer, to acces from a browser.

    kubectl port-forward svc/kube-state-metrics 8080:8080

--> helm provides multiple commands that allow us to inspect a third party chart from the command line.

`helm upgrade kube-state-metrics[release] bitnmae/kube-state-metrics[chart] --version[flag] 0.4.0 -n metrics` --> to upgrade chart

--> metrics server is essencial for collecting usage data for a cluster. And it will help montir the health of a kubernetes node and pods.

. Information stored under the data map, athat string data in the secrets manifest, the data must be encoded with base 64.

    echo -n 'admin' | base64 --> encode the string

To add the version number of the chart and the end of the configmap name:

    apiVersion: v1
    kind: ConfigMap
    metadata:
        name: first-chart-configmap-{{.Chart.Version}}
    data:
        port: 8080

. The if/else statement is a Helm directive and each part of the statement, begin and end with double curly bracers

    data:
        port: 8080
        {{if eq .Values.env "staging"}}
        allowTesting: "true"
        {{else}}
        allowTesting: "false"
        {{end}}
