GitHub Actions is a <strong style="color: #b16286">CI/CD platform that enables to automate the build, test and deploy GitHub workflow</strong>. It only works with and it's it's integrated into GitHub as a service. It allows to treat CI pipeline as code, which uses a <span style="color:#98971a">.ghithub/workflows</span> folder to store workflow definition as <span style="color:#98971a">.yaml</span> file.

> It doesn't matter the name of the YAML files because each file describes when they should be triggered.

<span style="color: #d65d0e">GitHub Actions Marketplace</span> hosts actions for workflows

<strong style="color: #d79921">Initial setup</strong>

- `.github` ---> `workflows` ---> `{ ci.yaml - cd.yaml - publish.yaml }`

<strong style="color: #d79921">Key elements</strong>

Workflow is the basic concept in Github Actions. A workflow is series of automated procedures represented as jobs and steps that GitHub Actions executes.

workflows are attached to the repositories and each repository can have any number of workflows.

Each workflow has the components: Event --> Runner --> Jobs --> Steps --> Actions

Workflow limitations: workflow concurrency is limited to twenty in the free plan, and Jobs are limited to six hours of runtime. If the workflow uses actions that interact with the GitHub API, which is limited to making 1000 API request per hour, and logs are limited to 4Kb. 

>[!note]
>Is a good practice to give the workflow a name that describes what it does.
>```yaml
>name: Project Pipeline
>```

<span style="color:#98971a">Event</span> <span style="color: #3588E9">--></span> Something that activates the execution of a workflow, it tells when the workflow should run. Example: checking code into a repo, push to a repository, create a pull request, etc..

The `on` keyword defines an event that should trigger the workflow to run.

```yaml
on: workflow_dispatch # manually trigger
```

```yaml
on: [ push, pull_request ] # for multiple events
```

```yaml
on: # defines an event 
  push: # event
    branches: ["main"] # runs whenever a push is made to the main branch, including from merging a pull request 
```

```yaml
on:
  pull_request:
    types: []
    branches:
     - master
```

```yaml
on:
  release: #  great for triggering a packaging workflow
    type: [publish]
```

To add conditional do a workflow:

```yaml
on:
  push:
    branches:
      - develop
      - main
  pull_request:
    branches:
      - develop
      - main
```

<span style="color:#98971a">Jobs</span> <span style="color: #3588E9">--></span>  made up for steps that are performed on the same runner. Workflows use runners to execute jobs. A workflow includes one or more jobs, it can have one job that build de component, and another to publish it to an artifact repository.

In case a workflows has more than one job, they are executed in parallel by default, but they can be configured to declare that one is dependent on another. (serially execution based on their dependencies). In case of multiple jobs they run in parallel ( by default), but they can also be configured to run in sequential order.

Conditioal jobs can be set up wichi will not always run, but which instead need a certain condtion to be met.

>[!info]
>Each workflow must have at least one job, and each job must have a unique identifier, which must start with a letter or underscore.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
  publish: # identifier
    runs-on: ubuntu-latest
      neeeds: build
      steps:
```

The `needs` directive specifies dependencies. It identifies one or more jobs that must complete successfully before a job will run.

Jobs can also optionally define required services for the workflow. Services are defined as Docker containers, any public Docker image can be used to create the service.

<span style="color:#98971a">Runner</span> <span style="color: #3588E9">--></span>  every job defines a so-called runner, which is the execution environment, the machine and operating system that will be used for executing the steps. There are built-in runners (predefined by GitHub) for different virtual environments, or a self-hosted runner that can be used in a owned environment. Example: ubuntu-latest.

```yaml
jobs:
  build:
    runs-on: ubuntu-22.04 # runner
```

<span style="color:#98971a">Steps</span> <span style="color: #3588E9">--></span>  Tasks comprising one or more shell commands or actions, each job can contain one or more steps, which are executed in the order that they're specified. Because all the steps of a job are executed of the same runner, they can share data with one another, that means a step can checkout the code, and another compile the code, etc.. 

A step is either a shell script, a command in the command line that should be executed, or an action, which is another important building block, are predefined scripts that perform a certain task. A Job must have at least one step, and those steps are then executed in order, and they can also be conditional.

An Action in the context of GitHub Actions, is a custom or third-party application that performs a (typically complex) frequently repeated task. Example: fetching the code fro ma GitHub Repository.

```yaml
jobs:
  test:
    runs-on: ubuntu-22.04
    steps:
      - name: Get code
		uses: actions/checkout@v4
