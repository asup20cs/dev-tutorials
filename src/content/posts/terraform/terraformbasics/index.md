---
title: Terraform Basics
published: 2025-05-15
description: 'Learn the very basic concepts of Terraform'
image: ''
tags: ['terraform']
category: 'tutorials'
draft: false 
lang: 'en'
---
### Terraform Workflow
Write the terraform configuration =====> Plan the infrastructure =====> deploy the infrastructure

### Terraform Initialization
- ```terraform init``` initializes the working directory for terraform

### Terraform Key Concepts
- ```terraform plan``` 
  After initializtion, reads the terraform code and shows the plan of execution / deployment. In this phase, the authentication of credentials takes place
- ```terraform apply```
  Deploys the infrastructure and statements in code
- ```terraform destory```
  Destorys all of the deployed infrastructure and removes the resources
  :::warning
  Non-reversible command. Proceed with caution
  :::

### Stages of Terrform
Write IaC =====> ```terraform init``` =====> ```terraform plan``` =====> ```terraform apply```

### Terraform Providers
- providers are cloud vendors like aws, azure, google cloud etc. to which terrraform interacts to create resources
- terraform providers should always be versioned
  
### Creating a machine using AWS as a provider
#### Project Files and What they do
![project files](src\content\posts\terraform\image1.jpg)
- **main.tf** contains the resource defining code and provider defining code.
```terraform
    terraform {
    required_providers {
      aws = {
        source  = "hashicorp/aws"
        version = "~> 5.0"
      }
    }
  }
  resource "aws_instance" "instance_tf" {
    ami           = "ami-05803413c51f242b7"
    instance_type = "t2.micro"
  }
```
- **provider.tf.example** contains the information needed by the provides, sometimes confidential secrets and passwords. Never share the **providers.tf** file if they contain your secrets. The .example has to be removed to use the file. Terraform will automatically use the **provider.tf** file to get the provider configuration files.
```terraform
provider "aws" {
  access_key = "your aws access key"
  secret_key = "your aws secret key"
  region     = "your aws region"
}
```
Currently, these are the only files you need to get an instance in AWS running.

#### Passing the credentials as environment variables
- from your terminal, export your environmental variables as ```export AWS_ACCESS_KEY = "your key"```
- to check you can use: ```env | grep -i aws``` which shows all the environmental variables starting with aws.
- to pass the environmental variables, no need to specify them when using `terraform plan` or `terraform apply`. Terraform will automatically read the variables from your environment and access them.
  
### Terraform State
- important for resource tracking
- is a way that terraform read to identify what has been deployed
- also seen as a database for terraform
- named as `terraform.tfstate`
- usually stored in same working directory, can also be stored remotely
:::caution
Never loose terraform state file
:::

### Github Repo for the practice files
Find the attached github repo for the files if you need to take a look. Also, some files will be missing as they may contain secrets. Figure them out yourself
::github{repo="asup20cs/terraform-practice"}