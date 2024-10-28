It uses <strong style="color: #b16286">declarative approach</strong> to <span style="color: #d65d0e">IaC</span> with a pre-execution check to ensure that is will do what it's expected to do. <span style="color:#98971a">Terraform</span> can be used as a base tool in combination with <span style="color:#98971a">Ansible</span>, where <span style="color:#98971a">Terraform</span> provisions the base infrastructure and <span style="color:#98971a">Ansible</span> configures the software on top of it.

Is an open-source infrastructure automation tool created by Hashicorp, which helps to automate and manage Data Center infrastructure. Terraform is a declarative language (What to do).

The terraform it's cloud agnostic, environments can be deployed across multiple cloud or hybrid cloud --> achieved through providers. It does not depend on a single public cloud. Example: An organization may have the primary site in one cloud provider and the disaster recovery site in another cloud provider for the production environment.

> [!info]
> A provider helps Terraform manage third party platforms through their API.

Terraform is written in HCL, which sands for Hashicorp Configuration Language, which is a simple declarative language to define the infrastructure resources to be provisioned as blocks of code. The files has a `.tf` extension and can be created using any text editor. It's designed to be both human and machine readable.
HCL is build using code configuraton blocks.

type code configuation block types: Settings, Providers, Resource, Data, Input Variables, Local Variables, Output Values, Module.

`terraform version`

Terraform workflow: 
- Write Terraform Config  --> Init --> Plan Infrastructure  --> Deploy Infrastructure

TerraForm initializes the project and identifies the providers to be used for the target environment. During the plan phase TerraForm drafts a plan to get to the target state and then in the upload phase.

TerraForm will consider any file with the .tf extension within the configuration directory.

Terraform is  very much focused on the resource definition.

Makes the necessary changes required on the target environment to bring it to the desired estate.

Terraform tracks the state of the infra - .tfstate

Terraform providers are plugins that implement resources types for particular clouds platforms and generally speaking any remote system. with an API. Some popular providers are: AWS, Azure, GCP, VMware and Oracle.

>[!info]
>It has a pluggable architecture which ultimately users can define to terrafrom how to connect to the different remote systems and how can actually create, read, modify or update any of the resources that are supported by a given provider.

Terraform configuration can have one to many providers actually installed within the configuration.

`terraform providers` --> shows  which providers are required in the configuration.

vários providers podem ser utilizados no mesmo projeto e mesclar os recursos. Ex:  um recurso do kubernetes seja uma dependência do recurso do EKS.

Terraform Core is the installed version of Terraform that can be done on a Linux.

The `required_version` property allows to define a specific version of terraform that has to be used in a system. 

```
terraform {
	required_version = "~> 1.9.8"
}
```

>[!info]
>It's a good practice to define  a specific version for the provider, because Terraform isn't versioned on the same schedule as the Terraform providers.

To provide credentials to the backend platform: 
inside the provider block --> not recommended, it har code the credentiasl on th state file that can be versioned

```terraform
providers "aws" {
	region = "us-east-1"
	access_key = ""
	secret_key = ""
}
```

use environment variables:

`export AWS_ACCESS_KEY=""`
`export AWS_SECRET_KEY=""`

use share credentials or a configuration file:

```terraform
providers "aws" {
	region = "us-east-1"
	shared_credentials_file = "users/guilherme/.aws/creeds"
	profile = "guilherme-us-east-1"
}
```

userdata - best wat is to use a templatr system

interpolaton in terraform may contain conditions (if-else)
syntax --> `CONDITION ? TRUE : FALSE`
Example
`count = "${var.env == "prod" ? 2 : 1}"`

bultiin functions can be used terraform resources.
the syntac to call a funtion is `name(arg1, arg2, ...)` and wrapped with `${...}`
for example `${file("mykey.pub")}` would read the context of the public file.

For loops are typically used when assigning a value to an argument
Example: `[for s in var.list2: upper(s)]`
`tags = {for k, v in merge({ Name = "Myvolume" }, var.project.tags): k => lower(v)}`
For_each loops are used to repeat nested blocks.

the `lock` file is created when `terraform init` is executed. This file tracks the versions of providers and modules. It should be commited to git.

cases when state manipulation can be done:
- when upgrading between version, for example 0.11 -> 0.12 -> 0.13
- when you want to rename a resource in terraform without recreating it
- when you changed a key in a for_each, but you don't want to recreate the resources
- change position of a resource in a list `(resource[0], resource[1],...)`
- when you want oto stop managing a resource, but you don't want to destroy the resource `terraform state rm`
Ex: `terraform state mv <resource1.name1 resource1.name2>`

