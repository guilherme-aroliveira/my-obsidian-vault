It uses <strong style="color: #b16286">declarative approach</strong> to <span style="color: #d65d0e">IaC</span> with a pre-execution check to ensure that is will do what it's expected to do. <span style="color:#98971a">Terraform</span> can be used as a base tool in combination with <span style="color:#98971a">Ansible</span>, where <span style="color:#98971a">Terraform</span> provisions the base infrastructure and <span style="color:#98971a">Ansible</span> configures the software on top of it.

Is an open-source infrastructure automation tool created by Hashicorp, which helps to automate and manage Data Center infrastructure. Terraform is a declarative language (What to do).

The terraform it's <strong style="color: #d79921">cloud agnostic</strong>, environments can be deployed across multiple cloud or hybrid cloud <span style="color: #3588E9">--></span> achieved through providers. <strong style="color: #b16286">It does not depend on a single public cloud</strong>. <strong style="color: white">Example:</strong> an organization may have the primary site in one cloud provider and the disaster recovery site in another cloud provider for the production environment.

<strong style="color: white">Benefits:</strong>
- Provides a high-level abstraction of infrastructure (IaC)
- Allows for composition and combination
- Supports parallel management of resources (graph, fast)
- Separates planning from execution (dry-run)

Terraform workflow: 
- Write Terraform Config  <span style="color: #3588E9">--></span> Init <span style="color: #3588E9">--></span> Plan Infrastructure  <span style="color: #3588E9">--></span> Deploy Infrastructure

Terraform is written in <span style="color: #d65d0e">HCL (Hashicorp Configuration Language)</span> and is designed to be both human and machine readable. 

<span style="color: #d65d0e">HCL</span> a simple <strong style="color: #b16286">declarative language to define the infrastructure resources</strong> to be provisioned using code configuration blocks. The files has a `.tf` extension and can be created using any text editor. 

```hcl
# Template
	<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
	 # Block body
	<IDENTIFIER> = <EXPRESSION> # Argument
}

# AWS EC2 Example
resource "aws_instance" "web_server" { # BLOCK
	ami = "ami-04d29b6f966df1537" # Argument
	instance_type = var.instance_type # Argument with value as expression (Variable value replaced 11 
}
```

>A block in Terraform contains information about the infrastructure platform and a set of resource within that platform that is going to be created.

Terraform Code Configuration block types: Settings, Providers, Resource, Data, Input Variables, Local Variables, Output Values, Module.

<strong>Terraform Based Architecture</strong>

Terraform relies on plugins called "<span style="color: #d65d0e">providers</span>" to interact with remote systems and expand functionality.

Terraform providers are <strong style="color: #b16286">plugins that implement resources types for particular clouds platforms</strong> and generally speaking any remote system with an API. Terraform configurations must declare which providers they require, so that Terraform can install and use them.

> [!info]
> A provider helps Terraform manage third party platforms through their API.

Popular Terraform Providers include: AWS, Azure, Google Cloud, VMware, Kubernetes and Oracle.

Terraform configuration can have one to many providers actually installed within the configuration. <strong style="color: white">Example</strong>: a kubernetes resource can be a dependency from an EKS resource.

The `required_version` property allows to define a specific version of terraform that has to be used in a specific system. 

```hcl
terraform {
  required_version = ">= 1.0.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"
    }
```

Terraform initializes the project and identifies the providers to be used for the target environment.

<span style="color: #d65d0e">Terraform Core</span> is the installed version of Terraform that can be done on a Linux.

>[!info]
>It's a good practice to define  a specific version for the provider, because Terraform isn't versioned on the same schedule as the Terraform providers.

Run a `terraform init`  to install the providers specified in the configuration:

```shell
terraform init
```

To know which providers are installed in the working directory and those required by the configuration, issue a `terraform version` and `terraform providers` command.

```shell
terraform version
```

To configure a Terraform provider:

```hcl
provider "aws" {
	region = "us-east-1"
}
```

The AWS Terraform provider offers a flexible means of providing credentials for authentication. The supported methods are: Static credentials, Environment variables, Shared credentials.

To see a list of all providers used in the configuration directory:

```shell
terraform providers
```

The command `terraform providers mirror ` allows to copy provider plugins needed for the current configuration to another directory.

```shell
terraform providers mirror /root/terraform/new_local_file
```

<strong style="color: #d79921">Shared credentials</strong>

```hcl
provider "aws" {
	region = "us-east-1"
	access_key = "my-access-key"
	secret_key = "my-secret-key"
}
```

>[!note]
>inside the provider block --> not recommended, it har code the credentiasl on th state file that can be versioned

<strong style="color: #d79921">Environment variables</strong>

