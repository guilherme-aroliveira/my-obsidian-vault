GitHub Actions is a <strong style="color: #b16286">CI/CD platform that enables to automate the build, test and deploy GitHub workflow</strong>. It only works with and it's it's integrated into GitHub as a service. It allows to treat CI pipeline as code, which uses a <span style="color:#98971a">.ghithub/workflows</span> folder to store workflow definition as <span style="color:#98971a">.yaml</span> file.

<span style="color: #d65d0e">GitHub Actions Marketplace</span> hosts actions for workflows

<strong style="color: #689d6a">Initial setup</strong>

```text
project_aws                 <- repository
└── .github                 <- github directory
	 └── workflows          <- directory for the workflows
	     ├── ci.yaml        <- yaml file
	     ├── cd.yaml
         └── publish.yaml   <- yaml file
```

>[!info]
>It doesn't matter the name of the YAML files because each file describes when they should be triggered.

<span style="color: #d65d0e">Workflow</span> is the basic concept in Github Actions. A workflow is <strong style="color: #d79921">series of automated procedures</strong> represented as jobs and steps that GitHub Actions executes. The <strong style="color: #b16286">workflows are attached to the repositories</strong> and each repository can have any number of workflows.

<strong style="color: #c6554f">Workflow limitations</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">workflow concurrency</strong> is limited to 20 in the free plan, and Jobs are limited to 6 hours of runtime. If the workflow uses actions that interact with the GitHub API, it will be limited to making 1000 API request per hour. Logs are limited to 4 Kb.

Workflow components: 
- <span style="color:#98971a">Event</span>
- <span style="color:#98971a">Runner</span>
- <span style="color:#98971a">Jobs</span>
- <span style="color:#98971a">Steps</span>
- <span style="color:#98971a">Actions</span>

>[!note]
>Is a good practice to give the workflow a name that describes what it does.
>```yaml
>name: Project Pipeline
>```
##### <strong style="color: #689d6a">Workflow components</strong>
###### <span style="color:#98971a">Event</span>

An <span style="color:#98971a">event</span> is <strong style="color: #d79921">something that activates the execution of a workflow</strong>, it tells when the workflow should run. <strong style="color: white">Example:</strong> checking code into a repo, push to a repository, create a pull request, etc..

The <code style="color:#d79921">on</code> keyword defines an event that should trigger the workflow to run.

>[!example] Events
>```yaml
on: workflow_dispatch # manually trigger 
>
>on: [ push, pull_request ] # for multiple events
>```

>[!example] Event types
>```yaml
>on: # defines an event 
>  push: # event
>    branches: ["main"] # runs whenever a push is made to the main branch, including from merging a pull request 
>```
>---
>```yaml
>on:
>  pull_request:
>    types: []
>    branches:
>      - master
>```
>By default, pull requests based on Forks do not trigger a workflow.
>```yaml
>on:
>  release: # great for triggering a package workflow
>    type: [publish]
>```

>[!example] Conditions on workflows
>```yaml
>on:
>  push:
>    branches:
>      - main
>      - develop
>      - 'feat/**'  # feat/new feat/new/button
>    paths-ignore:
>      - '.github/workflows/*'
>  pull_request:
>    branches:
>      - develop
>      - main
>```

Most of the <span style="color:#98971a">Events</span> are repository related <span style="color: #3588E9">--></span> push, fork, watch, pull_request, issues, discussion, create, issue_comment. 

Is possible to execute a workflow at a specific time using a trigger, which is called <span style="color: #d65d0e">Schedule event</span> <span style="color: #3588E9">--></span> configured through the `schedule` keyword which uses a cron syntax. 

The <span style="color: #d65d0e">cron syntax</span> uses five fields, separated by spaces to describe a schedule. Reading from left to right , these fields represent minutes, hours, the day of the month, month, and the day of the week. 

>[!example] Scheduled event
>```yaml
>on:
>  schedule:
>    - cron: '*/10 * * * *' # run every 10 minutes
>```
>All `schedule` use Coordinated Universal Time (UTC)
>
>`*` <span style="color: #3588E9">--></span> used to represent all values for that field. The asterisk is a special character in yaml. So, the cron schedule must be quoted.

