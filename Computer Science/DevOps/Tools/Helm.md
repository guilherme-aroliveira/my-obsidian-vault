<span style="color:#98971a">Helm</span> is a <strong style="color: #d79921">package management system</strong> for Kubernetes, it simplifies micro services management on K8s.

Helm is maintained by the CNCF - The Cloud native Computing Foundation. 

Helm uses a packaging format called <span style="color:#d65d0e">charts</span>. A <span style="color:#d65d0e">chart</span> is a <strong style="color: #d79921">collection of files that describe</strong> a set of Kubernetes <strong style="color: #b16286">resources</strong>. A single chart can deploy an app, or a database. 

A <span style="color:#d65d0e">chart</span> can have dependencies, e.g to install wordpress chart, it needs a mysql chart. 

<span style="color:#d65d0e">Charts</span> use <span style="color:#d65d0e">templates</span> that are typically developed by a package maintainer. They will generate yaml file that kubernetes understands. When a chart is executed, Helm runs the resource on the Kubernetes cluster.

>[!example] Example - template within a chart
>```yaml
>apiVersion: 1
>kind: ConfigMap
>metadata:
>  name: {{ .Release.Name }}-configmap
>data:
>  myvalue: "Hello World"
>  drink: {{ .Values.favoriteDrink }}  
>```
>When a helm command is triggered, it  downloads the chart which have the templates.

Instead of writing separate yaml files for each application, the user can simply create a helm chart and let Helm deploy the application to the cluster.  It can be customized when deploying it on different kubernetes cluster.

A single command is used to install an entire app.

```shell
helm install wordpress
```

A <span style="color:#d65d0e">repository</span> is the place where charts can be collected and shared. 

A <span style="color:#d65d0e">release</span> is an instance of chart running in a Kubernetes cluster. One chart can often be installed many times into the same cluster. And each time it is installed, a new release is created.

<strong style="color: #689d6a">Helm Workflow</strong>
1. Load Charts and Dependencies
2. Parse the Values to yaml file
3. Generate the YAMLs
4. Parse yaml to Kube Object & Validate
5. Send Validates YAMLs to K8s

Helm allows to customize the settings of an app or package by specifying desired values at installed time in the `value.yaml` file. It can define the size of the persistent volume, choose the name of the WordPress website, the admin password, setting for the database engine and so on. 

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

To upgrade an application:

```shell
helm upgrade wordpress
```

Helm keeps track of all the changes made the applications files and that allows to rollback to the previous so-called revision. 

>[!note]
>Helm lets treat the Kubernetes apps as applications instead of just a collection of objects.
###### <span style="color: #689d6a">Helm Components</span>

`helm cli` --> helm command line utility that stays at the local system, is used to perform Helm actions, such as installing a chart, upgrading, rollback, etc..  

charts --> collection of files that contains all the instructions that Helm needs to know to be able to create the collections of objects that is needed in a Kubernetes cluster.

By using charts and adding the objects according to the specific instructions in the carts, Helm install applications into the cluster.

When a chart is applied to the cluster a release is created, which a single installation of an application using a Helm chart.

To keep track of what it did in our cluster, such as the releases that it installed, the charts used, revision states and so on, Helm will need a place to save this data. This data is known as metadata.

`spec:`
`replicas: {{ .Values.replicaCount }} --> templating`
These values are part of another file called as `values.yaml` --> where configurable values are stored, the only file that will be modified to customize the deployent of th application (in case of using a chart from another source).

When a chart is applied to the cluster a release is created. Multiple release can be installed based on the same chart, which can be tracked separately can changed independently. 

Even tough the releases are based on the chart, they're two entirely different entities. For example: a release of the WordPress site for the customers and anther release only for the developers.
###### <span style="color: #689d6a">Helm Charts</span>

Charts are like an instruction manual for it. By reading and interpreting their contents, it then know exactly what is has to do to fulfill as user's request

Every chart has a `chart.yaml` file, that contains information about the chart itself, such as the API version, which could be either V1 or V2. There's also an app version, which is used to specify the version of the application.

>[!example] Chart.yaml
>```yaml
>apiVersion: v2
>appVersion: 5.8.1
>version: 12.1.27
>name: wordpress
>description: Web publishing platform for building blogs and websites
>type: application
>dependencies:
>  - condition: mariadb.enabled
>  - name: mariadb
>  - repository: https://charts.bitnami..com/bitnami
>keywords:
>  - application
>  - blog
>  - wordpress
>maintainers:
>  - email: containers@bitnami
>  - name: Bitnami
> home: 
> icon: 
>```