The aws credentials can be provided via the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`, environment variables, representing the AWS Access Key and AWS Secret Key, respectively.

```shell
export AWS_ACCESS_KEY_ID="anaccesskey"
export AWS_SECRET_ACCESS_KEY="asecretkey"
export AWS_DEFAULT_REGION="us-east-1"
```

<strong style="color: #d79921">Shared credentials</strong>

The AWS credentials or configuration file can be used to specify the credentials. The default location is `$HOME/.aws/credentials` on Linux and macOS.

Optionally a different location can be specified in the Terraform configuration by providing the shared_credentials_file argument or using the `AWS_SHARED_CREDENTIALS_FILE` environment variable. This method also supports a profile configuration and matching `AWS_PROFILE` environment variable.

```hcl
provider "aws" {
	region                  = "us-east-1"
	shared_credentials_file = "[/users/tf_user/.aws/creds]"
	profile                 = "customprofile"
}
```

>[!note]
>The functionality of a provider plugin may vary drastically from one version to another. Order from configuration may not work as expected when using a version different than the one it was written in.

`terraform.lock` file --> hashicorp hashes out the provider version so that Terraform can do a comparison during the `terrafrom init` command. This file tracks the versions of providers and modules and it <strong style="color: #d79921">should be commit</strong> to git.

<strong>Terraform Concepts</strong>

Terraform uses <span style="color: #d65d0e">resources block</span> to <strong style="color: #d79921">manage infrastructure</strong>, such as virtual networks, comute instances, or higher-level components such as DNS records. 

<span style="color: #d65d0e">Resource blocks</span> <strong style="color: #b16286">represent one or more infrastructure objects in the terraform configuration</strong>. A resource can be a file on a local host, a computer instance, a database server in the cloud or on a physical server on premise that Terraform manages.

```hcl
# Template
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
	# Block body
	<IDENTIFIER> = <EXPRESSION> # Argument
}
```

<strong style="color: white">Example</strong>

```hcl
resource "aws_s3_bucket" "my-new-S3-bucket" {   
  bucket = "my-new-tf-test-bucket-bryan"
}
```

Within a resource block, there are arguments that are specific to the type of resource that will be deployed.

> Terraform will consider any file with the .`tf` extension within the configuration directory.

The `show` command displays the current state of the resource, including all the attributes. 

```shell
terraform show
```

The `-json` option prints the contents of a resource in a JSON format.

Most Terraform providers have a number of different resources that map to the appropriate APIs to manage that particular infra type.

>[!info]
>Each resource created and managed by TerraForm would have a unique ID which is used to identify the resources in the real world.

Terraform destroys the resource first before creating a new one in its place.

Even from resources that Terraform does not manage, it can read attributes such as the database name, host address or the DB user and use it to provision an application resource that is managed by Terraform.

>[!note]
>Terraform can also import other resources outside of Terraform that were either created manually or by the means of other IaC tools and bring it under its control so that it can manage those resources going forward.

Just as in any general purpose programming language such as Bash, scripting or Python, is possible to make use of <span style="color: #d65d0e">input variables</span> in Terraform to assign variables.

<span style="color: #d65d0e">Input variables</span> allows aspects of a module or configuration to be customized without altering the module's own source code. This allows modules to be shared between different configurations.

Input variables (commonly referenced as just variables) are often declared in a separate file called `variables.tf`, although this is not required. Each variable used in a Terraform configuration <strong style="color: #d79921">must be declared before it can be used</strong>, which has its own block.

```hcl
variable "VARIABLE_NAME" {
	# Block body
	type = <VARIABLE_TYPE>
	description = <DESCRIPTION>
	default = <EXPRESSION>
	sensitive = <BOOLEAN>
	validation = <RULES>
}
```

<strong style="color: white">Example:</strong>

```hcl
variable "vpc_cidr" {
	description = "CIDR Block for the VPC"
	type = string
	default = "10.0.0.0/16"
}

resource "aws_vpc" "main_vpc" {
	cidr_block = var.cidr_block
}
```

> Input variables make the Terraform configuration more flexible.

To call a variable on a resource or module: `var.<variable_name>`

>[!note]
>A best practice is to create a `variables.tf` file to use input variables

Variable - <strong style="color: white">order of precedence:</strong>
1. `-var` and `-var-file`
2. `*.auto.tfvars or .auto.tfvars.json`
3. `terraform.tfvars.json`
4. `terraform.tfvars` file
5. environment variables
6. variable defaults

To change the value of a variable on the terminal:

```shell
terraform apply -var="web_subnet=10.0.20.0/24"
```

A `.tfvars` file can be specified using the `-var-file` option at the command line.

```shell
terraform plan -var-file="prod.tfvars"
```

The basic variable types that can be used in Terraform, are string number, boolean. Terraform also supports additional types (complex types) such as list, map, set, object and tuple, which the most common are list and map.

Variables can also be specified with environment variables on the terminal

```shell
export TF_VAR_subnet_zone="us-east-1a"
```

The `terraform console` command allows to test terraform variables on the terminal.

```shell
terraform console
```

To interpolate variables in strings:

```hcl
"Name" = "Production ${var.main_vpc.name}"
```

<span style="color: #d65d0e">Local block</span> (often referred to as locals) are <strong style="color: #b16286">defined values in Terraform that are used to reduce repetitive references</strong> to expressions or values. Locals are defined in `locals block` (plural) and include named local variables with their defined values.

Local values are placeholders that can reused throughout the configuration.

```hcl
locals {
	# Block body
	local_variable_name = <EXPRESSION OR VALUE>
	server = "ec2-${var.environment}-api-${var.variables_sub_az}"
	common-tags = {
		Environment = "dev"
		ManagedBy = "terraform"
	}
}

