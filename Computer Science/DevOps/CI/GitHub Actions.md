GitHub Actions is a <strong style="color: #b16286">CI/CD platform that enables to automate the build, test and deploy GitHub workflow</strong>. It only works with and it's it's integrated into GitHub as a service. It allows to treat CI pipeline as code, which uses a <span style="color:#98971a">.ghithub/workflows</span> folder to store workflow definition as <span style="color:#98971a">.yaml</span> file.

> It doesn't matter the name of the YAML files because each file describes when they should be triggered.

<span style="color: #d65d0e">GitHub Actions Marketplace</span> hosts actions for workflows

<strong style="color: #d79921">Initial setup</strong>
- .github --- workflows --- { ci.yaml - cd.yaml - publish.yaml }

<strong style="color: #d79921">Basic concepts</strong>

Workflow <span style="color: #3588E9">--></span>  series of automated procedures represented as jobs and steps that GitHub Actions executes.
- Every repository can have any number of workflows.

Each workflow has the components: EVENT, RUNNER, JOBS, STEPS, ACTIONS

>[!info]
>EVENT ---> RUNNER ---> JOB ---> STEPS ---> ACTIONS

- <span style="color:#98971a">EVENT</span> <span style="color: #3588E9">--></span> Something that activates the execution of a workflow. Ex: push to a repo, create a pull request, etc..
- <span style="color:#98971a">RUNNER</span> <span style="color: #3588E9">--></span>  Servers that runs jobs on a specific platform or OS. There are built-in runners for different virtual environments, or a self-hosted runner can be used in a owned environment.
- <span style="color:#98971a">JOBS</span> <span style="color: #3588E9">--></span>  Made for steps that are performed onf the same runner. In case a workflows has more than 1 job, they are executed in parallel by default, but they can be configured to declare that one is dependent on another. (serially execution based on their dependencies).
- <span style="color:#98971a">STEPS</span> <span style="color: #3588E9">--></span>  Tasks comprising one or more shell commands or actions, each job can contain one or more steps. Ex: one step can check out the code, another step might compile the code.
- <span style="color:#98971a">ACTIONS</span> <span style="color: #3588E9">--></span>  procedures tha can be executed within a step.

>[!note]
>Actions are the lowest level of a workflow

Events are created with on keyword

Jobs runs in an isolated environment (VM or Docker container)

Steps can have an optional name specified by the ‘name:’ keyword that displays in the report. It’s best to name your steps something descriptive so that when you look at the report, you know exactly what's going on in each step.

Steps can have an optional ID specified by the ‘id:’ keyword, making it really helpful to refer to them in other steps. useful when you want to use the output of one step as the input parameters for another step.

Steps have either an action specified by the ‘uses:’ keyword or shell commands specified by the ‘run:’ keyword. You can specify more than one shell command by starting with a vertical bar and then placing each command on a new line. 

Steps can also have defined environment variables (env:) --> n true 12-factor fashion, you should be configuring your services through environment variables

Actions are procedures that can be executed within a step. Defining actions requires the ‘uses:’ keyword followed by the name of the action.

actions can have arguments to configure them by specifying the ‘with:’ keyword followed by name-value pairs. Some actions use the ‘args:’ keyword. read the actions documentation to explore all options.