Benefits:
- Provides a high-level abstraction of infrastructure (IaC)
- Allows for composition and combination
- Supports parallel management of resources (graph, fast)
- Separates planning from execution (dry-run)

comments in Terraform:
`#` --> begins a single line comment, ending at the end of the line
`//` --> also a single-line comment, alternative to `#`
`/* */` --> multiple line comment that uses start and end delimiters

###### Terraform commands

`terraform init` --> command to initialize the working directory/project
- downloads and installs necessary plugins to execute the configuration
- Terraform uses a plugin based architecture to work with hundreds of such infrastructure platforms
- plugins are downloaded into a hidden directory called .terraform in the working directory
- hashicorp/local --> plugin also known as the source address. Identifier that is used by Terraform to locate and donwload the plugin from the registry. registry.terraform.io[Hostname]/hashicorp[Organizatioan Namespace]/local[Type] -- the hosname if the name of the registry where the plugin is located

`terraform validate` --> runs checks in the terraform file, to validade whether the configuration is syntactically valid and it's internally consistent. 
- primarily used for general verification of modules or the configuration file, including the correctness of attributes names and values types.

`terraform show` --> it displays the current state of the resource, including all the attributes.
- terraform show -json --> print the contents in JSON format.

`terraform plan` --> create an execution plan which shows a "plan" of deployment, it reads the current state file, and make sure that terraform state is up to date. it's going to compare the current configuration to prior state and it's going to note all the diferences.
- `--out` --> save the changes in a file. 
  Ex: `terraform plan --out changes.terraform`

`terraform apply` --> execute all the actions that were proposed in the terrafom plan
deploy the Infrastructure and statements in the code. If some resource are already deployed, this command will deploy updated code and tracking. it's goign to execute the configuration file.
- Ex: `terraform apply "myplan"`

`terraform destroy` --> destroy all resources found in state file. Its a non-reversible command.

`terraform providers` --> shows a list of all providers used in the configuration directory
- terraform providers mirror --> to copy provider plugins needed for the current configuration to another directory
- Ex: <code>$ terraform providers mirror /root/terraform/new_local_file</code>
 
`terraform output` --> print all output variables in the configuration directory
- `terraform output pet-name` --> print the value of a specific variable

terraform get --> download and update modules

`terraform refresh` --> Used to sync Terraform with the real world infrastructure
- useful to determine what action to take during the next apply. It won't modify any infrastructure resource, but it will modify the state file

terraform remote --> configure remote state storage

terraform state --> use it for advanced state management, e.g. Rename a resource with `terraform state mv aws_instance.example aws_instance.production`

terraform taint --> manually mark a resource as tainted, meaning it will be destroyed and recreated at the next apply
- Ex: `terraform taint aws_instance.example`

`terraform graph` --> used to create a visual representation of the dependencies in a Terraform configuration or an execution plan. A graph is generated in a format called dot
- We can pass it through a graph visualization software such as graphviz 
- Ex: <code>terraform grpah | dot - Tsvsg > graph.svg</code>
###### Terraform concepts

resource --> every object data that Terraform manages. A resource can be a file on a local host, a computer instance, a database server in the cloud or on a physical server on premise that Terraform manages.

>[!info]
>Each resource created and managed by TerraForm would have a unique ID which is used to identify the resources in the real world.

Terraform destroys the resource first before creating a new one in its place.

Even from resources that Terraform does not manage, it can read attributes such as the database name, host address or the DB user and use it to provision an application resource that is managed by TerraForm.

TerraForm can also import other resources outside of TerraForm that were either created manually or by the means of other IaC tools and bring it under its control so that it can manage those resources going forward.

Another common practice is to have one single configuration file that contains all the resource blocks required to provision the infrastructure. A single configuration file can have as many number of configuration blocks that you need. A common naming convention used for such a configuration file is to call it the main.tf.

TerraForm can read attributes of existing infrastructure components by configuring data sources. This can lead to be used for configuring other resources within TerraForm
The data source block consists of specific arguments for a data source. Data sources are also called data resources.

Meta arguments can be used within any resource block to change the behaviour of resources. That depends on for defining explicit dependency between resources and the lifecycle rules, which define how the resources should be created, updated and destroyed within TerraForm.

 One of the easiest ways to create multiple instances of the local file is to make use of the count meta argument. Ex: count = 3, We can make use of count index in the expression to make iterations --> filename = var.filename[count.index] # best way to do it
 
This built in function called length return the length of the list --> `count = length(var.filename)`

for_each --> only works with a map or a set
for_each = toset(var.filename)

toset --> convert the variable from a list to a set.