>[!note]
>The shortest internal for <span style="color: #d65d0e">Schedule Triggers</span> is five minutes, and they are deactivated when a public repository is forked, and after 60 days of inactivity.
###### <span style="color:#98971a">Jobs</span>

A <span style="color:#98971a">Job</span> <strong style="color: #d79921">made up of steps that are performed on the same runner.</strong> A workflow includes one or more jobs <span style="color: #3588E9">--></span> It can have one job that build de component, and another to publish it to an artifact repository. 

>[!note]
>Workflows use runners to execute jobs.

In case a workflow has more than one job, it's executed in parallel by default, but they can be configured to declare that one is dependent on another (serially execution based on their dependencies). In case of multiple jobs they run in parallel (by default), but they can also be configured to run in sequential order.

<span style="color: #3588E9">--></span> <strong style="color: #d79921">Conditional</strong> <span style="color:#98971a">jobs</span> can be set up, which will need a certain condition to be met.

>[!info]
>Each <span style="color: #d65d0e">workflow</span> <strong style="color: #d79921">must have</strong> at least one job, and each job must have a unique identifier, which must start with a letter or underscore.

>[!example] Example
>```yaml
>jobs:
>  build: # identifier 
>    runs-on: ubuntu-latest
>    steps:
>  publish:
>    runs-on: ubuntu-latest
>    needs: build
>    steps:
>      ...    
>```
>The `needs` directive <strong style="color: #b16286">specifies dependencies</strong> <span style="color: #3588E9">--></span> one or more jobs that must complete successfully before a job will run.

Any Job that use the `needs` directive will be cancelled or aborted, in case a previous job fails.

>[!note]
>The default behavior of GitHub Actions is <span style="color: #3588E9">--></span>  if one steps fails, the entire job to which the step belongs is aborted.

`needs: [lint, deploy]` <span style="color: #3588E9">--></span> GitHub Actions will delay the execution of the job until the other jobs have finished, than evaluates if any other job in front of that job has failed. The entire chain is evaluated.

Jobs can also optionally define required services for the workflow. 

>[!info]
><span style="color:#98971a">Services</span> are defined as Docker containers, any public Docker image can be used to create the service.
###### <span style="color:#98971a">Runner</span>

Every job defines a so-called <span style="color:#98971a">Runner</span>, which is the <strong style="color: #d79921">execution environment</strong> <span style="color: #3588E9">--></span> the <strong style="color: #b16286">machine and operating system</strong> that will be used for executing the steps. 

The runner application manages all the jobs, steps and actions in a workflow. It's an open-source application hosted on GitHub.com.

There are built-in runners (predefined by GitHub) for different virtual environments, or a self-hosted runner that can be used in a owned environment. Example: ubuntu-latest.

>[!Example]
>```yaml
>jobs: 
>  build: 
>    runs-on: ubuntu-22.04 # runner
>```
>hosted runners start in a fresh new compute environment on each workflow run.

GitHub Actions provider 3 different platforms for Jobs and workflows, Ubuntu linux, macOS, and Windows.

self-hosted runners lets you configure your job's compute environment to your specifications.  deploy and manage by the user. offers more control over the compute environment where the jobs run.

it can be associated with a single repository, organizaion or an enterprise. Runners added at the organization and enterprie ;evel can be used in mujltipe repositories. and simplify the management of multiple runners.

jobs; build; runson: sel-hosted

>[!example] self-hosted runner
>```yaml
>on:
>  build:
>    runs-on: self-hosted
>```
>Different labels can be used to identify different runners. <strong style="color: white">Example:</strong> redhat-linux.



any hardware can be used as long as the operating system is compatible with the runner application. Servers in an on-premises data server can be used. 

only use self-hosed runner with private repositories. Malicious code can persiste across workflow runs


###### <span style="color:#98971a">Steps</span>

A <span style="color:#98971a">Step</span> is a <strong style="color: #d79921">task comprising one or more shell commands</strong> or actions (predefined scripts that perform a certain task).

Each Job <strong style="color: #d79921">must</strong> <strong style="color: #b16286">contain at least one Step</strong>, which are executed in the order that they're specified, and they can also be conditional.