tags = {
	Name = local.server_name
}
```

The `console` command retrieves values from the `locals.tf` file

```shell
terrarom console
> local.common-tags
```

<span style="color: #d65d0e">Data sources</span> are <strong style="color: #b16286">used in Terraform to load or query data</strong> from APIs or other Terraform `workspaces`. To use data sources, declare it using a `data block` in the Terraform configuration.

> Data sources are API that fetches dynamic data from cloud providers. 

Data block within Terraform HCL are comprised of the following components:
- Data Block - "resource" is a top-level keyword like "for" and "while" in other programming languages.
- Data Type - The next value is the type of the resource. Resources types are always prefixed woth their provider.
- Dta Local Name - The next value o=is the name of the resource. The resource type and name together from the resource identifier, or ID, which mus tbe uniquer for a give nconfiguration, even if multiple files are used.
- Data Arguments - Most of the arguments within the body of a resource block are specifies to the selected resource type.

<strong style="color: white">Example:</strong> A data block request that Terraform read from a given data source ("`aws_ami`") and export the result under the given local name ("example"). The name is used to refer to this resource from elsewhere in the same Terraform module.

```hcl
data "<DATA TYPE>" "<DATA LOCAL NAME>"{
	# Block body
	<IDENTIFIER> = <EXPRESSION> # Argument
}
```

<strong style="color: white">Example:</strong>

```hcl
#Retrieve the AWS region
data "aws_region" "current" { }

#Define the VPC
resource "aws_vpc" "vpc" {
	cidr_block = var.vpc_cidr

	tags = {
		Region = data.aws_region.current.name
	}
}
```

A <span style="color: #d65d0e">module</span> is <strong style="color: #b16286">used to combine resources that are frequently used together into a reusable container</strong>. Individual modules can be used to construct solution required to deploy applications.

>[!note]
>When creating modules, make sure that variables are being used everywhere, and its being made as flexible as possible.

Modules <span style="color: #3588E9">--></span> make terraform more organized
- use third party modules <span style="color: #3588E9">--></span> modules from GitHub 
- reuse parte of the code

Modules are called by a parent or a <strong style="color: #d79921">root module</strong>, and then any modules that his parent module calls are actually known as <strong style="color: #d79921">child modules</strong>.

Modules can be used from a number of different locations, including remote locations such as the Terraform module registry, or locally within a folder. While not required, local modules are commonly saved in a folder called `modules`, and each module is named for its respective function inside that folder.

```hcl
module “<MODULE_NAME>” {
  # Block body
  source = <MODULE_SOURCE>
  <INPUT_NAME> = <DESCRIPTION> #Inputs
  <INPUT_NAME> = <DESCRIPTION> #Inputs
}
```

<strong style="color: white">Example:</strong>

```hcl
module "vpc" {
  source = "./modules/vpc"
}
```

Along with input variables, Terraform also supports output variables. These variables can be used to store the value of an expression.

<span style="color: #d65d0e">Terraform output</span> values <strong style="color: #b16286">allow to export structured data</strong> about the resources. Outputs are also necessary to share data from a child module the root module.

```hcl
output "<NAME>" {
	# Block body
	value = <EXPRESSION> # Argument
}
```

>[!info]
>Output values are like functions returning values.

>outputs are a way to export data from individual modules. The root module can use outputs to print values ta the terminal after running terraform values.

>[!note]
>The mandatory argument for value is the reference expression. A description can also be added, which is an optional argument to describe what this output variable will be used for.

<strong style="color: white">Example:</strong>

```hcl
output "vpc_id" {
	description = "Output the ID for the primary VPC"
	value = aws_vpc.main_vpc.id
}
```

<span style="color: #d65d0e">Output declarations</span> can appear anywhere in the terraform files, but <strong style="color: #d79921">it's recommended</strong> to put them into a separate file called `output.tf`

Output values can be designated as <strong style="color: #d79921">sensitive</strong>, and terraform won't print them in the console. To declare it as sensitive add the argument with its value to the output block.

```hcl
output "vpc_id" {
	description = "Output the ID for the primary VPC"
	value = aws_vpc.main_vpc.id
	sensitive = true
}
```

The `output` command prints all outputs variables that are in the configuration directory. 

```shell
terraform output
```

The `-json` flag generates JSON formatted output, so that it can be easily parsed by other applications.

To print the value of a specific output variable:

```shell
terraform output <variable_name>
```

The output can be redirected to file any time using shell redirection

```shell
terraform output -json > outputs.json
```

<strong>Commenting Terraform Code</strong>

The <strong style="color: #d79921">use of comment</strong> is a way to make the code easier to understand for others who might want to contribute.

```hcl
# begins a single-line comment, ending at the end of the line.
```

```hcl
// also begins a single-line comment, as an alternative to #.
```

```hcl
/* and */ are start and end delimiters for a comment that might span over multiple lines.
```

<strong style="color: white">Example:</strong>

```hcl
# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}
```

```hcl
/*
Name: IaC Buildout for Terraform Associate Exam
Description: AWS Infrastructure Buildout
*/

# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}
```

<strong>Multiple Terraform Providers</strong>

Due to the plug-in based architecture of Terraform providers, it is easy to install and utilize <span style="color: #d65d0e">multiple providers</span> within the same Terraform configuration.

```hcl
terraform {
	required_providers {
	    aws = {
	      source = "hashicorp/aws"
	    }
	    tls = {
		    source  = "hashicorp/tls"
		    version = "3.1.0" 
		}
	}
}
```

Run a `terraform init -upgrade` to validate you pull down the provider versions specified in the configuration and validate with a `terraform version` or a `terraform providers` command.

```shell
terraform init -upgrade
```

You can modify the version line of the AWS provider to be as specific or general as desired. Update the `version` line within your `terraform.tf` file to try these different versioning techniques.

```shell
version = "~> 3.0"
version = ">= 3.0.0, < 3.1.0"
version = ">= 3.0.0, <= 3.1.0"
version = "~> 2.0"
version = "~> 3.0"
```

<strong>Terraform Provisioners</strong>

<span style="color: #d65d0e">Provisioners</span> can be used to model specific actions on the local machine or on a remote machine in order to prepare servers or other infrastructure objects for service.

The `local-exec` provisioner invokes a local executable after a resource is created. 

```hcl
provisioner "local-exec" {
  command = "chmod 600 ${local_file.private_key_pem.filename}"
}
```

The `remote-exec` provisioner runs remote commands on the instance provisioned with Terraform.

```hcl
  provisioner "remote-exec" {
    inline = [
      "sudo rm -rf /tmp",
      "sudo git clone https://github.com/hashicorp/demo-terraform-101 /tmp",
      "sudo sh /tmp/assets/setup-web.sh",
    ]
  }
```

>[!info]
>Provisioners are used to execute scripts on a local or remote machines as part of resource creation or destructive.

The command `terraform fmt` allows to format the all Terraform files of a single project. The `-diff` flag shows in details the changes that have been made. 

The `-check` flag checks the files and don't override them, and the `-recursive` flag, formats all the files in sub-directories. 

```shell
terraform fmt -diff
```

The terraform `taint` command allows to <strong style="color: #b16286">manually mark a resource for recreation</strong>. It informs Terraform that a particular resource needs to be rebuilt even if there has been no configuration change for that resource.

```shell
terraform taint aws_instance.web_server
```

>[!note]
>As of Terraform 15.2 the `taint` command is actually deprecated.

An alternative method is to replace a resource through the `-replace` option during the apply <span style="color: #3588E9">--></span> recommended approach

```shell
terraform apply -replace="aws_instance.web_server"
```

Terraform can also import other resources outside of it that were either created manually or by the means of other IaC tools and bring it under its control so that it can manage those resources going forward.

To manage existing resources there weren't created by Terraform use the `import` command, which adds these resources to the state file.

>[!note]
>It's important to add the resource to the configuration, the required arguments must be included.

```shell
terraform import aws_instance.aws_linux <resource_id>
```

<strong>Terraform Workflow</strong>

The `terraform init` command initialize the working directory/project, it also downloads and installs necessary plugins to execute the configuration.

```shell
terraform init
```

It will retrieve source code for any reference modules, and copy them locally. It will also source all the providers that are used in the configuration file.

The `init` is also going to connect to the backend.

>[!note] 
>plugins are downloaded into a hidden directory called `.terraform` in the working directory

To restore the current configuration to the same remote state:

```shel
terraform init -reconfigure
```

The `validate` command validates the configuration files in a directory, referring only to the Terraform configuration. It runs checks that verify whether the configuration is syntactically valid and it's internally consistent.

```shell
terraform validate
```

>It's primarily used for general verification of modules or the configuration file, including the correctness of attributes names and values types.

Terraform validate <strong style="color: #d79921">doesn't check</strong> with the backend providers to validate if the provided input is actually valid.

The `terraform plan` command compare the state file, which contain the current configuration to prior state and it's going to note all the diferences.

```shell
terraform plan
```

The `--out` option saves the output to a specific name.

```shell
terraform plan -out myplan
```

Plans can be saved to a file to guarantee what will happen

```shell
terrform plan -out=myplan
```

The `terraform apply` command will execute all the actions proposed during the `plan` command. It executes the configuration file and deploys the infrastructure.

```shell
terraform apply myplan
```

The `terraform destroy` delete all remote objects (resources) managed by a particular Terraform configuration. Its a non-reversible command.

```shell
terraform destroy
```

The `-auto-approve` flag deletes all resources without confirming with the user. 

>[!info]
>The `destroy` command does not delete the configuration file(s). It destroys the resources built from the terraform code.

The `-destroy` simulates a destroy action.

```shell
terraform plan -destroy
```

<strong>Terraform modules</strong>

A <span style="color: #d65d0e">module</span> is a set of Terraform configuration files in a single directory. Even the simplest configuration consisting of a single directory with one `.tf`.

Terraform <strong style="color: #b16286">modules help to organize configuration</strong>, re-use configuration and provides consistency and ensure best practices. It's a way to reuse code.

The root configuration (also called your <strong style="color: #d79921">root module</strong>) consist of the resources defined in the `.tf` files in the working directory. The root module is the <strong style="color: #d79921">calling module</strong>.

All the configuration that are imported from other directories into the root module are called <strong style="color: #d79921">child modules</strong>. There are two types of modules: local and remote.

To organize, encapsulate, and reuse configuration, all child modules are created under the `modules` directory and are called on the root module. Modules name <strong style="color: white">must</strong> be unique.

```hcl
module "vpc" {
  source          = "../modules/vpc"
  subnet_id = module.vpc.web_subnet.id
}
```

To transform an input from optional to required, is by removing the `default` value from the input block.

```hcl
variabe "size" {
	# default = "t2.micro"
}
```

Modules can be sourced from a number of different locations, including both local and remote sources. 

The <span style="color: #d65d0e">remote modules</span> are loaded from a remote source such as Terraform Registry and are created and maintained by HashiCorp, it's partners and by third parties. 

Terraform Public Registry is an index of modules shared publicly. This public registry is the easiest way to get started with Terraform and find modules created by others in the community.

>[!note]
>Modules are the key to write reusable, maintainable and testable Terraform code. It is a good practice to start building everything as module. Create a library of modules to share with the team.

Installing the module means downloading remote modules into `.terraform` directory, or if the module is local, it will only create a reference to it.

<span style="color: #d65d0e">parametizing modules</span> <span style="color: #3588E9">--></span> the best practice is to use the same names for variables declared both int root and in child modules.

<strong style="color: #d79921">After importing</strong> child modules into the root module, the `terraform init` command must be executed.

Modules on the public Terraform Registry can be sourced using a registry source address of the form `//`, with each module's information page on the registry site including the exact address to use.