`apiVersion` <span style="color: #3588E9">--></span> API version of the chart, with this field, Helm 3 can now differentiate between old charts built for Helm 2 and new charts built specifically for Helm 3. The value `v1` indicates that indicates that the chart was build specially for Helm 2.

`appVersion` <span style="color: #3588E9">--></span> version of the application that's inside of the chart. For example, the WordPress version that the chart will deploy, it's for informational purposes only.

`version` <span style="color: #3588E9">--></span> indicates the version of the chart itself. Every chart must have its own version, and it's independent of the version of the app. This helps in tracking changes to the chart itself.

There are two types of charts: application and library. The application is the default type, and library is the type of chart that provides utilities that help in building charts. The `library` chart won't contain the templates, but only the reusable code functions.
###### <span style="color: #689d6a">Chart Structure</span>

Each Helm Chart contains a predictable set of directories and files, and Helm provides a basic template for these, that can be generated from the command line.

>[!example]
>```shell
># To generate a boilerplate Helm chart template
helm create chart_name
>```
>The `create` command creates a skeleton structure of a helm chart.

The custom Helm charts have the following directory structure:

>[!example]
>```text
>my_chart
>├── charts/ ---> Dependency Charts
>├── templates/
>├── Chart.yaml ---> Chart information
>│	├── Notes.txt
>│	├── helpers.tpl
>│	├── deployment.yaml
>│	├── hpa.yaml
>│	├── service.yaml
>│	└── tests/
>├── LICENSE ---> Chart License
>├── README.md ---> Readme file
>└── values.yaml ---> Configurable value
>```

The `Chart.yaml` file defines the structure of the chart, it contains the metadata of the deployment. 

The `charts/` directory contains charts which will be implement at runtime. In case additional charts won't be used, it can be removed.

The `templates/` directory contains the YAML files which define the resources that will be deployed on the Kubernetes cluster.

The `deployment.yaml` is the main file of the chart, which will deploy all the Kubernetes resources. It uses a template syntax, driven by the go language.

Obs: Each time a new release of a helm chart is installed, it must have a different name. To solve this, the name of the deployment must be templatize.

>[!example] Example - deployment.yaml
>```yaml
>apiVersion: apps/v1 # static content
>kind: Deployment
>metadata:
>  name: {{ .Release.Name }}-nginx # dynamic content
>```
>`{{ }}` <span style="color: #3588E9">--></span> template actions, the content within these are dynamic, which will be resolved at a runtime

`{{ .Release.Name }}` <span style="color: #3588E9">--></span> Template Directive, this is in fact the Go Programming Languages template language (Go Template Language). The path of the objects to be accessed stays within the curly brackets. 

>[!note]
>The Template Directive start with a `.` (dot), which refers to the root level or top-level scoped.  

The are other objects similar to `Release.Name`, such as `Release.Namespace`, `Release.IsUpgrade`, `Release.IsIntall`, `Release.Revision`, `Release.Service`. But any values from the `Chart.yaml` file can be refereed, like the API version, or the version or type, keywords, home, etc...

Details of the Kubernetes cluster can also be used as objects in a helm chart, such as `Capabilities.KubeVersion`, `Capabilities.ApiVersions`,`Capabilities.HelmVersion`, `Capabilities.GitCommit`, `Capabilities.GitTreeState`, `Capabilities.GoVersion`

The `values.yaml` file provides the dynamic values for the custom chart. It contain the default values for a helm chart. This file will supply the value to the template.

>[!example] Example - values.yaml
>```yaml
># Default values for nginx-chart
>replicaCount: 2
>image: nginx
>```

<span style="color: #3588E9">--></span> Anything that starts with `Values` is something that refers to the properties defined in the `values.yaml` file.

>[!info]
>For  built-in objects, the second part after the `.` (dot), all starts with a capital letter. But for objects under values, which are defined by the user, are case sensitive. Example: `Values.image`

Obs: anything defined as values should either be passed through the values option or the `--set` option.

The best way to write objects like `images` is to write like a dictionary:

>[!example]
>```yaml
>image: 
>  repository: nginx
>  pullPolicy: IfNotPresent
>  tag: "1.16.0"
>```
>---
>```yaml
>spec:
>  containers:
>    - name: hello-world
>      image: {{ .Values.image.repository }}:{{ .Values.image.tag }}
>```

To remove duplication in a kubernetes objects like `deployment.yaml` file, the repeating lines can be moved to a partial/named template <span style="color: #3588E9">--></span> `_helper.tpl`. 