>[!info]
>All steps of a job are executed of the same runner, they can share data with one another, that means a step can checkout the code, and another compile the code, etc.. 

An <span style="color:#98971a">action</span> is a <strong style="color: #d79921">custom or third-party application that performs a frequently repeated tasks</strong> (typically complex). <strong style="color: white">Example:</strong> fetching the code from a GitHub Repository.

>[!example] Example - action
>```yaml
>jobs:
>  test:
>    runs-on: ubuntu-22.04
>    steps:
>      - name: Get code
>        uses: actions/checkout@v4       
>```
>Defining actions require the `uses` keyword, followed by the name of the action.

>[!note]
>Actions are the lowest level of a workflow, they perform a single task, like check out code, install dependencies, compile code or run tests.

<span style="color:#98971a">Actions</span> can have arguments to configure them by specifying the `with` keyword followed by name-value pairs. Some actions use the `args` keyword.

>[!example] actions - arguments
>```yaml
>steps: 
>  - name: Upload code average
>    uses: codecov/codecov-action@v3
>    with:
>      version: v0.1.13 
>```

>[!note]
>Actions <strong style="color: #d79921">can't</strong> trigger other workflows. Actions are basically a collection of code that gets compiled on the fly.

Actions can be sourced from 3 different types of locations:
- public repository
- the same repository as the workflow
- docker image from and image registry

>[!example] action - location
>```yaml
>steps:
>  - uses: codecov/codecov-action@v3 # owner/repository@reference
>```
>The <span style="color: #d65d0e">reference</span> can be a  specific branch, like the branch name for example.
>```yaml
>uses: docker://image:tag
>```
>- To specify a docker image in a public repository other than docker hub, the host name must be informed before the image name
>```yaml
>uses: //host/image:tag
>```

Steps can have any name, which is specified by the `name` keyword that displays in the report.

>[!example] Naming a Step 
>```yaml
>steps:
>  - name: Run unit test with nose
>```
>It's a best practice to name the steps with something descriptive, if a step is not named, it can assume the name of the command that it's running

Shell commands in a Step is specified the `run` keyword, which are defined by the user. 

>[!example] Steps
>```yaml
>steps:
>  - name: Install dependencies
>    id: dependencies
>    run: |  # to run multiple shell commands
>      python -v
>      python -v pip install --upgrade pip
>```
>Steps can have an optional ID specified by the `id` keyword, making it really helpful to refer to them in other steps. It's useful when it's needed to use the output of one step as the input parameters for another step.

Steps can also use <span style="color: #d65d0e">environment variables</span>, which are <strong style="color: #d79921">dynamic key value pair</strong>, stored in memory on the virtual environments. Example: password that is used for a database.

The environment variables are used in actions or in shell commands to store some value, that is inject at runtime. An environment variable <strong style="color: #b16286">can be defined at the workflow level or at the job level</strong> <span style="color: #3588E9">--></span> defined by the `env` keyword.

If an <span style="color: #d65d0e">environment variables</span> is defined at the workflow level (interpreted before it gets passed to any step), it will use the shell syntax, which it's passed to shell commands during the step.

>[!example] shell syntax - workflow level
>```yaml
>on: workflow_dispatch
>env:
>  MONGODB_DB_NAME: gha-demo
>jobs:
>  deploy:
>    runs-on: ubuntu-latest
>    steps:
>      - name: Output imformation
>        run: |
>           echo "MONGODB_DB_NAME: $MONGODB_USERNAME"
>```

If an <span style="color: #d65d0e">environment variables</span> is defined at the Job level it will use the yaml syntax, which must be placed inside the github identifier <span style="color: #3588E9">--></span> `${{ }}`. The github identifier treats an expression or value as a metadata. 

>[!example] yaml syntax - job level
>```yaml
>jobs:
>  build:
>    env:
>      MONGODB_NAME: cluster
>    runs-on: ubuntu-22.04
>    steps:
>      - name: Output information
>         run: |
>           echo "MONGODB_NAME: ${{ env.MONGODB_NAME }}"
>```
>---
>```yaml
>$Env:VARIABLE # for powershell
>```
>In 12-factor fashion, services should be configured through environment variables, and the `env` keyword allows to do that. 

