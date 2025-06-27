Ref-Repository: https://github.com/iam-veeramalla/terraform-zero-to-hero

**Terraform** is an infrastructure as code (IAC) tool that lets you build, change, and version infrastructure safely and efficiently. This includes low-level components like compute instances, storage, and networking, and high-level components like DNS entries and SaaS features.

**Alternatives to Terraform / Competitors of Terraform**
1. AWS CloudFormation Template
2. Azure Resource Manager
3. Google Cloud Deployment Manager
4. OpenStack Heat Templates
5. Crossplane
6. Pulumi
7. Salt

**Why Terraform?**

In all the above options, we have to stick only to the specific platform, but Terraform can run on all clouds and any platform. It is not defined only for a specific platform. As a DevOps engineer, it is difficult to learn different tools just for 1 purpose. Terraform has a universal approach. Terraform can automate infrastructure on any cloud and on-prem environment.

Terraform helps us to harden the server.

**Server hardening** is the process of identifying security vulnerabilities in a Linux server and then making changes to reduce them. Also, if all the infrastructure details are written in a file and used this file as a code that becomes 'hardened'.

Terraform uses HashiCorp Configuration Language (HCL), a human-readable language that can be written in JSON or YAML.

Terraform helps us create highly available infrastructure. It is difficult to create.

Terraform uses an API as a code approach, meaning if we want to automate the infrastructure on AWS, Terraform will talk to the AWS API's and apply these API's and create infrastructure.

**VScode plugin for Terraform:** Hashicorp Terraform (Syntax highlighting and autocompletion for Terraform)

**AWS Cli:** https://awscli.amazonaws.com/AWSCLIV2.msi

**Terraform download on Windows**: https://developer.hashicorp.com/terraform/install

* Extract files once downloaded > Copy the terraform.exe file > Create a folder in the C drive (terraform-bins) > Paste the terraform.exe file > Copy folder location (C:\terraform-bins)
* Search for "Environment variables" > Click on "Environment variables" > Click on "Path" > Edit > New > Paste the location path (C:\terraform-bins) > OK > OK
* Open cmd prompt > Run "terraform version"
* Must get the version number
* Same time verify the AWS Cli also

