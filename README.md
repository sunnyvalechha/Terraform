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

Terraform help us to create highly available infrastructure manually it is difficult to create manually.

Terraform uses API as code approach meaning if we want to automate the infra on AWS, terraform will talk to the Aws API's and apply this API's and create infrastructure.

Setup CodeSpaces:

Go to GitHub > Click on Code option from right > Under Codespaces > '+' Icon > Create Codespaces on main > On top search bar '> Add dev container configuration files' > Modify your active configurations > Search for Terraform (Tflint and TFGrunt) > A new file will be add below called devcontainers > but terraform still not installed > Same step do with AWS. 

'> Add dev container configuration files' > rebuild > rebuild container > OK 



Practical:

    provider "aws" {
    region = "us-east-1" 
  
    }
    resource "aws_instance" "example" {
    ami = "ami-0cd59ecaf368e5ccf"
    instance_type = "t2.micro"
    }



    terraform init

It initializes a working directory, downloads the necessary provider plugins and modules, and sets up the backend for storing infrastructure's state. The terraform init command performs the following actions: Backend initialization, Child module installation, Plugin installation, Creating a lock file called .terraform.lock.hcl, and Generating a new .terraform folder. 

    terraform plan

Terraform plan is a command that generates an execution plan that shows the changes that will be made to infrastructure based on the current code configuration. It does this by:
* Reading the current state of any remote objects
* Comparing the current configuration to the previous state
* Noting any differences
* Proposing a set of change actions that should make the remote objects match the configuration
* Presenting a description of the changes necessary to achieve the desired state


      terraform apply

  Apply make the actual changes in infrastructure.

      terraform destroy

  Delete all configuration created through terraform


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

* Every region has different ami id of same image os Os. Example us-east-1 Suse Linux has different Ami Id than us-east-2. So you have to change in script also.
