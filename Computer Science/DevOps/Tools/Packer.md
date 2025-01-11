Packer is a tool to build AMIs. It's a command line tool that can build AWS AMIs based on templates. Instead of installing the software after booting up and instance, you can create an AMI with all the necessary software on. It's a common approach when you ran a horizontally scaled app layer or a cluster of something.
We can use Packer to create golden images across each of these different platforms (vmware, AWS, Docker, Vagrant).

hashicorp packer is a open- source machine image creation tool
helps to automate the installation and configuration on Packer-made images, it works on multiple platforms- even from the same configuration
it eliminates manual steps for golden image creation

Original Machine Image --> packer build --> New Machine Image

primary use cases:
create golden image across platforms and environments
establish an image factory based n new commits for continuous delivery
automate the monthly patching for new/existing workloads 
create immutable infra using packer in CI/CD pipelines

benefits:
version controlled --> images are defined and versioned as code
consistent images--> cross-platform consistency
automate everything --> stop the manual madness 

Workflow

Core components:
templates --> file that is used to  build images
- it can be versioned
- can be built using either JSON (old way) or HCL2
- it defines all the settings using blocks

source --> defines the initial image to use to create a customized image. Any defined source is reusable. within build block.
- Example: building a new AWS Image (AMI), is needed to point to an existing AMI to customize.

builders
variables
provisioners
post-processors
communicators


Command line

