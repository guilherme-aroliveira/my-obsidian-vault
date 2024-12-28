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

The `key` keyword will be used for retrieving the cache in the future and recreating the folder on the runner machine based on that cached managed by GitHub in the future. It also indicated whether the cache should be discarded because it must be recreated, in case of some dependency changed.

The `hashFiles()` function produces a unique hash value based on a file path passed to it. The hash value will change whenever the file passed to it changes too.

Environment Variables

values that are dynamic in the code. Example: password that is used for a database.
Using secrets

Also environment variables but stored, such that no one can access them.

```yaml
name:
on:
  push:
    branches: [main, dev]
env:
  MONGODB_DB_NAME: gha-demo # at workflow level

jobs:
  test:
	environment: staging
    env: # variáveis disponíveis at job level
      MONGODB_CLUSTER_ADDRESS: cluster0.15pwqcc.mongodb.net
      MONGODB_USERNAME: ${{ secrets.MONGODB_USERNAME }}
      MONGODB_PASSWORD: ${{ secrets.MONGODB_PASSWORD }}
      PORT: 8080
    runs-on: ubuntu-22.04
    steps:
      - name: Run server
        run: npm start & npx wait-on https://127.0.0.1:$PORT
      - name: Output information
        run: echo "MONGODB_USERNAME: ${{ env.MONGODB_USERNAME }}"

  deploy:
    needs: test
    runs-on: ubuntu-22.04
    steps:
      - name: Ouput information
        run: |
	      echo "MONGODB_DB_NAME: $MONGODB_USERNAME"
```


controlling workflow & Job execution
conditional steps

control Step or Job execution with `if` and dynamic expressions  

```yaml
    steps:
    
	  - name: Test code
	    run: npm run test
	    id: test
	    
      - name: Upload rest report 
        if: steps.test.outcome == 'failure'
	    uses: actions/upload-artifact@v3
	    with:
	      name: test-report
	      path: test.json
```

The step "Upload test report" will only "Test code" is successful

Other dependent (!) Jobs (using "needs") would be cancelled / aborted, if a previous job fails.
default behavior of GitHub Actions is that if one steps fails, the entire job to which the step belongs is canceled, is aborted.

${{ }} --> the condition can be wrapped in here (Github Actions expression syntax) , it evaluates an expression, the syntax can be omitted for the `if` field.

`if: failue() & steps.test.outcome == 'failure'` --> the Steps should still be evaluated if it has failing steps of Jobs before that step.
special conditions functions: failure(), success(), always(), cancelled()
failure() --> returns true when any previous Step or Job failed


If isn't true (not able to use the cache), than manually install the dependencies again, if it's true the step os skipped based of the condition.

```yaml
- name: Install dependencies
  if: steps.cache.outputs.cache-it != 'true'
  run: npm ci
```


Conditional Jobs

```yaml
report:
  needs: [lint, deploy] # run the job only if any other job fails
  if: failure()
  runs-on: ubuntu-latest
  steps: 
    ... 
```

runs the jobs only if some other job failed.
make sure that the job will run if any other job failed

`needs: [lint, deploy]` --> GitHub Actions will delay the execution of the job until the other jobs have finished, than evaluates if any other job in front of that job has failed. The entire chain is evaluated.

Ignoring Errors and Failures

```yaml
- name: Test code
  continue-on-error: true
  id: run-tests
  run: npm run test
```

`continue-on-error: true` --> The job will continue it's execution even if the step fails. It treats the step as a success, despite it's technically failing because it basically overrides the default behavior. 

Matrix strategies

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

Reusable Workflows 

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

Docker Containers 

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

service containers --> 


Custom Actions

to simplify workflow steps
- build and use a single custom actiosn instrad or writing multiple Step definitions
- multiples Steps can be grouped into a single custom Action

existing public Actions might not solve a specific problem in a workflow

Custom Actions can contain any logic needed to solve a specific Workflow problem.

types of custom actions:
- JavaScrit Actions --> actions where the its logic is written in JavaScript
	- execute a JavaSript file 
	- use JavaScript (NodeJS) and any other package 
- Docker Actions --> containeeized acrtion, which create a Dockerfile with the required configuration.
	- perform any task(s) with any language
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

```yaml
name: 'Deploy to AWS S3'
description: 'Deploy a static website voa AWS S3'
inputs:
 ...
outputs:
 ...
runs: 
 using: 'node16'
 main: 'main.js'
```

the file for the `main` field must be created, but it can be any name. It will execute the `main.js` file whenever the custom action is used in a workflow step.

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

Custom Docker actions

It uses a `.py` file with all the logic behind the action that will be executed, a dockerfile that creates the environment where the code will run, and a requirements file specifiyng the packages that should be installed into the environemnt.

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


Security

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

--> only use your own actions 