![image](https://github.com/user-attachments/assets/c2b0c7e5-50df-477a-b91f-1515f41afa7d)

![image](https://github.com/user-attachments/assets/663c95d0-f0bc-4c76-aff7-fc4a4057d924)

**VScode**: Restart VScode after following the above process, then check for the terraform version. Also, you might need to run the code in the folder (C:\terraform-bins)

![image](https://github.com/user-attachments/assets/fbec6dcf-c09a-4328-af26-0b2577d4e0db)

**An alternate playground to run the Terraform is GitHub Codespaces**

**Setup CodeSpaces**:

Go to GitHub > Click on Code option from right > Under Codespaces > '+' Icon > Create Codespaces on main > On top search bar write "**> Add**" It give option like "Add dev container configuration files" > Modify your active configurations > Search for Terraform (Tflint and TFGrunt) > A new file will be add below called devcontainers > but terraform still not installed > **Same step do for AWS.** '> Add dev container configuration files' > rebuild > rebuild container > OK 

![image](https://github.com/user-attachments/assets/e2b9a1b8-3751-4b35-a661-90b75a83b9d3)

![image](https://github.com/user-attachments/assets/eefde59e-e85a-4b52-a5d5-f4e8cc94a5d7)

![image](https://github.com/user-attachments/assets/6b6ecc74-7a37-4b43-b7a3-64309ffdd38b)

![image](https://github.com/user-attachments/assets/66f06163-5a6e-40ca-8476-98cca9940c6f)


**4 things we need to understand to Master Terraform**.

1. Block
2. Arguments
3. Identifiers
4. Comments

**Terraform Block**

* The HCL file contains blocks and arguments
* A block is defined in curly brackets
* Contains a set of arguments in a key-value pair format
* This data represents the configuration data.

What information block contains - Information of the infrastructure of the platform, like AWS, and the set of resources within that platform that we want to create.

**Arguments** are resource-specific. It is either optional or required. Terraform will give an error if the required argument is missing.

**Attributes** are values exposed by a particular resource. A resource's attributes are assigned to it by the underlying cloud provider or API

**Meta-arguments** Terraform-specific arguments 

Within the block, we can define the resource block, and inside the resource block, we specify the filename to be created as well as its contents.

    resource "local_file" "pet" {
        filename = "/root/pet.txt"
        content = "We love pets!"
    }

![image](https://github.com/sunnyvalechha/Terraform/assets/59471885/ac55a9e8-1204-4de1-9c19-2d470e88be5d)

Here, the resource name can be anything

**Types of Blocks in Terraform / Top-level blocks**

1. Terraform Block
2. Provider Block
3. Data Block
4. Resource Block
5. Module Block
6. Variable Block
7. Output Block
8. Locals Block.

All are the same - Terraform block / Terraform Setting block / Terraform configuration block 




**Practical:**

    provider "aws" {
    region = "us-east-1" 
  
    }
    resource "aws_instance" "example" {
    ami = "ami-0cd59ecaf368e5ccf"
    instance_type = "t2.micro"
    }

    
**terraform init**

It initializes a working directory, downloads the necessary provider plugins and modules, and sets up the backend for storing the infrastructure's state. The terraform init command performs the following actions: Backend initialization, Child module installation, Plugin installation, creating a lock file called .terraform.lock.hcl, and generating a new .terraform folder. 

**terraform plan**

Terraform plan is a command that generates an execution plan that shows the changes that will be made to the infrastructure based on the current code configuration. It does this by:
* Reading the current state of any remote objects
* Comparing the current configuration to the previous state
* Noting any differences
* Proposing a set of change actions that should make the remote objects match the configuration
* Presenting a description of the changes necessary to achieve the desired state

**terraform apply**

  Apply the actual changes in infrastructure.

**terraform destroy**

  Delete all configurations created through Terraform

**Subcommands run with terraform:**

    list                List resources in the state
    mv                  Move an item in the state
    pull                Pull current state and output to stdout
    push                Update remote state from a local state file
    replace-provider    Replace provider in the state
    rm                  Remove instances from the state
    show                Show a resource in the state


# Providers

Providers are plugins that help terraform that where it has to create infrastructure, without provider it is not possible to create infra.

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
      provider = "aws.us-east-1"        # aws.<alias>    
    }

    resource "aws_instance" "example2" {
      ami = "ami-058bd2d568351da34"
      instance_type = "t2.micro"
      provider = "aws.us-east-2"        # aws.<alias>
    }

* This alias can be anything like ABC, XYZ, it will read the value from the region only

Note: 
* At the time of command "terraform init", a notification appears that no config file is found, then check your location, create a folder, create a .tf file than go inside a folder than run commnand.

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

In Terraform two types of variables are there.

1. Input Variable
2. Output Variable

Input and output variables in Terraform are essential for parameterizing and sharing values within your Terraform configurations and modules. Variables allow you to make your configurations more dynamic, reusable, and flexible.

Input: Suppose we want to pass some information to Terraform, then it is an input variable.
Output: If we want Terraform to print a particular value in the output called Output variable.

    variable "example_var" {
      description = "An example input variable"
      type        = string
      default     = "default_value"
    }
    
* variable > is used to declare an input variable named example_var.
* description > provides a human-readable description of the variable.
* type > specifies the data type of the variable (e.g., string, number, list, map, etc.).
* default > provides a default value for the variable, which is optional.

Example: A folder created a Variable inside its main.tf and variable.tf created 

![image](https://github.com/user-attachments/assets/235bf903-6111-419d-a96f-371e035e2a36)

![image](https://github.com/user-attachments/assets/ea4a6823-a436-4bf3-896f-d0074c40b233)

**Variables - Assign when Prompted**

Note: We did not specify a default value in Variable.tf so when we run the plan or apply command a prompt will appear to provide value. Main.tf is the same, no modifications.

![image](https://github.com/user-attachments/assets/ce5cabfa-b91e-4369-a7e6-527dcf0973db)

![image](https://github.com/user-attachments/assets/6d3fca0a-1eab-47db-b894-3baa16b99529)


**Variable - Terraform.tfvars**

If the file name is terraform.tfvars, terraform will auto-load the variables present in this file by overriding the default value in variables.tf, even if we do not specify the variable value, the values are taken from tfvars automatically.

Error in the below snap, correct

![image](https://github.com/user-attachments/assets/3384fd1d-95da-4eb7-908d-fcccd6d716d4)

**Some more recent snaps**

![image](https://github.com/user-attachments/assets/ae5b5adb-6a2e-44db-a16b-ff614cedd81e)

![image](https://github.com/user-attachments/assets/d5060645-7bca-4f76-8771-e5b80989593f)

Then, we have created a separate file to assign the variables. (to get the value of the variables)

![Uploading image.png…]()



**Output Variables - Pending**

**Conditional expressions**

* Conditional expression in Terraform are used to define conditional logic within your configurations. They allow you to make decisions or set values based on conditions.
* Conditional expressions are typically used to control whether resources are created or configured based on the evaluation of a condition.

Syntax: condition ? true_val : false_val

* condition: expression that evaluates to either true or false.
* true_val: value that is returned if the condition is true.
* false_val: value that is returned if the condition is false

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

Terraform lets you specify a range of acceptable versions for something; it expects a specially formatted string known as a version constraint.

While running 'terraform init' the latest version of plugins are downloaded that are required by the configuration, but this is not desired every time, we might need older plugins becuase the code written in older plugin version. 

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

* In the above version field we can mention the version required or not required

      version = "! = 2.0.0"  # do not use this version.
      version = "< 1.4.0"    # use a version less than this version.
      version = "> 1.4.0"    # use version greater than this version.
      version = "> 1.2.0, < 2.0.0, ! 1.4.0" # greater, lesser, not required.
      version = "~> 1.2"      # Any stable version greater than 1.2.*. So here "*" will be modified

Note: When using the "~>" sign, ensure that you specify the minor version; otherwise, it will upgrade to the major version, as shown above. For example, 1.2. "2" is the major version, and 1.2.11. "11" is the minor version. We always wanted it to automatically use the latest minor version, not the major version.


      


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