To store sensitive information <span style="color: #d65d0e">secrets</span> must be used, which are stored as encrypted values in the GitHub repository settings. <span style="color: #d65d0e">Secrets</span> they can be accessed in the workflow using the secrets context in yaml format <span style="color: #3588E9">--></span> passed in as environment variables or arguments, they must be explicit passed in.

>[!example] Secrets
>```yaml
>jobs:
>  test:
>    env:
>      MONGODB_USERNAME: ${{ secrets.MONGODB_USERNAME }}
>```
>Workflows can have up to 100 secrets, and secrets are limited to 64 kilobytes in size.
##### <strong style="color: #689d6a">Controlling workflow</strong>

<span style="color: #d65d0e">Artifacts</span> can be used to pass data between jobs in a workflow. They can only be uploaded by a workflow, which is done through the `upload-artifact` action. Artifacts can only be downloaded by the workflow where they were created using the `download-artifact` action.

<span style="color: #d65d0e">Job artifacts</span> <span style="color: #3588E9">--></span> assets that must be uploaded or distributed, it's the output generated by a job. <strong style="color: white">Example:</strong> app binary, web site files, log files, etc.

>[!example] artifacts
>```yaml
>steps:
>  - uses: actions/upload-artifact@v3
>    with:
>      name: dist-files
>      path: |
>        dist
>        package.json
>```

<span style="color: #d65d0e">Job output</span> <span style="color: #3588E9">--></span> values typically used for re-using in a different job. <strong style="color: white">Example:</strong> name of a file generated in a previous build step.

>[!example] output
>```yaml
>jobs:
>  build:
>    runs-on:
>    outputs:
>      script-file: ${{ steps.publish.outputs.script-file}}
>    steps:
>      - name: Publish JS filename
>        id: publish
>        run:  find dist/assets/*.js -type f -execdir echo 'script-file={}' >> $GITHUB_OUTPUT ';'
>        
>```
>The variable `$GITHUB_OUTPUT` <span style="color: #3588E9">--></span> targets a file, a special file created by GitHub in the environment in which the job runs where the output key-value pair is written to.
>```yaml
>steps:
>  - name: Output filename
>    run: echo ${{ needs.build.outputs.script-file }} # syntax to use the output from another job
>```

<span style="color: #d65d0e">Dependency caching</span> <span style="color: #3588E9">--></span> creates a copy of the dependencies to use again later. It allows to save time and to reuse dependencies across Jobs and Workflows executions.

>[!example] dependency caching
>```yaml
>jobs:
>  tests:
>    runs-on: ubuntu-latest
>    steps: 
>      - name: Caching dependencies
>        uses: actions/cache@v3
>        with:
>          path: ~/.npm # path(s) to be cached
>          key:  deps-node-modules-${{ hashFiles(**/package-lock.json) }}
>```
>The `key` keyword will be used for retrieving the cache in the future and recreating the folder on the runner machine based on that cache. It also indicated whether the cache should be discarded because it must be recreated, in case of some dependency changed.
>
>The `hashFiles()` function produces a unique hash value based on a file path passed to it. The hash value will change whenever the file passed to it changes too.
###### <span style="color: #d79921">Conditions</span>

The `if` keyword and the usage of <span style="color: #d65d0e">dynamic expressions</span> allows to control steps and jobs executions in a workflow.

>[!example] step condition
>```yaml
>steps:
>  - name: Upload test report
>    if: steps.test.outcome == 'failure'
>    uses: actions/upload-artifact@v3
>```
>This step will only be executed if the previous step is successful

<span style="color: #d65d0e">Dynamic expressions</span> are wrapped using `${{ }}`, but in the `if` directive they can be omitted. The expression will be evaluated in the same way.

Another way to evaluate Steps is by using special <span style="color: #d65d0e">conditions functions</span>, like `failure()` for example.

The are four special conditions functions:
- `failure()` <span style="color: #3588E9">--></span> returns true when any previous Step or Job failed
- `success()` <span style="color: #3588E9">--></span> 
- `always()` <span style="color: #3588E9">--></span> 
- `cancelled()` <span style="color: #3588E9">--></span> 