```hcl
module "autoscaling" {
	source  = "terraform-aws-modules/autoscaling/aws"
	version = "4.9.0"
}
```

Modules on the public Terraform Registry can be sourced using a registry source address of the form `<NAMESPACE>/<NAME>/<PROVIDER>`, with each module's information page on the registry site including the exact address to use.

Each module in the Terraform Public registry is versioned. These versions syntactically must follow semantic versioning. The version argument can be specified as part of the module block.

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "3.11.0"
}
```

Another source of modules that be can used are those that are published directly on GitHub. Terraform will recognize unprefixed github.com URLs and interpret them automatically as Git repository sources.

```
module "autoscaling" {
  source = "github.com/terraform-aws-modules/terraform-aws-autoscaling?ref=v4.9.0"
```

A child module can use outputs to expose a subset of its resources attributes to a parent module.

```hcl
output "vpc_id" {
	value = aws_vpc_.main_vpc.id
}
```

A module's outputs can be accessed as read-only attributes on the module object, which is available within the configuration that calls the module. To reference these outputs in expressions, they use the following syntax:

`module.<MODULE NAME>.<OUTPUT NAME>`

```hcl
resource "aws_subnet" "public" {
	vpc = module.aws_vpc.vpc_main.id
}
```

>Modules outputs are the only supported way for users to get information about the resources that have been configured within a child module.

To view the outputs returned by any module and their values, the `console` command be used for it.

```shell
terraform console
```

<strong>Terraform Workspaces</strong>

Workspaces is a Terraform feature that allows to organize infrastructure by environments and variables in a single directory.

>[!info]
>Terraform is based on a stateful architecture and therefore stores state about the managed infrastructure and configuration. This state is used by Terraform to map real world resources to the configuration, keep track of metadata, and to improve performance for large infrastructures.

The persistent data stored in the state belongs to a Terraform workspace. Initially the backend has only one workspace, called "default", and thus there is only one Terraform state associated with that configuration.

>[!note]
>The default workspace can't be deleted

 The `workspace` command allows to check which workspace you is being used by Terraform.

```shell
terraform workspace
```

The `-help option` shows a list of the option within the `worksapce` command

To create a new workspace:

```shell
terraform workspace new development
```

To move between terraform workspaces:

```shell
terraform workspace select default
```

> Workspaces isolate their state, if `terraform plan` is executed, Terraform will not see any existing state for this configuration.

<strong>Terraform state</strong>

Terraform stores and operates on the state of the managed infrastructure. Terraform uses this <span style="color: #d65d0e">state</span> on each execution to make plan and make changes. This state must be stored and maintained on each execution so future operations can be performed correctly.  

The location and method of operation of Terraform's state is determined by the Terraform <span style="color: #d65d0e">backend</span>. By default Terraform uses a local backend, where state information is stored and acted upon locally within the working directory in local file name `terraform.tfstate`.

>[!note]
>The <span style="color: #d65d0e">local state</span> file is indexed in JSON format and stored on disk, even though the local state file is editable, <strong style="color: #d79921">direct file editing is not recommended</strong>. It's meant for internal use within Terraform. 

The local state must always be up to date before a person or process runs Terraform. If the state is out of sync, the wrong operation might occur, causing unexpected results.

>Terraform basically compares the configuration with the state file and the existing infrastructure to create, place and make changes to the infrastructure, in order to ensure that the managed resources match the desired state.

Cases when state manipulation can be done:
- when upgrading between version, for example 0.11 -> 0.12 -> 0.13
- to rename a resource in terraform without recreating it
- when changing a key in a for_each, but you don't want to recreate the resources
- change position of a resource in a list `(resource[0], resource[1],...)`

To `state` command is used for advanced state management, which is the recommended way to make changes on the Terraform state file. It can also be used to see the options for performing more granular operations.

```shell
terraform state
```

To show an json output of the `.tfsate` file:

```shell
terraform show state
```

To show an specific resource:

```shell
terraform state show aws_instance.web_server
```

To list all resource on the `.tfsate` file:

```shell
terraform state list
```

To rename a resource:

```shell
terraform state mv aws_instance.server aws_instance.web_server
```

To stop stop managing a resource without destroying it:

```shell
terraform state rm <resource_name>
```

If supported, the state backend will "lock" to prevent concurrent modifications which cloud cause corruption. Locking on state allows to make sure to protect the state from being written by multiple users at the same time.

Using the `apply` command with a locking mechanism:

```shell
# timeout if the lock doesn't free up within 60 seconds
terraform apply -lock-timeout=60s
```

The `terraform refresh` command reads the current settings from all managed remote objects found in Terraform state and updates the Terraform state to match configuration drift.
- it's useful to determine what action to take during the next apply. It won't modify any infrastructure resource, but it will modify the state file

> It's done automatically as part of the `plan` and `apply` process.

Refreshing state is the first step of the `terraform plan` process: read the current state of any already existing remote objects to make sure that the Terraform state is up-to-date.

To perform the first part of the `terraform plan`:

```shell
terraform plan -refresh-only
```

>[!note]
>The `terraform refresh` command is deprecated, and it 's because the provider may be misled into thinking that all of the managed objects have been deleted.

Backends define how operations are executed and where the Terraform `.tfstate` is stored. Each Terraform configuration has an associated backend with different set of configurations, that deals with authentication in a little different way. 

Terraform backends are actually configured inside the Terraform configuration block. In case of the default backend it's configuration doesn't need to be explicit.

```hcl
terraform {
  backend "local" {
    path = "terraform.tfstate"
  }
}
```

>[!note]
>Terraform only can accept a single backend for any given working directory.

It's important to protect terraform state data as it can contain extremely sensitive information <span style="color: #3588E9">--></span> store it in a backend that supports encryption.

Most backends support security and collaboration features so using a backend is a must-have both from a security and teamwork perspective.

The most popular backends are:
- AWS S3 Backend (with DynamoDB - locking)
- Consul (with locking)
- Terraform Enterprise (the commercial solution)
- Google Cloud Storage Backend
- Azure Storage Backend

>[!info]
>The Terraform `remote` backend stores Terraform state and may be used to run operations in Terraform Cloud. This backend supports the ability to store Terraform state information and perform operations all within Terraform Cloud, based on privileged access.

It's necessary to have a valid set of access key for authentication to be able to read information from the state. To invalid the backend authentication: 

```shell
export AWS_ACCESS_KEY_ID="notvalid"
```

The are only two enhanced backends: local and remote. The remote backend stores Terraform state and may be used to run operations in Terraform Cloud.

When using full remote operations, operations like terraform plan and terraform apply can be executed in Terraform Cloud's run environment, with log output streaming to the local terminal.

```hcl
terraform {
	backend "remote" {
		hostname = "app.terraform.io"
		organization = "Terraform Cloud"
		workspaces {
			name = "my-aws-app"
		}
	}
}
```

> The remote backend also works with Terraform Enterprise.

Terraform provides a longing method to authenticate using the remote enhanced backend. 

```shell
terraform login
```

>it generates an API token to be able to authenticate into the Terraform Cloud remote backend.

The `s3` backend supports encryption, which reduces worries about storing sensitive data in state files.

To use a remote backend:

```hcl
terraform {
	backend "s3" {
		bucket = "bucket_name"
		key = "dev/backend.tfsate"
		dynamodb = "table_name"
		region = "aws_region"
		encrypt = true
	}
}
```

To migrate the state from backends:

```shel
terraform init -migrate-state
```

Any time a change is made to the backend configuration, it must be reconfigured.

```shell
terraform init -reconfigure
```

>[!info]
>Terraform backends do not support interpolation within a configuration block. But it does support the ability to specify partial backend configuration.

The partial configuration can be provided via a file or within the command line using the `-backend-config` option. 

```hcl
path="state_data/terraform.dev.tfstate"
```

```shell
terraform init -backend-config=state_config/dev_local.hcl
```

Using an S3 backend:

```hcl
bucket = "my-terraform-state-ghm"
key = "dev/aws_infra"
region = "us-east-1"
```

```shell
terraform init -backend-config=state_config/dev-s3-state.hcl
```

>[!info]
>If backend settings are provided in multiple locations, the top level settings are merged such that the command line options will override the settings in the main configuration.

<strong>Debugging</strong>

Terraform allows to enable logging in order to do some troubleshooting. This can be done by setting `TF_LOG` environment variable to any value. The log levels are trace, debug, info, warn or error.  

```shell
export TF_LOG=TRACE
# trace is the most verbose level
```

The environment variable `TF_LOG_PATH` allows to debug to a log file

```shell
export TF_LOG_PATH="terraform_log.txt"

# The configuration must be updated
terraform init -upgrade
```
###### Modifying Configuration

<strong>Local Values</strong>

A local value assigns a name to an expressions, so it can be used multiples times within a configurations without repeating. The expressions in local values are note limited to literals constants, they can also reference other values.

Use local values only in moderation, in situations where a single values or result is used in many places and that value is likely to be changed in future. 

```hcl
locals {
	team = "api_mgmt_dev"
	application = "corp_api"
	server_name = "ec2-${var.environment}-api-${var.variables_sub_az}"
}

locals {
	service_name = local.team
	app_team = "Cloud Team"
	createdby = "terraform"
}

locals {
	common_tags {
		Name = local.server_name
		Owner = local.team
		App = local.application
		Service = loca.service_name
		AppTeam = local.app_team
		CreatedBy = local.createdby
	}
}
```

```hcl
tags = local.common_tags
```

>[!info]
>Common tags are defined so it can be used to assign to all resources. In organizations they may be required for all instances throughout AWS. 

<strong>Input Variables</strong>

```hcl
variable "variables_sub_cidr" {
	description = "CIDR Block for the Variables Subnet"
	type = string
	default = "10.0.202.0/24"
}
```

Set an environment variable to override the default value. to se a value for a particular Terraform variable, create a environment variable called `TF_VAR_<NAME>`

```shell
export TF_VAR_variables_sub_cidr=10.0.203.0/24
```

TF vars file is another way to set the value of the variables in Terraform. It's a special file that Terraform can use to retrieve specific values of variables without requiring the operator to modify the variables file or set environment variables.

```hcl 
# Public Subnet Values
variables_sub_auto_ip = true
variables_sub_az = "us-eas-1d"
variables_sub_cidr = "10.0.204.0/24"
```

>[!note]
>Any value provided on the CLI will override everything, it will override the default, the TF vars file, and including an environment variable.

```shell
terraform plan -var variables_sub_az="us-east-1e"
```

<strong>Terraform output</strong>

`terraform output <output_name>`
`terraform output public_ip`

The last part of this one we can actually wrap this output query to ping this record if we want to.

`ping $(terraform output -raw public_ip)`

suppress the output

```shell
output "ec2_instance_arn" {
	value = aws_instance.web_server.arn
	sensitive = true
}
```

<strong>Variable Validation</strong>

```hcl
variable "cloud" {
	type = string

	validation {
		condition = contains("aws", "azure", "gcp"), lower(var.cloud)
		error_message = "You must use an approved cloud"
	}
}
```

> It will validate the value of a variable based on certain condition or criteria.

To suppress sensitive information:

```hcl
variable "phone_number" { 
	type = string
	sensitive = true
	default = "867-5309"
}
```

>[!note]
>Even if the values are marked as sensitive in the Terraform input and output, it still needs to add the value to the state file. 

<strong>Secure Secrets</strong>

remove the default value and use an environment variable to set it.
add the environment variable in workspace variables on terraform cloud 

using terraform vault

```shell
vault version

# start vault
vaul server -dev

export VAULT_ADDR="http://127.0.0.1:8200"

vault login <root_token>

# add the value to the vault
vault kv put secret/app phone_number=867-5309
```

```hcl
provider "vault" {
	address = "http://127.0.0.1:8200"
	token = <root_token>
}

data "vault_generic_secret" "phone_number" {
	path = "secret/app"
}

output "phone_number" {
	valut = data.vault_generic_secret.data["phone_number"]
}
```

>[!note]
>Never use in the vault provider block the token on a real-world production scenario.

<strong>Collections and Structure Types</strong>

string: a sequence os Unicode characters representing some text, like "hello".

number: a numeric value. The number type can represent both whole numbers like 15 and fractional values like 6.283185.

bool: a boolean value, either true or false, bool values can be used in conditional logic.

list( or tuple): a sequence of values, like `["us-west-1a", "us-weat-1c"]`. Elements in a list or tuple are identifies by consecutive whole numbers, starting with zero. 

```hcl
variable "us-east-1-asz" {
	type = list(string)
	default = [
		"us-east-1a",
		"us-east-1b",
		"us-east-1c",
		"us-east-1d",
		"us-east-1e"
	]
}
# A list will index the strings
```

Tuple is similar to a list and consists of a sequence of elements.The difference between a tuple and a list is that list uses elements of the same variable type, such as string or number.

```hcl
# Tuple
variable "kitty" {
	type = tuple([string, number, bool])
	default = ["cat", 7, true]
}
```

map (or object): a group of values identified by named labels, like `{name="Mabel", age=52}`, Maps are used to store key/value pairs.

```hcl
variable "ip" {
	type = map(string)
	default = [
		prod = "10.0.150.0/24"
		dev = "10.0.250.0/24"
	]
}
```

```hcl
resurce "aws_subnet" "list_subnet" {
	cidr_block = var.ip["prod"]
}
```

Map of maps

```hcl
variable "env" {
	type = map(any)
	default = {
		prod = {
			ip = "10.0.150.0/24"
			az = "us-east-1a"
		}
		dev = {
			ip = "10.0.250.0/24"
			az = "us-east-1e"
		}
	}
}
```

```hcl
resurce "aws_subnet" "list_subnet" {
	for_each = var.env
	vpc_id = aws_vpc.vpc.id
	cidr_block = each.value.ip
	availability_zone = each.value.ip
}
```

Objects allows to create complex data structures by combining all the variable types.

```hcl
variable "bella" {
	type = object ({
    	name = string
        color = string
        age = number
        food = list(string)
        favorite_pet = bool
    })
    
    default = {
    	name = "bella"
    	color = "brown"
        age = 7
        food = ["fish", "chicken", "turkey"]
        favorite_pet = true
    }
}
```


>[!note]
>List/tuples and maps/objects are sometimes called complex types, structural types, or collection types.

<strong>Data Blocks</strong>

Terraform uses data sources to fetch information from cloud provider APIs, such as disk image IDs, or information about the rest of your infrastructure through the outputs of other Terraform configurations.

```hcl
data "aws_s3_bucket" "data_bucket" {
	bucket = "my-data-lookup-bucket-btk"
}
```

<strong>Built-in Function</strong>

Terraform language has many built-in functions that can be used in expressions to transform and combine values.

`max` --> function that takes on or more numbers and return the greatest number from the set.

```shell
max(12, 54, 3)
```

`min` -->  function that takes on or more numbers and return the smallest number form the set.

```shell
min(12, 54, 3)
```

`floor` --> returns the closet whole number that is less than or equal to the given value, which may be a fraction.

```shell
floor(5)
```

`join(sepatator, list)` --> produces a string by concatenating together all elements of a given list of strings with  the given delimiter.

```shell
join(",", ["foo", "bar", "baz"] )
```

`upper`
`lower`

`tolist` --> converts its argument to a list of value.

```shell
tolist(["a", "b", "c"])
```

`cidrsubnet(prefix, newbits, netnum` --> calculates a subnet address within a given IP network address prefix.

```shell
cidrsubnet(var.vpc_cidr, 8, each.value + 100)
```

<strong>Dynamic Blocks</strong>

Are used for nested configurations that are repeatables. Terraform dynamic block allows to dynamically construct repeatable mesteds blcoks using specicl blcok type, which is suupported inside resource, data, provider, and povisioner blocks.

using locals

```hcl
locals {
	ingress_rules [{
		port = 443
		description = "Port 443"
	},
	{
		port = 80
		description = "Port 80"
	}]
}
```

```hcl
resource "aws_security_group" "main" {
	name = "core-sg"
	vpc_id = aws_vpc.vpc_.id

	dynamic "ingress" {
		for_each = local.ingress_rules
		content {
			description = ingress.value.description
			from_port = ingress.value.from_port
			to_port = ingress.value.to_port
			protocol = "tcp"
			cidr_blocks = ["0.0.0.0/0"]
		}
	}
}

```

using variables

```hcl
variable "web_ingress" {
	type = mac(object(
	{
		description = string
		port = number
		protocol = string
		cidr_blocks = list(string)
	}
	))
	default = {
		"80" = {
			description = "Port 80"
			port = 80
			protocol = "tcp"
			cidr_blocks = ["0.0.0.0/0"]
		}
		"443" = {
			description = "Port 443"
			port = 443
			protocol = "tcp"
			cidr_blocks = ["0.0.0.0/0"]
		}
	}
}
```

```hcl
resource "aws_security_group" "main" {
	name = "core-sg"
	vpc_id = aws_vpc.vpc_.id

	dynamic "ingress" {
		for_each = local.web_ingress
		content {
			description = ingress.value.description
			from_port = ingress.value.port
			to_port = ingress.value.port
			protocol = ingress.value.protocol
			cidr_blocks = ingress.value.cidr_blocks
		}
	}
}

```

>[!note]
>Overuse of dynamic block can make configuration hard to read and maintain, so it is recommended to use them only when its needed to hide details in order to build a clean user interface for a re-usable module.

<strong> Terraform Graph</strong>

The `terraform graph` command is used to generate a visual representation of either a configuration or an execution plan. The output is in the DOT format, which highlights the Terraform resource graph.  

The graph is useful for visualizing infrastructure and its dependencies, and it can be pass  it through a graph visualization software such as graphviz.

```shell
terraform grpah | dot - Tsvsg > graph.svg
```

<strong>Resource Lifecycles</strong>

The `lifecycle` block is used in situations where the default lifecycle order that Terraform uses needs to be changed. The `lifecycle` block provide control over dependency erros.

The lifecycle directives are used to influence and ultimately control the order in which Terraform creates and destroys resources.

```hcl
resource "aws_security_group" "main" {
	name = "core-sg-global"
	vpc_id = aws_vpc.vpc_.id

	lyfecycle {
		create_before_destroy = true
		# prevent_destroy = true
	}
}
```
#### Non-Cloud Providers
#### Terraform Cloud

The workstation is where the actual code lives.

Create an organization --> Log into  the account from the workstation --> Create API token

The Terraform Cloud authenticates the user is through a token based authentication.

Defining the remote backend

```hcl
terraform {
	backend "remote" {
		hostname = "app.terrafomr.io"
		organization = "Enterprise-Cloud"
		workspaces {
			name = "my-aws-app"
		}
	}
}
```

Terraform workspace is a managed unit of infrastructure. Workspaces are the workhouse of Terraform Cloud and build on the Terraform CLI workspace construct. Each uses the same Terraform code do deploy infrastructure and each keeps separate data for each workspace. 

In Terraform Cloud the workspace stores state data, has it's own set variables values and environment variables, and allows for remote operations and logging. Terraform Cloud workspaces also provide access controls, version control integration, API access and policy management.


###### Terraform commands

terraform get --> download and update modules

terraform remote --> configure remote state storage
###### Terraform concepts

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

We can also combine the comparison operators like this to make use of a specific version within a range. pessimistic constraint operators --> defined by making use of the tilde greater than symbol --> ~> 1.2 This operator allows TerraForm to download the specific version or any available incremental version based on the value we provided.
 
we can also make use of command line flags. We can pass an as many variables as we want with this method by making use of the dashboard flag multiple times. terraform apply -var "filename=/root/pets.txt" -var "content=We love Pets!"

We can also make use of environment variables with TF_VAR followed by the name of a declared variable. Ex: export TF_VAR_filename="/root/pets.txt"

when we're dealing with a lot of variables, we can load values by making use of variable definition files. These variable definition files can be named anything but should always end in either .tfvars or .tfvars.json. The variable definition file if called .tfvars or .tfvars.json or by any other name ending with *.auto.tfvars or *.auto.tfvars.json will be automatically loaded by TerraForm.

If you use any other file name such as variable.tfvars for example, you will have to pass it along with a command line flag: terraform apply -var-file variables.tfvars

variable definition precedence: -var or -var-file --> *.auto.tfvars --> terraform.fvars --> environment variables

standardized AMIs : using file uploads, using remote exec, automation tools like ansible, chef which is integrated within terraform. puppet gent can be run using remote-exec.

userdata - best wat is to use a template system

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