The `_helper.tpl` file contains the functions that the template files use to generate the values within the YAML files for the kubernetes. These functions are used by the yaml files to generate the final deployable YAML on the Kubernetes. 

>[!info]
>The `_` in the file name, tells helm not to consider this file as a usual template. All files starting with an underscore are skipped from being created or converted into a kubernetes manifest file.

>[!Example]
>```yaml
>{{- define "labels" }}
>	app.kubernetes.io/name: {{ .Release.Name }}
>	app.kubernetes.io/instance: {{ .Release.Name }}
>{{- end }}
>```
>---
>```yaml
>metadata:
>  name:
>  labels:
> 	 {{- template "labels" . }}
>```
>The `.` (dot) transfers the current scope to the template file.

>[!note]
>When lines of code are move to templates, it must have the same indentation or the number of spaces before these lines --> the template statement add the lines there as is.

chart hooks --> extract actions such as backing up a database automatically before the upgrade.  
the pre-upgrade hook runs a predefined action, which could be anything.
post upgrade hook --> runs after the install phase is successful and performs actions configured such as sending an email status

to differentiate the chart hooks from the normal templates file is by using annotations. Annotations are a way to add addioional metadat to an object which may be used by client of Kubernetes to sotre data about that object and performs some kind of actions.

>[!example]
>```yaml
>apiVersion: batch/v1
>kind: Job
>metadata:
>  name: {{ .Release.Name }}-nginx
>  
>  annotations:
>    "helm.sh/hook": pre-upgrade
>    "helm.sh/hook-weight": "5" # hook weight
>```
>This job will run before the upgrade step when a chart is upgraded. 

Multiple hooks can be configured for each step. For example, multiple pre-upgrade hooks configured. To define the order that these hook are executed, weights can be set for each one. 

```yaml
"helm.sh/hook-weight": "5" # hook weight
```

The same weight can be set for multiple hooks, which will be sorted by resource kind, and finally by name in ascending order.

After a job is completed, tre resourtcd for the hook stays as a resource on the cluster,but they can be configured to be cleaned up by setting hook deletion policies

```yaml
"helm.sh/hook-delete-policy": hook-succeded
```

--> The `hook-succeded` deletes the resource after the hook is succefully executed. If the hook fail to execute, the resources won't be deleted --> can be useful to debug.

`hook-failed` deletes the resource even if the hook-failed execution 

`before-hook-creation` the default value if no hook-deleti policy is specified, it deletes the previous resource before a new hook is launched. 

helm upgrade --> verify --> render --> upgrade 
workflow
###### <span style="color: #689d6a">Helm CLI</span>

The `--help` feature can be used for sub commands. 

```shell
helm repo --help
```

To search for a specific chart on the command line:

>[!example]
>```shell
>helm search hub wordpress
>```
>---
>```shell
>helm search repo wordpress
>```
>`hub` refers to the artifact hub, where all the repositories are listed. The `repo` option search in a specific repository.

The application can be deployed in two commands:

```shell
helm repo add <name> <url>
```

```shell
helm install my-release bitnami/wordpress
```

To list all existing releases:

```shell
helm list
```

To remove the app:

```shell
helm uninstall my-release
```

The `helm repo` command be added to add, list and remove or update Helm repositories.

>[!example]
>```shell
># list existing repositories
>helm repo list
>
># update the new release of the chart
>helm repo update
>```

The `--set` options allows to modify some of the default values from `values.yaml`, it can be used multiple times to pass multiple parameters to customize the deployment.

>[!example]
>```shell
>helm install --set wordpressBlogName="Helm Tutorial" my-release bitnami/wordpress
>```
>it overrides the values set in the `values.yaml` file.

The `--values` option allows to pass a custom `values.yaml` file:

```shell
helm install --values custom-values.yaml my-release bitnami/...
```

To pull the chart: 

```shell
helm pull bitnami/wordpress # compressed form
```

```shell
helm pull --untar bitname/wordpress 
```

To install the application:

```shell
hekm install my-release ./wordpress
```

The `--version` option allows to pass a specific version of the helm chart:

```shell
hekm install my-release bitnami/nginx --version 7.1.0 
```

To upgrade a release:

```shell
helm upgrade nginx-release bitnami/nginx
```

>[!info]
>In the upgrade process the old pod gets destroyed, and a new one is created. Helm verifies the files and templates in the chart and then renders the manifest files in their final form. Obs: always use atomic with the upgrade

>[!note]
>Every time when a deployment is upgraded, Helm will restore the previous state data (revision history) in a secret in Kubernetes. It creates a new secret for each revision that are stored in the encoded format.

To see more details about a particular release:

```shell
helm history nginx-release
```

If a deployment is uninstalled, it will also delete all the previous revisions <span style="color: #3588E9">--></span> it's important to keep history of the deployments. Helm can restore (rollback) the application from any state if the release history is available.

To return to a previous revision of a release:

```shell
helm rollback nginx-release 1
```

>[!note] 
>The `rollback` command instead of going back to Revision 1, it creates a new revision with a similar configuration as in Revision 1.

To check if a chart is working as intended: 
linting verify that the chart and the yaml format is corect. this command goes through the files in the chart and validade their format, and looks for erros. It highlights these erros, and informs which file and what line the errors are on.

```shell
helm lint ./nginx-chart # validates the chart
```

verifiyn the template hepls to make sure the the templating part is working as expected. verify wht will be generated, it renders a cgart tempkate locally and siplay the output. the `--debug` flag displays the generated yaml file in the output, 

dry run option --> checks if the works well with kubetnetes itself, it checks the kubernetes manifest format.  execute the four stages of the deployment workflow. It helps to validate the configuration before deploy to the cluster. This just pretends to install the package to the cluster.

```shell
helm install hello-1 ./nginx-chart --dry-run
```

To package a chart:

>[!example]
>```shell
>helm package ./nginx-chart 
>```
>This packages the chart into an archive format `.gz`. The version number is picked from the version within the `Chart.yaml` file.

>[!note]
>Before uploading the apckaged charged is recommended to singing it to make sure users know that the package they are downloading is legit. 

Helm uses a private key that only the developers have access to, and with this key it produces a digital signature and adds to what is called a provenance file. The users downloads the chart and providance file for the signatur. With the public key, they can verify if the chart is corctly signed.

To generate the private key:

```shell
gpg --full-generate-key "Guilherme Oliveira"
```

Obs: Mos lInx distros now uses GnuPG v2, whic storres keys in a differents format that he previous version. To sing charts, Hlems curently prefers the older format. 

To convert the gpg key to the old format:

```shell
gpg --export-secrets-keys > ~/.gnupg/secring.gpg
```

To package the chart with the private key:

>[!example]
>```shell
>helm package --sign --key 'John Smith' --keyring ~/.gnupg/secring.gpg -d /root/nginx-chart
>```
>The `--key` parameter expects to receive either the full name or the email address associate with the key.
>`-d` <span style="color: #3588E9">--></span> to save the chart in another location
>`-u` <span style="color: #3588E9">--></span> chart will download the latest version of the dependencies.

To list key details:

```shell
gpg --list-keys
```

To check the file hash:

```shell
sha256sum nginx-chart-0.1.0.tgz
```

To verify the integrity of the chart:

>[!example]
>```shell
>helm verify ./nginx-chart-0.1.0.tgz
>
># Verify when installing the chart
>helm install --verify nginx-chart-0.1.0
>```
>Obs: the veririfation phase cna be integrated into regular Helm commands, such as when dowling the chart or installing it.

>[!info]
>Generally chart repos contains the package chart, and `index.yaml` file --> this file contains information about the chart repository, and helm will read it when a new repository is added.

To generate the index file:

```shell
helm repo index chart-file --url https://repo.com/charts
```

To upload the chart:

```shell
helm repo add cool-chart https://example.charts.srorage.com
```


- `helm repo remove <name>` --> deletes a helm repository
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
- `helm upgrade` --> upgrades a chart, apply to the cluster.
	- `--atomic` --> automatically rollback a previous version of a deployment
- `helm uninstall` --> removes a deployment
	- `--keep-history` --> to keep the previous release (maintain the secrets)
- `helm rollback` --> restore a revision
	- Ex: `helm rollback mymariadb 3 -n database`
###### <span style="color: #689d6a">Helm Functions</span>

functions in Helm help transform data from one format to another

`upper` --> converts the value to upper case in the generated manifest file

>[!example]
>```go
>{{ upper .Values.image.repository }}
>```
>upper <span style="color: #3588E9">--></span> function name
>Values.image.repository <span style="color: #3588E9">--></span> argument

quote --> add quotes around the text in the generated manifest file

```yaml
{{ quote .Values.image.repository }}
```

replace --> replaces a character with another

>[!example]
>```shell
>{{ replace "x" "y".Values.image.repository }}
>```
>X is the string to look for and Y is the string to replace it with.

shuffle --> shuffle the characters

```yaml
{{ shuffle .Values.image.repository }}
```

The `default` function can be used to specify a default value.

>[!example]
>```yaml
>image: {{ default "nginx" .Values.image.repository }}
>```
>The value always have to be within a quote, anything that's not in quote is considered a variable.