>[!example] failure() function
>```yaml
>if: failure() & steps.test.outcome == 'failure'
>```
> the Steps should still be evaluated even if previous Steps of Jobs have failed.
> ```yaml
> reports:
>   needs: lint
>   if: failure()
>   steps:
>     ....
> ```
> The job will run if any other job failed.

The `continue-on-error` directive allows to ignore erros and failure. If the value is set to `true`, the job will continue it's execution even if the step fails. it overrides the default behavior. 
###### <span style="color: #d79921">Matrix strategies</span>

Run multiple Job configuratins in parallel; add or remove individual cominations; control whether a single failling Job should cancel all other Matrix Jobsd via conrinue-on-error.

```yaml
jobs:
  build:
    strategy: 
      matrix: 
        operating-system: [ubuntu-latest, windows-latest]        
    runs-on: ${{ matrix.operating-system }}    
```

it can be any value that could be changing and for which Job to run for different values. 

`runs-on: ${{ matrix.operating-system }}` --> run the job multiples times, once per value, in the operation system array. The Jobs will be run in parallel by default.

node version example

```yaml
jobs:
  build:
    continue-on-error: true
    strategy: 
      matrix: 
        node-version: [12, 14, 16]
    runs-on: ubuntu-latest
    steps:
      - name: Install NodeJS
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
```

`continue-on-error: ` on job level tells GitHub Actions to continue executing jobs that are related to this matrix, even if some jobs for some combinations failed.

The `include` key allows to add a list with dashes of the key values that should be included without adding a bunch of new combinations.

```yaml
strategy: 
  matrix: 
    node-version: [12, 14, 16]
    include:
      - node-version: 18
        operating-system: ubuntu-latest
```

The `exclude key` will exclude some combinations.

```yaml
strategy: 
  matrix: 
    node-version: [12, 14, 16]
    exclude:
      - node-version: 18
        operating-system: windows-latest
```
###### <span style="color: #d79921">Reusable Workflows </span>

```yaml
name: Reusable Deploy
on: workflow_call 
jobs: 
  deploy:
    runs-on: ubuntu-latest
    steps:
     - name: Output information
       run: echo "Deploying & uploading ..."
```

`on: workflow_call` --> allows a certain workflow to be called from other workflows.
Workflow can be reused via the `workflow_call` event; reuse any logic (as many Jobs & Steps as needed)

```yaml
deploy:
  needs: build
  uses: ./.github/workflows/reusable.yaml
```

`uses` --> references an entire workflow by providing a full path to the workflow file seen relative from the route project folder. 

to vie the reusable workflows all the data it might need and to also pass data back to the workflow that uses the reusable workflow.

Adding data (input)

```yaml
on: 
  workflow_call :
    inputs: 
      artifact-name:
        description: The name of the deployable artifact files
        required: true
        default: dist
        type: string
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Get Code
        uses: actions/download-artifact@v3
        with:
          name: ${{ inputs.arfifact-name }}
```

`${{ inputs.arfifact-name }}` --> to use an input

```yaml
deploy:
  uses: ./.github/workflows/reusable.yaml
  with:
    arifact-name: dist-files
```

secrets

```yaml
on: 
  workflow_call :
    secrets:
      some-secret:
        required: true
```

```yaml
deploy:
  uses: ./.github/workflows/reusable.yaml
  secrets: 
    some-secret: ${{ secrets.some-secret }}
```

Outputs

```yaml
name: Reusable Workflow
on:
  workflow_call:
    outputs:
      result:
        description: The result of the deployment operation
        value: ${{ jobs.deploy.outputs.outcome }}
jobs:
  deploy:
	outputs:
	  outcome:  ${{ steps.set-result.outputs.step-result}}
    runs-on: ubuntu-latest
    steps:
      - name: Set result ouput
        id: set-result
        run: echo "step-result=success" >> $GITHUB_OUTPUT
```

The `value` is typically taken from the steps in one of  the Jobs.

```yaml
deploy:
  uses: ./.github/workflows/reusable.yaml
  with:
    ...
print-deploy-result: 
  needs: deploy
  runs-on: ubuntu-latest
  steps:
    - name: print deploy output
      run: echo "${{ needs.deploy.outputs.result }}"
report:
  ... 
```