A Lifecycle rule allows to a resource to be created fisrt before the older one is deleted. Some options for the lifecycle: create_before_destroy, prevent_destroy --> useful to prevent your resources from getting accidentally deleted

The functionality of a provider plugin may vary drastically from one version to another. Order from configuration may not work as expected when using a version different than the one it was written in.

We can also combine the comparison operators like this to make use of a specific version within a range. pessimistic constraint operators --> defined by making use of the tilde greater than symbol --> ~> 1.2 This operator allows TerraForm to download the specific version or any available incremental version based on the value we provided.

terraform console --> command line that allows to test terraform variables. 

Just as in any general purpose programming language such as Bash, scripting or PowerShell, we can make use of input variables in TerraForm to assign variables.
variables in terraform. Ex: `variable "myvar" {}`
it has a default value and a type.
A best practice is to create a variables.tf file to use input variables
simple variable types: string, number, bool
complex types: `list(type`, `set)type`, `map(type`, `obejct({<ATTR NAME> = <TYPE>, ...})`, `tuple({<TYPE>,...})`
The basic variable types that can be used are string number, boolean. TerraForm also supports additional types such as list, map, set, object and tuple.
The most common types are list and map.
use variables for elements that might change (generic)
make it easier to reuse terraform files

we can also make use of command line flags. We can pass an as many variables as we want with this method by making use of the dashboard flag multiple times. terraform apply -var "filename=/root/pets.txt" -var "content=We love Pets!"

We can also make use of environment variables with TF_VAR followed by the name of a declared variable. Ex: export TF_VAR_filename="/root/pets.txt"

when we're dealing with a lot of variables, we can load values by making use of variable definition files. These variable definition files can be named anything but should always end in either .tfvars or .tfvars.json. The variable definition file if called .tfvars or .tfvars.json or by any other name ending with *.auto.tfvars or *.auto.tfvars.json will be automatically loaded by TerraForm.

If you use any other file name such as variable.tfvars for example, you will have to pass it along with a command line flag: terraform apply -var-file variables.tfvars

variable definition precedence: -var or -var-file --> *.auto.tfvars --> terraform.fvars --> environment variables

Along with input variables, TerraForm also supports output variables. These variables can be used to store the value of an expression in TerraForm. inside this block. The mandatory argument for value is the reference expression. We can also add a description, which is an optional argument to describe what this output variable will be used for.

standardized AMIs : using file uploads, using remote exec, automation tools like ansible, chef which is integrated within terraform. puppet gent can be run using remote-exec.

output

Modules --> make terraform more organized
- use third party modules --> modules from GitHub 
- reuse parte of the code

providers
Google Cloud, Azure, Heroku, Digital Ocean.
###### Terraform State

By default state is stored loccally in the directory that terraform is executed.

Terraform will use state each time terraform plan and apply is executed. Terraform is going to compare any chnages that extis in the state file, and indicate to the user ythe necessary chnages to be applied, in order to ensure that the managed resources math the desired state.

it uses it as a single source of truth when using commands such as TerraForm Plan and Apply. If you make a change to the configuration file now and rerun the TerraForm Plan or apply Command. TerraForm, by default, refreshes the state again and compares it against the configuration file. When Terraform creates a resource, it records its identity in the state.

The state is a blueprint of the infrastructure deployed by Terraform. `terraform.tfsate` file --> created as a consequence of data from apply command. This file is not created until later from apply Command is run at least once. The state file is a JSON data structure that maps the real world infrastructure resources to the resource definition in the configuration files.

One other benefit of using state is performance. When dealing with a handful number of resources, it may be feasible for TerraForm to reconcile state with the real world infrastructure after every single TerraForm command such as plan or apply.

The final benefit of state that we are going to look at is collaboration when working as a team. Every user in the team should always have the latest state data before running TerraForm In such a scenario, it is highly recommended to save the State Farm State file in a remote data store rather than to rely on a local copy. State is a non optional feature in TerraForm.

The state file contains sensitive information within it. It contains every little detail about our infrastructure. The state may also store initial passwords when using local state. The state is stored in plain text JSON files. make sure that the state file is always stored in a secure storage. store the state in remote backend systems such as CSS three, Google Cloud Storage, Azure Storage, Terraform Cloud, etc. Terraform State is a JSON data structure that is meant for internal use within Terraform. We should never manually attempt to edit the state files ourselves.

The default is a local backend (the local terraform state file).
Other backends include:
- S3 (with locking mechanism using DynamoDB)
- consul (with locking)
- terraform enterprise (the commercial solution)

some backends will enable remote operations. The terraform apply will run completely remote --> enhance backends.

`terraform state list` --> show a list with less details of the resources that's current managing.

