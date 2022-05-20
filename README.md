# Terraform - Automate your AWS cloud infrastructure

Github: https://github.com/Sanjeev-Thiyagarajan/Terraform-Crash-Course  

# AWS Setup:
Go to https://aws.amazon.com/  and create an aws account following the instructions.  

# Install Terraform on Windows Machine:
1. Download terraform file.  
2. Unzip it.  
3. Add the terraform.exe file location path in user level environment variable.  
4. Type $terraform -version to check if terraform is installed properly or not.  

# Visual Studio Code setup:
Download VScode from https://code.visualstudio.com/ 

# Terraform Overview:
 
Language: hashicorp configuration language.   
File extension: .tf  
AWS Provider: https://registry.terraform.io/providers/hashicorp/aws/latest/docs   
Region: means where AWS data center is, check your region from your AWS management console.  

Configure the AWS Provider  
provider "aws" {  
  region = "us-west-1"  
  access_key = ""  
  secret_key = ""  
}


How to deploy an EC2 instance within AWS?  
EC2 is just a virtual machine within AWS (you can deploy windows, linx, database etc within AWS)  
Purpose of deploying EC2 - EC2 is a service that enables business subscribers to run application programs in the computing environment.  (https://www.techtarget.com/searchaws/definition/Amazon-EC2-instances )  
There are two ways- you can do it from AWS console or from terraform.  
 From AWS console- Go to EC2 instance- launch instance  
 From terraform   
- declare resource  
- execute command - [terraform init, terraform plan, terraform apply]  
     - 	Modify resources [ add tags if you want to put name of your instance]  
     - 	Destroy resources [$terraform destroy]  
     -   	Reference resources [when you create a subnet under a vpc you can reference that vpc using vpc id like: vpc_id     = aws_vpc.first-vpc.id]  


resource "aws_instance" "first-server" {  
  ami           = "ami-01fd3b69ad00fd21c"  
  instance_type = "t2.micro"  
 
  tags = {  
    Name = "ubuntu server"  
  }  


Terraform Plan:
The $terraform plan command creates an execution plan, which lets you preview the changes that Terraform plans to make to your infrastructure.

Terraform Apply:
The $terraform apply command executes the actions proposed in a Terraform plan to create, update, or destroy infrastructure.

AWS VPC:
Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network that you've defined.

resource "aws_vpc" "first-vpc" {  
  cidr_block       = "10.0.0.0/16"  
 
  tags = {  
    Name = "production"   
  }  
}  


Terraform files:  
.terraform=> terraform init create this, it installs all plugins necessary for the code to run.  
terraform.tfstate=> whenever we create any resource terraform stores that in this state file.  


# Project Step:
1.Create vpc.  
2.Create internet gateway.  
3.Create custom route table.  
4.Create a subnet.  
5.Associate subnet with route table.  
6.Create security group to allow port 22,88,443.  
7.Create a network interface with an IP in the subnet that was created in step 4.  
8.Assign an elastic IP to the network interface created in step 7.  
9.Create ubuntu server and install/enable apache2.  

Terraform state commands:  

$terraform state list => output will be all states you created.  
$terraform state show (put name of a state) => will provide details of any particular state.  

If you want to destroy one particular resource=> $terraform destroy -target (resource name).  
If you want to deploy one particular resource=> $terraform apply -target (resource name).  

Terraform Variable:  
1.If you don't assign value of a variable, after running terraform apply it will ask for value.  
2.You can assign value of a variable through command line: $terraform apply -var “value”.  
3.You can assign value of a variable by creating a separate file named terraform.tfvars.  
4.You can change name of .tfvars file by mentioning it through command line.  