##### <strong style="color: #689d6a">Docker Containers</strong>

And the advantage of using Containers instead of "Just the Runner" machine as we did it thus far, is that with a Container, since you defined the entire environment you have full control over the environment over the installed software and the setup steps that were performed for setting up that environment.

 GitHub Actions supports Docker Containers and you can simply run Docker Containers on top of those Runners provided by GitHub and by GitHub Actions.
Your containerized job is then simply hosted by the Runner so it's running on that Runner machine but in an isolated environment. The environment defined by you in the Container definition and the steps, and that's the important part the steps of the job are then executed inside the Container.

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    container: 
	  image: node:16
```

The names of the images must be the ones available on Docker Hub.

service containers --> They allow you to run extra services side-by-side with your Jobs and their Steps. So that they can be used by your Jobs and the Steps. Runs inside a containers. 
Job steps can communicate with service containers (and the service exposed by them)

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    container: 
	  image: node:16
	services:
	  mongodb: # label, could be anything
	    image: mongo
	    env: 
	      ...
```

And that's important, services, plural, not service because you can add more than one service container for a job.

Services belong to a job, so to one specific job. If different jobs need different services, you do set them up with different services settings for those different jobs.

services always run in containers, but they can be used using just the runner.

push event --> ideal for building images

```yaml
on:
  push:
    branches: [main]
    tags:['v*.*.*']
```
push event will be use to tag images with a brnach name adn the sha associated with the commit that triggered the psh. 
These tags can be used for testing and other dynamic scenarios

Push events with tags like release are best used to create images that can be referenced in places where the image is fixed.

```yaml
- uses: docker/login-action
  with: 
    registry: gcrh.io
    username: ${{ github.actor }}
    password: ${{ secrets.GITHUB_TOKEN }}
```
to authenticate to the docker registry

```yaml
- uses: docker/metadat-action
  id: meta
  with: 
    images: |
      registry_1/image_name
      registry_2/image_name
```
helps to extract metadata from the code that can be used to create tags an labels
Multiples images can be provided if we are pushing to multiple registries

```yaml
- uses: docker/build-push-action
  with:
    context: . 
    tags: ${{ steps.meta.outputs.tags }}
    labels: ${{ steps.meta.outputs.labels }}
```
build and publish the image to the target registry

using an image
```yaml
run: docker run ghst.io/account/image:main # run step
```
`uses: account/image@main` --> in uses step




##### <strong style="color: #689d6a">Custom Actions</strong>

to simplify workflow steps
- build and use a single custom actiosn instrad or writing multiple Step definitions
- multiples Steps can be grouped into a single custom Action

existing public Actions might not solve a specific problem in a workflow

Custom Actions can contain any logic needed to solve a specific Workflow problem.

types of custom actions:
- JavaScrit Actions --> actions where the its logic is written in JavaScript
	- execute a JavaSript file 
	- bundled with dependencies 
	- runs directly on the runner system
	- all supported runners
	- use JavaScript (NodeJS) and any other package 
- Docker Actions --> containeeized acrtion, which create a Dockerfile with the required configuration.
	- self-contained
	- perform any task(s) with any language
	- pulled or build on each workflow run
	- requires a linux-based runner
- Composite Actions --> combine multiple Workflow Steps in one single Action
	- Combine `run` commands and `uses` actions
	- allows for reusing shared Steps

Composite Actions

actions can be added to projects tha I already havem --> only available in that prpject. Is must have a action.yaml file

Example: 

.github --> actions --> contains the actions only usable by the current project  / cached-deps; workflows 

action.yaml --> file tha tcontains the configuration and the definition of that action.
```yaml
name: 'Get & Cache Dependencies'
description: 'Get the depdencies (via npm) and cache them.'
runs: 
 using: 'composite'
 steps:
  - name: Cache dependencies
    id: cache
    uses: action/cache@v3
    with:
     path: node_modules
  - name: Install depdencies
    if: 
    run: npm ci
    shell: bash
```

To create actiosn that are available to different workflows in different repos, they must be created as standalone repos.

to use custom actions on another project
deploy.yaml