`{{ | }}` --> pipe function, used to chain the functions available in the go and it supply the first function output as the input to the next function. Pipeline allows to pipe multiple functions one after the other.

```shell
{{ .Values.image.repository | upper | quote }}
```

The `indent` and functions helps to fix the indentation:

>[!example]
>```yaml
>spec:
>  selector: 
>    matchLabels:
>    {{- template "labels" . | indent 2 }}
>```
>The number indicates the space to indent.

The `nindent` function provides a new line and indentation to the defined argument 

```yaml
{{- template "labels" . | nindent 4 }}
```

The `include` function does the same job as the template function, but it can import a named template and also pipe it to another function.

>[!example]
>```yaml
>spec:
>  selector: 
>    matchLabels:
>    {{- include "labels" . | indent 2 }}
>```

>[!note]
>A full list of supportive function can be found in the Helm documentation pages.
>https://helm.sh/docs/chart_template_guide/function_list/#helm
###### <span style="color: #689d6a">Chart Templates</span>

<strong>Conditionals</strong>

In Helm charts we can encapsulate the lines taht we want to be available in an if condicioan lblock only the org;abel value is defined

>[!example]
>```yaml
>orgLabel: payroll
>```
>---
>```yaml
>metada:
>  name: {{ .Release.Name }}-nginx
>  {{ if .Values.orgLabel }}
>  labels:
>    org: {{ .Values.orgLabel}}
>  {{ end }}
>```

When the tempalte is converted to a manifest file, everything between the curly braces are removed. to remve wiede sapce that are before the template directive starts or near t the beggining of the curly braces, a dash can be addes ritgh after the curluy braces to indicate Helm to trim those out when the file are generated.

>[!example]
>```yaml
>metada:
>  name: {{ .Release.Name }}-nginx
>  {{- if .Values.orgLabel }}
>  labels:
>    org: {{ .Values.orgLabel}}
>  {{- end }}
>```
>The `-` (dash) removes the extra sapces adn the extra lines.

Else and else if statatements can also be added within cndional block in Hem chart:

>[!example]
>```yaml
>metada:
>  name: {{ .Release.Name }}-nginx
>  {{- if .Values.orgLabel }}
>  labels:
>    org: {{ .Values.orgLabel }}
>    {{- else if eq .Values.orgLabel "hr" }}
>    labels:
>      org: human resources
>  {{- end }}
>```
>The `eq` funtion checks the equality. It take two arguments and returns true uf they are euqal.

>[!example] Example 2 - not function
>```yaml
>{{- if not .Values.autoscaling.enabled }}
>  replicas: {{ .Values.replicaCount }}
>{{- end }}
>```

The most common use cases where conditional is used is whether to create objects of a certain kind or not.

>[!example]
>```yaml
>serviceAccount:
>  create: true
>```
>---
>```yaml
>{{- if .Values.serviceAccount.create }}
>apiVersion: v1
>kind: ServiceAccount
>metadata:
>  name: {{ .Release.Name }}-robot-sa
>{{- else }}  
>```
>It will only create the serviceAccount if the field create is set to true.

<strong>Scope</strong>

If a scope is not specifically set, the current scope in the file is set to the root scope by default. To access an specific object it must traverse all the way to the root scope.

>[!example] Example - Scope
>```yaml
>data:
>  background: {{ .Values.app.ui.bg }}
>```

To avoid duplication of scope, just set a scope using the `with` block:

>[!example] Example - with block
>```yaml
>data:
>  {{ - with .Values.app}}
>    {{- with .ui}}
>    background: {{ .bg }}
>    foreground: {{ .fg }}
>    {{- end }}
>  {{- end }}
>```
>The `.` within this block implies the current scope.

To access anything in the root scope:

```yaml
release: {{ $.Release.Name }} # $ --> represents the root scope
```

<strong>Loops</strong>

The `range` operators allows to create a for loop to iterate though the list in the values of a yaml full for example.

>[!example]
>```yaml
>regions:
>  - ohio
>  - newyork
>  - ontario
>  - london
>```
>---
>```yaml
>data:
>  regions:
>  {{- range .Values.regions}}
>    - {{ . | quote }}
>  {{- end }}
>```
>This create a block with a loop. Everything specified inside it will be repeated each time the loop iterates.

>[!note]
>The `range` block sets the scope each time it iterates though the list.

To write a custom template, it must use the same template language, but it doesn't have to be the go language. 

To execute the template without deploying resources:

```shell
helm template <char_name>
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
  {{$key}}: {{ $value | quote }}
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