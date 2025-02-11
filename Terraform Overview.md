# Terraform Notes

- [Terraform Notes](#terraform-notes)
  - [Overview of Task](#overview-of-task)
  - [Installing Terraform on Windows](#installing-terraform-on-windows)
  - [Storing AWS Access Keys as Environment Variables](#storing-aws-access-keys-as-environment-variables)
  - [Infrastructure as Code (IaC)](#infrastructure-as-code-iac)
  - [What is Terraform?](#what-is-terraform)
  - [Why Use Terraform? Benefits](#why-use-terraform-benefits)
  - [Alternatives to Terraform](#alternatives-to-terraform)
  - [How Does Terraform Work?](#how-does-terraform-work)
  - [Terraform Code Commands](#terraform-code-commands)
  - [Orchestration in IaC: How Terraform Acts as an Orchestrator](#orchestration-in-iac-how-terraform-acts-as-an-orchestrator)
  - [Best Practices for Supplying AWS Credentials to Terraform](#best-practices-for-supplying-aws-credentials-to-terraform)

## Overview of Task

1. Installed Terraform
2. Added AWS Access Key ID and Secret Key to System Environment Variables
3. Created a folder for this project:
   - `~/OneDrive - Sparta Global/Documents/Github/tech501-terraform/create-ec2-instance`
4. Ran Terraform commands to create and destroy an EC2 instance (see [Terraform steps.md](Terraform steps.md))
5. Initialized this folder as a Git repository:
   - `git init`
   - `git branch -M main`
6. Created a `.gitignore` file in the repo with the following entries:
   - `.terraform/`
   - `terraform.tfstate`
   - `terraform.tfstate.backup`
7. Ran `git status` to ensure the files weren't being tracked, then ran `git add .` and checked with `git status`
8. Created an AWS security group using Terraform and updated the `main.tf` file for the EC2 instance

## Installing Terraform on Windows

1. Download the Terraform zip folder from the HashiCorp site
2. Unzip the folder
3. Run `echo $PATH` to check where PATH folders are located
4. Move the unzipped folder from Downloads to one of these PATH folders
5. Verify the installation by running `terraform -help`
6. Ensure that we can run Terraform commands from anywhere in Git Bash
7. Output of `terraform --version`:
   - `Terraform v1.10.5 on windows_amd64`

## Storing AWS Access Keys as Environment Variables

1. Press `Windows key + R`
2. Run `sysdm.cpl`
3. Navigate to the **Advanced** tab > **Environment Variables**
4. Under **System variables**, click **New**, and add the following:
   - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` with values stored securely in a .csv file
5. Click OK
6. In Git Bash, run the appropriate command to set environment variables

## Infrastructure as Code (IaC)

- **IaC**: Provisioning infrastructure via code, not GUIs
- **Declarative IaC**: Users define the desired end state, and the tool handles how to achieve it (e.g., Terraform)
- **Imperative IaC**: Users specify the exact steps taken (e.g., Ansible)
- **Idempotent**: Running the script multiple times does not change the result if the desired state is already achieved
- **Dependencies**: Infrastructure has dependencies, and some resources need to be created before others
- **IaC Tools**:
  - Configuration management tool: e.g., Ansible
  - Orchestration tool: e.g., Terraform
- **Configuration Drift**: Occurs when systems deviate from the desired configuration over time, e.g., in a load-balanced server environment

## What is Terraform?

- Terraform is an IaC tool used to orchestrate and manage the lifecycle of resources in infrastructure.
- It uses HashiCorp Configuration Language (HCL).
- Terraform views infrastructure as immutable, meaning it will destroy and rebuild resources if changes are needed, as opposed to configuration management tools like Ansible, which modify existing infrastructure.

## Why Use Terraform? Benefits

- Open-source
- Efficient and scalable

## Alternatives to Terraform

- Pulumi
- AWS CloudFormation
- OpenTofu

## How Does Terraform Work?

- Terraform requires credentials for your cloud provider (the naming conventions are consistent across providers).
- Terraform code is stored in `.tf` files, such as:
  - `main.tf`
  - `variables.tf`
  - Additional files may include `networking.tf` or `provider.tf`
  - `.terraform.lock.hcl` can be shared within teams to lock plugin versions
- Files like `terraform.tfstate` must be git-ignored because they contain sensitive information.
- Terraform will look at all files ending in `.tf`.

## Terraform Code Commands

- `terraform init`: Initializes Terraform in a folder and downloads the necessary provider plugins.
- `terraform plan`: Generates a plan to bring the infrastructure to the desired state (can be saved).
- `terraform apply`: Destructive command; applies the plan and provisions the resources.
- `terraform destroy`: Destructive command; destroys the resources managed by Terraform.
- `terraform fmt`: Standardizes the format of `.tf` files.
- `terraform validate`: Validates the syntax of Terraform code.

## Orchestration in IaC: How Terraform Acts as an Orchestrator

- As an orchestration tool, Terraform determines the order in which resources should be created or deleted.
- It ensures the entire lifecycle of resources is managed, often requiring the destruction and recreation of resources to maintain consistency.

## Best Practices for Supplying AWS Credentials to Terraform

- Use environment variables to store credentials securely.
- Terraform can look up AWS credentials in the following order:
  - Environment variables (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`)
  - Terraform variables
  - AWS shared credentials file
  - IAM role (if applicable)