```

Steps can have n optional name specified by the name keywords that displays in the report.

```yaml
steps:
 - name: Run unit test with nose
```

>It's a best practice to name the steps with something descriptive, if a step is not named, it can assume the name of the command that it's running.

Steps can have an optional ID specified by the `id` keyword, making it really helpful to refer to them in other steps. It's useful when it's needed to use the output of one step as the input parameters for another step.

Steps have either an action specified by the `uses` keyword or shell commands specified by the `run` keyword. `run`to execute shell commands defined by the user. 

```yaml
steps:
 - name: Install dependencies
   id: dependencies
   run: | # to run multiple shell commands
     python -v
     python -m pip install --upgrade pip
```

Steps can also have defined environment variables, which are dynamic key value pair stored in memory on the virtual environments.

Commands and actions running as steps can access environment variables to use the information they hold. These values are red as the process runs. They inject at runtime, they are also use sensitive.

Context Objects
Expressions --> github identifier `${{ }}`--> treat as metadata
`${{ toJSON(github) }}` --> expression
`toJSON` --> built in function

GitHub sets default environment variables that are available to every step in a workflow. Environment variables can be localized to specific parts of the workflow. The `env` keyword defines environment variables.

Environment variables can be accessed in two ways: using the syntax of shell running the step or using a yaml syntax. With the shell variable syntax, variable is passed on to step's shell to be interpreted or they are accessed within an action using that actions default shell for a step running.

```yaml
-$VARIABLE
```

To access environment variables using the yaml syntax, the variable name is placed inside a set of curly braces that start with a dollar sign. They are interpreted at the workflow level, which means that they are interpreted before it gets passed to any steps that use it.

```yaml
-${{ env.VARIABLE }}

-$Env:VARIABLE # for powershell
```



<span style="color:#98971a">Actions</span> <span style="color: #3588E9">--></span>  procedures that can be executed within a step.

>[!note]
>Actions are the lowest level of a workflow

Events are created with on keyword. most of the events are repository related. --> 
push, fork, watch, pull_request, issues, discussion, create, issue_comment. 

some event has activity types, which offers more detailed control over when a workflow will be triggered. example for pull_request event: opened, closed, edited.

```yaml
on: 
  pull_request:
    types: [closed]
```

event filters 

```yaml
on:
  push: 
    branches:
      - main
      - 'dev-*' # dev-new dev-this
      - 'feat/**' # feat/new feat/new/button
    paths-ignore:
      - '.github/workflows/*'
```

Jobs runs in an isolated environment (VM or Docker container)

By default, pull requests based on Forks do not trigger a workflow.

Actions are procedures that can be executed within a step. Defining actions requires the ‘uses:’ keyword followed by the name of the action.

actions can have arguments to configure them by specifying the ‘with:’ keyword followed by name-value pairs. Some actions use the ‘args:’ keyword. read the actions documentation to explore all options.

Job artifacts --> assets that must be uploaded or distributed, it's the output generated by a job. Example: app binary, web site files, log files, etc.

Job output --> values typically used for re-using in a different job. Example: name of a file generated in a previous build step

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    outputs: ${{ steps.publish.outputs.script-file}}
      script-file:
	steps:
	  - name: Publish JS filename
		id: publish
		run: find dist/assets/*.js -type f echo 'script-file={}' >> $GITHUB_OUTPUT ';'
```

Using an output from a previous job

```yaml
deploy:
  needs: build
  runs-on: ubuntu-latest
  steps:
    - name: Output filename
      run: echo ${{ needs.buid.outputs.script-file }}
```

$GITHUB_OUTPUT --> it targets a file, a special file created by GitHub in the environment in which the job runs where the output key-value pair is written to. 

cachin dependencies

```yaml
jobs:
  tests:
    runs-on: ubuntu-latest
    steps:
      - name: Cache dependencies
        uses: actions/cache@v3
        with: 
          path: ~/.npm # path(s) to be cached
          key: deps-node-modules-#{{ hashFiles('**/package-lock.json') }}
```

The `key` keyword will be used for retrieving the cache in the future and recreating the folder on the runner machine based on that cachaed managed by GitHub in the future. It also indicated wether the cache should be discarded because it must be recreated, in case of some depedency changed.

The `hashFiles()` function produces a unique hash value based on a file path passed to it. The hash value will change whenever the file passed to it changes too.

