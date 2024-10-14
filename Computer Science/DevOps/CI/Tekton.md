Tekton is a flexible, <strong style="color: #b16286">open source framework that abstract the implementation details</strong>. It enable to build, test and deploy apps in [[Kubernetes]] using an open-source, vendor-neutral framework. It offers modularity, allowing to deploy across multiple environments such as VMs, serverless, Kubernetes, and cloud providers.

By standardizing the CI/CD tooling and process, Tekton works well with other other CI/CD tools such as Jenkins, Skafold, Knative. Tekton pipelines are fully portable, so once they are created or defined, a developer in the organization can take the pipeline and reuse its components.

Everything about Tekton is <strong style="color: #d79921">Kubernetes native</strong>. Everything is running in a Kubernetes cluster with no external CI/CD servers required.

<strong style="color: white">Benefits:</strong>
- standardization across vendors, languages, and deployment environments
- cloud native solution
- maximizes flexibility and customization
- abstract the underlying implementation

Tekton has parallel processing, which allows to execute two pipeline stages at the same time.

<code style="color:#98971a">tkn</code> <span style="color: #3588E9">--></span> Tekton CLI tool
- `tekton cli` can be used for both searching and getting information about tasks in Tekton Hub.
- <code style="color:#98971a">tkn [<span style="color:#689d6a">command</span>] [<span style="color:#689d6a">command</span>]</code>
- <strong style="color: #d79921">Commands:</strong>
	- <code style="color:#689d6a">tkn search --kinds task build [keyword]</code> <span style="color: #3588E9">--></span> search for a task and pipeline
	- <code style="color:#689d6a">tkn hub search cli</code> <span style="color: #3588E9">--></span> search for tasks with the 'cli' tag
	- <code style="color:#689d6a">tkn hub install task [task_name]</code> <span style="color: #3588E9">--></span> install a task
	- <code style="color:#689d6a">tkn hub install task [task_name]</code> <span style="color: #3588E9">--></span> install the task on the local namespace
	- <code style="color:#689d6a">tkn clustertask ls</code> <span style="color: #3588E9">--></span> to see what cluster tasks are installed
	- <code style="color:#689d6a">tkn hub info task [task_name]</code> <span style="color: #3588E9">--></span> show info about the task
	- <code style="color:#689d6a">tkn pipelinerun logs</code> <span style="color: #3588E9">--></span> to show the logs
		- <code style="color:#689d6a">--latest</code> <span style="color: #3588E9">--></span> specify the latest logs
	- <code style="color:#689d6a">tkn pipeline ls</code>
	- <code style="color:#689d6a">tkn task ls</code>

<span style="color: #d65d0e">Tekton catalog</span> or Tekton Hub is a repository of Tekton task that have been contributed by the community <span style="color: #3588E9">--></span> <span style="color: #d65d0e">hub.tekton.dev</span>

<span style="color: #d65d0e">Workspace</span> <span style="color: #3588E9">--></span> is a shared volume that all tasks have access to. They are declared in the PipelineRun, and they are implemented as a Kubernetes PersistentVolumeClaim.
- Each task defines the parameters and workspaces it needs in order to run.
- The PipelineRun must map the workspace to a PersistentVolumeClaim.
- Parameters can be mapped from the pipeline to the taks as nedeed.

>[!info]
>Workspace is required to share build artifact.
###### <span style="color: #d79921">Conceptual Building Blocks</span>

EVENT <span style="color: #3588E9">--></span> TRIGGER <span style="color: #3588E9">--></span> PIPELINE <span style="color: #3588E9">--></span> TASK <span style="color: #3588E9">--></span> STEP

EVENT --> external event that fires a trigger, might be a Pull Request or a Push to a Git repository.

TRIGGER --> allow the pipeline to respond to external events, starts a pipeline run.

PIPELINE --> collection of tasks to execute, there is no limit to the number of tasks that a pipeline can have.

TASK --> a unity of work that comprises one or more steps, can also define parameters required to carry out the steps.

STEPS --> commands that are executed within a task, most often they are shell scripts that execute commands to build, test and deploy applications.

###### <span style="color: #d79921">Building a Tekton Pipeline</span>

Defining TASK <span style="color: #3588E9">--></span> STEP
- Check out the code (TASK)
- Run quality checks (TASK)
- Run unit tests (TASK)
- Build container image (TASK)
- Deploy to an environment (TASK)

--> All the definitions are described in YAML files.

Tekton defines new custom resource definitions in Kubernetes.

A task is a collection fo steps. A step is contained within a task, and that task runs on a pod. Every step executes in a new container in that pod.

Note: Since steps are always run in series, the containers will be created one at a time, each one starting when the previous one ends.

After the creation of the necessary Pods, usaully, a PersistentVolumeClaim is created, and the storage is attached to all the pods so that they can share artifacts throughout the pipeline --> allows to checkout the code in one task and run unit test in another for example.

Most pipelines require some form of persistent storage

> Just like the task definition, a pipeline definition is a Kubernetes manifest.

Run the PIPELINE
1. kubectl apply -f tasks.yaml -- (just create a task definition)
2. kubectl kubectl apply -f pipeline.yaml -- (just create a pipeline definition)
- tkn pipeline start pipeline --showlog -p repo-utl="https://github.com/guilherme.ar/tekton-testing.git" -- (runs the pipeline)
	- <code>--showlog</code> --> parameter to show the logs on the console
	- <code>-p</code> --> flag to pass any parameter

The actual task and pipeline are created by other resources called ‘TaskRun’ and ‘PipelineRun’. The Tekton CLI creates the ‘PipelineRun’ and ‘TaskRun’ resources behind the scenes -- it automates this process.

<strong style="color: #d79921">Tekton Triggers</strong>

Defining EVENT --> TRIGGER

Tekton triggers allow the pipeline to respond to external events. They do this with a custom resource definition (or CRD) known as an EventListener that points to two other CRDs.

Note: Tekton is a set of Kubernetes CRDs

The TriggerBinding CRD, which takes data from the event and binds it to the properties in the pipeline. And the TriggerTemplate CRD, which takes data from the binding and instantiates a PipelineRun, passing in that data.

> PipelineRuns could be create manually and not use events, but CI/CD pipelines are usually driven by events.

triggers flow<ul><li>Event ---> [ [TriggerBiding] ---> Parameters ---> [TriggerTemplate] ] ---> PipelineRun</li></ul>
> When an EventListener is created, it creates a pod running in Kubernetes that listens for events.

<strong style="color: #d79921">Tasks and Quality Checks</strong>

