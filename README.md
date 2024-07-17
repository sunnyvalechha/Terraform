Ref-Repository: https://github.com/iam-veeramalla/terraform-zero-to-hero

Terraform is an infrastructure as code (IAC) tool that lets you build, change, and version infrastructure safely and efficiently. This includes low-level components like compute instances, storage, and networking; and high-level components like DNS entries and SaaS features.

Alternatives of Terraform / Competitor of terraform
1. Aws Cloud Formation Template
2. Azure Resource manager
3. Google Cloud Deployment Manager
4. Openstack Heat Templates
5. Crossplane
6. Pulumi
7. Salt

Why Terraform ?
In all the above options we have to only stick to the specific platform but terraform can run on all cloud and any platform. It is not defined only for specific platform. As a DevOps engineer it is difficult to learn different tools just for 1 purpose. Terraform have a universal approach. Terraform can automate infrastruce on any cloud and on-prem enviroment.

Terraform helps us to Hardening the server.

Server hardening is the process of identifying security vulnerabilities in a Linux server and then configuring changes to reduce them also if all the infrastructure details is written in file and use this file as a code that become 'hardened'.

Terraform is using HashiCorp Configuration Language (HCL) an human readable language can be written in json or yaml.

Terraform help us to create highly available infrastructure manually it is difficult to create.

Terraform uses API as code approach meaning if we want to automate the infra on AWS, terraform will talk to the Aws API's and apply this API's and create infrastructure.

4 things we need to understand to Master.

1. Block
2. Arguments
3. Identifiers
4. Comments

**Terraform Block**

* The HCL file contains blocks and arguments
* A block is defined in curly brackets
* Contains a set of arguments in a key:value pair format
* This data is representing the configuration data.

What information block contain - Information of infrastucture of the platform Ex: AWS and the set of resources within that platform that we want to create.

Within the block we can define the resource block and inside the resource block we specify the filename to be created as well its contents.

    resource "local_file" "pet" {
        filename = "/root/pet.txt"
        content = "We love pets!"
    }