```yaml
lint:
  deploy:
    runs-on: ubuntu-latest
    steps:
     - name: Load cache
       uses: <repo_name>/action
```

using custom action on the same project
```yaml
lint:
  deploy:
    runs-on: ubuntu-latest
    steps:
     - name: Load cache
       uses: ././github/actions/cached-deps
```

Adding inputs

```yaml
name: 'Get & Cache Dependencies'
description: 'Get the depdencies (via npm) and cache them.'
inputs: 
  caching: # can be any name
    description: 'Whether to cache dependencies' # must be added
    required: false
    default: 'true'
runs: 
 using: 'composite'
 steps:
  - name: Cache dependencies
    if: inputs caching == 'true'
    ...
```

```yaml
lint:
  deploy:
    runs-on: ubuntu-latest
    steps:
     - name: Load cache
       uses: ./.github/actions/cached-deps
       with:
         caching: 'false'
```

outputs

```yaml
name: 'Get & Cache Dependencies'
description: 'Get the depdencies (via npm) and cache them.'
outputs: 
  used-cache: # can be any name
    description: 'Whether the cache was used' # must be added
    value: ${{ steps.install}}
runs: 
 using: 'composite'
 steps:
  - name: Install dependencies
    id: install
    if: steps.cache.outputs.cache-hit != 'true'
    run: echo "cache=${{ inputs.caching }}" >> $GITHUB_OUTPUT
```

```yaml
lint:
  deploy:
    runs-on: ubuntu-latest
    steps:
     - name: Load cache
       uses: ./.github/actions/cached-deps
       id: cache-deps
    - name: Output information
      run: echo "Cache used? ${{ steps.cache-deps.outputs.used-cache }}"
```

Javascript custom actions
requirements :
- repository for the code
- use `.gitinore` file for Node projects
- node runtime installed
- run `npm init`
- run `npm install --globak @vercel/ncc` --> installs a global package, it helps compile the action into a single file along with all of its depoendencies
- install dependencies: `@actions/core` and `@actions/github`
- add an action metadata file and a README file

The metada file is the inteface that a Gighutb action's workflow will use to connect tto the javascript action. it describes the name of the action, along with the runtime, and any inputs and outputs. The pasth to the index file mus be specified. 

```yaml
name: 'Deploy to AWS S3'
description: 'Deploy a static website voa AWS S3'
inputs:
 ...
outputs:
 ...
runs: 
 using: 'node16'
 main: 'dist/index.js'
```

the package.json must be updaded byt addinf a valid test, ad na buidl script to make it easier to compile the action.

```json
"sctipts": {
	"test": "node dist/index.js",
	"build": "ncc build index.js"
},
npm run test
npm run build
```

example
```javascript
// require the libraries for actions
const core = require('@actions/core')
const github = require('@actions/github')

// use an async function ro the main tasks
async function main() {
	console.log('Hello')
}

// call the function
main();
```





the file for the `main` field must be created, but it can be any name. It will execute the `index.js` file whenever the custom action is used in a workflow step.

```js
const core = require('@actions/core')
//const github = require('@actions/github')
const exec = require('@actions/exec')

function run() {
	// 1) Get some input values
	const bucket = core.getInput('bucket', { required: true });
	const bucketRegion = core.getInput('bucket-region', { required: true });
	const distFolder = core.getInput('dist-folder', { required: true });

	// 2) Upload files
	const s3Uri = `s3://${bucket}`
	exec.exec(`aws s3 sync ${distFolder} ${s3Uri} --region ${bucketRegion}`)

	const websiteUrl = `http://${bucket}.s3-website-${bucketRegion}.amazonaws.com`
	core.setOutput(`website-url`, websiteUrl); //::set-output

	//core.notice('Hello from my custom JavaScript Action')
}