![image](https://github.com/sunnyvalechha/Terraform/assets/59471885/ac55a9e8-1204-4de1-9c19-2d470e88be5d)

Here, resource name can be anything

**Types of Blocks in Terraform**

1. Terraform Block
2. Provider Block
3. Data Block
4. Resource Block
5. Module Block
6. Variable Block
7. Output Block
8. Locals Block.

# Setup CodeSpaces

Go to GitHub > Click on Code option from right > Under Codespaces > '+' Icon > Create Codespaces on main > On top search bar '> Add dev container configuration files' > Modify your active configurations > Search for Terraform (Tflint and TFGrunt) > A new file will be add below called devcontainers.

> Add dev container configuration (AWS)

> rebuild - rebuild container > OK

Plugins Installed:
* HashiCorp HCL
* Hashicorp Terraform

Our first code to provision ec2 instance

![image](https://github.com/user-attachments/assets/e7dd2173-708e-49aa-b3b3-2d84d14da7c0)

    terraform init
    terraform fmt
    terraform validate
    terraform plan
    terraform destroy

It initializes a working directory, downloads the necessary provider plugins and modules. The terraform init command performs the following actions: Backend initialization, Child module installation, Plugin installation, Creating a lock file called .terraform.lock.hcl, and Generating a state file new .terraform folder. 

Terraform plan is a command that generates an execution plan that shows the changes that will be made to infrastructure based on the current code configuration. It does this by:
* Reading the current state of any remote objects
* Comparing the current configuration to the previous state
* Noting any differences
* Proposing a set of change actions that should make the remote objects match the configuration
* Presenting a description of the changes necessary to achieve the desired state

Multi-region ec2 instance provision

				terraform {
				required_providers {
					aws = {
						source = "hashicorp/aws"
						version = "~> 5.0.0"
					}
				}
				}
				provider "aws" {
				alias  = "us-east-1"
				region = "us-east-1"
				}
				provider "aws" {
				alias  = "us-west-1"
				region = "us-west-1"
				}
				resource "aws_instance" "example" {
				ami           = "ami-0b72821e2f351e396"
				key_name      = "my-key"
				instance_type = "t2.micro"
				provider      = aws.us-east-1
				}
				resource "aws_instance" "example-2" {
				ami           = "ami-0fb83b36371e7dab5"
				key_name      = "my-key-test"
				instance_type = "t2.micro"
				provider      = aws.us-west-1
				
				}

Subcommands run with terraform:

    list                List resources in the state
    mv                  Move an item in the state
    pull                Pull current state and output to stdout
    push                Update remote state from a local state file
    replace-provider    Replace provider in the state
    rm                  Remove instances from the state
    show                Show a resource in the state


# Providers

Providers are plugins that helps terraform that where it has to create infrastructure, without provider it is not possible to create infra.

Providers are categorized into 3 parts:
* Official Providers - These providers which Hashicorp actively maintains (Aws. Azure, Google, Kubernetes).
* Partner Providers - Partners are only maintains the documentation, how anybody can create infra through terraform. (Alibaba cloud and Oracle cloud)
* Community Providers - We also can provide the entire provider configuration and opensource will maintain these providers. There is no official backing up by Hashicorp and Partner provider on this.


**Multiple Providers** - We can setup multi region infra setup on terraform.

Use keyword 'alias' to implement multi region infra setup on terraform.

    provider "aws" {
      alias = "us-east-1"
      region = "us-east-1"
    }

    provider "aws" {
      alias = "us-east-2"
      region = "us-east-2"
    }

    resource "aws_instance" "example" {
      ami = "ami-058bd2d568351da34"
      instance_type = "t2.micro"
      provider = "aws.us-east-1"
    }

    resource "aws_instance" "example2" {
      ami = "ami-058bd2d568351da34"
      instance_type = "t2.micro"
      provider = "aws.us-east-2"
    }


Note: 
* At the time of command "terraform init" notification appear that no config file found than check your location, create a folder, create a .tf file than go inside a folder than run commnand.

* Every region has different ami id of same image of Os. Example us-east-1 Suse Linux has different Ami Id than us-east-2. So you have to change in script also.


You can use multiple providers in one single terraform project. For example,

* Create a providers.tf file in the root directory of your Terraform project.
* In the providers.tf file, define the AWS and Azure providers. For example:

        provider "aws" {
      region = "us-east-1"
    }

        provider "azurerm" {
      subscription_id = "your-azure-subscription-id"
      client_id = "your-azure-client-id"
      client_secret = "your-azure-client-secret"
      tenant_id = "your-azure-tenant-id"
    }

In your other Terraform configuration files, you can then use the aws and azurerm providers to create resources in AWS and Azure, respectively

    resource "aws_instance" "example" {
      ami = "ami-0123456789abcdef0"
      instance_type = "t2.micro"
    }

    resource "azurerm_virtual_machine" "example" {
      name = "example-vm"
      location = "eastus"
      size = "Standard_A1"
    }



# Variables

Use of Variable in terra: Generally we write a hcl file and put the value of Ami and Instance as it is but this is not a good practise instead of hard coded the value we should make variable because as a DevOps person we might have support to different teams and might couple of times we receive a request to do a same kind of work for different teams so Variable would be very useful here.

In Terraform two types of variable are there.

1. Input Variable
2. Output Variable

Input and output variables in Terraform are essential for parameterizing and sharing values within your Terraform configurations and modules. They allow you to make your configurations more dynamic, reusable, and flexible.

Input: Suppose we want to pass some informaton to terraform then it is a input variable.
Output: If we want terraform to print a particular value in the output called as Output variable.

    variable "example_var" {
      description = "An example input variable"
      type        = string
      default     = "default_value"
    }

    
* variable > is used to declare an input variable named example_var.
* description > provides a human-readable description of the variable.
* type > specifies the data type of the variable (e.g., string, number, list, map, etc.).
* default > provides a default value for the variable, which is optional.


# Modules 

# Terraform Commands:
    terraform init
    terraform plan
    terraform apply
    terraform validate     #check for errors
    terraform plan -out=/root/plan.txt
    terraform --help
    terraform providers --help
    
All other commands:

    console       # Try Terraform expressions at an interactive command prompt
    fmt           # Reformat your configuration in the standard style
    force-unlock  # Release a stuck lock on the current workspace
    get           # Install or upgrade remote Terraform modules
    graph         # Generate a Graphviz graph of the steps in an operation
    import        # Associate existing infrastructure with a Terraform resource
    login         # Obtain and save credentials for a remote host
    logout        # Remove locally-stored credentials for a remote host
    metadata      # Metadata related commands
    output        # Show output values from your root module
    providers     # Show the providers required for this configuration
    refresh       # Update the state to match remote systems
    show          # Show the current state or a saved plan
    state         # Advanced state management
    taint         # Mark a resource instance as not fully functional
    test          # Experimental support for module integration testing
    untaint       # Remove the 'tainted' state from a resource instance
    version       # Show the current Terraform version
    workspace     # Workspace management


# Mutable and Immutable infrastructure


# Lifecycle rules

* create_before_destroy
* prevent_destory
* ignore_changes


# Datasources in terraform

# Meta Arguments

# Version Constraints

Terraform lets you specify a range of acceptable versions for something, it expects a specially formatted string known as a version constraint.

While running 'terraform init' the latest version of plugins are downloaded that are required by the configuration but this is not desired everytime, we might need older plugins becuase the code written in older plugin version. 

    terraform {
        required_providers {
            local = {
                source = "hashicorp/local"
                version = "1.4.0"
            }
        }
    }

    resource "local_file" "my_pet" {
        filename = "/root/pet.txt"
        content = "Pet loved by all"
    } 

* In above version feild we can mention the version required or not required

      version = "! = 2.0.0"  # do not use this version.
      version = "< 1.4.0"    # use version lesser than this version.
      version = "> 1.4.0"    # use version greater than this version.
      version = "> 1.2.0, < 2.0.0, ! 1.4.0" # greater, lesser, not required.
      version = "~> 1.2"    
      


# Terraform with AWS 

    resource "aws_iam_user" "users" {
      name = "mary"
    }

    provider "aws" {
        region = "ca-central-1"
    }

    cat /root/.aws/credentials
    [default]
    aws_access_key_id = foo
    aws_secret_access_key = bar

    resource "aws_iam_user" "users" {
      name = var.project-sapphire-users[count.index]
      count = length(var.project-sapphire-users)
    }












# EKS Cluster through Terraform

Install AWS CLI

    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip
    sudo ./aws/install

Install Terraform

    sudo yum install -y yum-utils
    sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
    sudo yum -y install terraform

Setup Aws configure

Git clone repository: https://github.com/sunnyvalechha/terraform-eks.git

    mkdir eks-terraform
    cd eks-terraform/
    yum install git -y
    git clone https://github.com/sunnyvalechha/terraform-eks.git
    ls -lrth
    cd terraform-eks/
    ls -lrth
    git remote -v
    git status

    terraform init 

    terraform plan

    terraform apply --auto-approve


# Terraform Workspaces

* Terraform starts with a single workspace called "default" and this "default" workspace cannot deleted.

* By default we always works on "default" workspace.

* Use case is, some changes we need to test but we cannot implement directly on Production so we can create a workspace and test there just like git branch.

* Terraform CLI workspaces are completely different from Terraform cloud workspaces.

* In any workspace we work it will create their personal "terraform.tfstate" file

Commands:-

1. terraform workspace show	    # Show current workspace
2. terraform workspace list	    # List all workspace
3. terraform workspace new		# Create new
4. terraform workspace select	# Switch between workspaces
5. terraform workspace delete	


Note: We will assign workspace name as:-

name = "vpc-ssh-${terraform.workspace}"