run();
```

`npm init -y` --> to use `npm` command
install dependencies to use the javascript actions
`npm install @actions/core @actions/github @actions/exec`

`github.getOctokit()` --> tool provided by Github that makes easier to send requests to the Github Rest API

Github actions Toolkit --> a collection of javascript packages that help developers to create javascript actions. the most essentials are core and github.
`@actions/core` --> provides functionality for working with GitHub actions front-end and internals of the GitHub actions framework
- read inputs, set outputs
- create annotations --> useful for bringing atention to details in workflow logs
- set exit code

core.info() --> used for logging
core.notice(), core.warning(), core.error() for annotations  --> appear on the log but have color styling and are also added to the summary page of a workflow run
annotations --> useful for indicating when an action had to handle an exception, 
or encountered some sort of problem. 

core.setFailed() more useful if the condidtion is critial enough to cause a workflow to fail. set the status of the step to a non-zero exit code. 

call to the info function are printed in the workflow log.

`@actions/github` --> exposes the workflow-action context as JSON
provides an authenticated octokit client (GitHub client) --> allows javascript action s to directly access the GitHub API

 workflow-action context --> json object that contains all the properties related to a GitHub event. `cont { context } = require('@actions/github')`
 `context.payload` --> context object
 context values can be used as parameter for octokit API calls.
example
```yaml
const { context } = require('@actions/github')
const { pull_request } = context.payload

await ocktokit.rest.issues.createComment({
	owner: repo.repo.owner,
	repo: repo.repo.repo,
	issues_number: context.payload.number,
	body: 'Thanks for the issue!'
});
```



Custom Docker actions

It uses a `.py` file with all the logic behind the action that will be executed, a dockerfile that creates the environment where the code will run, and a requirements file specifying the packages that should be installed into the environment.

```dockerfile
FROM python:3

COPY requirements.txt /requirements.txt

RUN pip install -r requirements.txt

COPY deployment.py /deployment.py

CMD ["python", "/deployment.py"]
```

action.yaml

```yaml
name: 'Deploy to AWS S3'
description: 'Deploy a static website via AWS S3'
inputs:
  bucket:
    description: 'The S3 bucket name'
    required: true
outputs:
  website-url:
    description: 'The URL of the deployed website'
runs:
  using: 'docker'
  image: 'Dockerfile'
```
##### <strong style="color: #689d6a"> Security</strong>

concerns
- Script Injection
	- a value, set outside a Workflow, is used in a workflow
	- example: issue title used in workflow shell command
	- workflow / command behavior could be changed
- Malicious Third-Party Actions
	- Actions can perform any logic, including potentially malicious logic
	- Example: a third-party Action that reads and exports secrets
	- Only use trusted Actions and inspect code of unknown/untrusted authors
- Permission Issues
	- Consider avoiding overly permissive permissions
	- Example: only allow checking out code ("read only")
	- GitHub Actions supports fine-grained permissions control

GitHub Actions makes controlling Permissions for jobs quite easy and straightforward. Because you can add the special permissions key to a job, to control the permissions for various kinds of actions or areas a Workflow could be acting on. permissions are managed on job level, you can also add them here, on Workflow level, so that they apply to all jobs,

if you don't set permissions at all, then by default this Workflow with all its jobs is able to do anything. It basically has full permissions or almost full permissions.

```yaml
jobs:
assign-label:
  permissions: 
    issues: write-all
```

If you would be vulnerable to script injection, those scripts would not be able to do things that are not allowed by Permissions.

 token automatically generated by GitHub, which is available in the jobs of this workflow, and which is only valid until our jobs are done. So the token will be deleted by GitHub once our job's executed. t's a very short lift token that's only valid as long as our jobs are running here.

an then be attached to requests being sent to GitHub's API to authenticate the request and perform certain actions.

--> only use your own actions 

Github Actions allows to build human interactions  with  envronment protection rules that include manual apprvoals. 
environments --> descirves a target for a deployment
to protect environment, rules can be defined to identify which branches can deployt to a given invoronment --> deployment branches 

environemnt secrets are useful for configurations that use the same variable but have different values.

workflows that are protected by manual approvals can only access environemnt secrets after te deployment is approved

GitHub packages also provides built int controls for permissions and visibiliy of any packages that are publish.For packages, permissions and visibilitu are inherited fomr the repo where the package ois hosted.

container image permissins can be customized (granularity) to accounts and organizations.

Authentication is required to create and access softwagre pacgages. in owrkflows, the GITHUB_TOKEN must be used to autehntica to the package management tools.

For private packages, each account receives a certain amount of storage and data transfer.