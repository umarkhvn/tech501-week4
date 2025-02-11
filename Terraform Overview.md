# Terraform Notes
- [Terraform Notes](#terraform-notes)
  - [Overview](#overview)
  - [Setting Up Terraform on Windows](#setting-up-terraform-on-windows)
  - [AWS Access Key Management](#aws-access-key-management)
  - [Infrastructure as Code (IaC)](#infrastructure-as-code-iac)
  - [Terraform: What and Why?](#terraform-what-and-why)
  - [Why Choose Terraform?](#why-choose-terraform)
  - [Alternatives to Terraform](#alternatives-to-terraform)
  - [Understanding Terraform’s Workflow](#understanding-terraforms-workflow)
  - [Key Terraform Commands](#key-terraform-commands)
  - [Orchestration](#orchestration)
  - [Best Practices](#best-practices)


## Overview 

1. **Terraform Installation**
2. **Configured AWS Credentials**
3. **Set Up Project Directory**:
   - Created a folder for the project:  
     `~/OneDrive - Sparta Global/Documents/Github/tech501-terraform/create-ec2-instance`
4. **Executed Terraform Commands** to deploy and remove an EC2 instance (full process documented in [Terraform steps.md](Terraform steps.md)).
5. **Initialized Git Repository**:
   - Commands used:
     - `git init`
     - `git branch -M main`
6. **Created .gitignore**:
   - Included `.terraform/`, `terraform.tfstate`, `terraform.tfstate.backup`
7. **Confirmed Files Were Not Tracked**:
   - Checked status with `git status` and `git add .` to confirm.
8. **Provisioned AWS Security Group**:
   - Updated `main.tf` to reflect changes for EC2 setup.

## Setting Up Terraform on Windows

1. **Download** the Terraform zip file from HashiCorp’s website.
2. **Extract** the zip file.
3. Open **Git Bash** and run `echo $PATH` to check existing PATH directories.
4. **Move** the extracted Terraform folder to one of the PATH directories.
5. **Verify Installation**:
   - Run `terraform -help` to ensure it's properly installed.
6. **Confirm Global Access**:
   - Test running `terraform` commands from any directory in Git Bash.
7. **Verify Version**:
   - Output: `Terraform v1.10.5 on windows_amd64`

## AWS Access Key Management

1. **Open System Properties**:  
   Press `Windows + R`, type `sysdm.cpl`, and press Enter.
2. Navigate to **Advanced** > **Environment Variables**.
3. Under **System variables**, click **New**, and add:
   - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` (values stored securely).
4. **Confirm Setup**:
   - Check credentials in Git Bash to ensure they're accessible.

## Infrastructure as Code (IaC)

- **IaC Definition**: Automating infrastructure setup through code, as opposed to manual GUI interactions.
- **Declarative vs. Imperative IaC**:
  - **Declarative**: Define the desired state (e.g., Terraform handles the "how").
  - **Imperative**: Define exact steps to reach the state (e.g., Ansible).
- **Idempotency**: Re-running scripts ensures the infrastructure matches the desired state, no matter how many times it’s executed.
- **IaC Tools**:
  - **Configuration Management**: Tools like Ansible define infrastructure configurations.
  - **Orchestration**: Terraform is used for managing the lifecycle of infrastructure, ensuring dependencies are respected.

## Terraform: What and Why?

- **Terraform** is an orchestration tool for IaC, enabling the management of the entire infrastructure lifecycle (e.g., creation, modification, destruction of resources).
- Unlike configuration management tools, Terraform treats infrastructure as immutable, requiring recreation for updates.
- Terraform is well-suited for orchestration, while tools like Ansible are primarily for configuration management.

## Why Choose Terraform?

- **Open Source** and free to use.
- Efficient and scalable for managing large infrastructures.

## Alternatives to Terraform

- **Pulumi**: An alternative tool with a different approach to IaC.
- **AWS CloudFormation**: AWS’s native IaC solution.
- **OpenTofu**: A new open-source tool with similar functionalities.

## Understanding Terraform’s Workflow

- Terraform requires credentials for cloud providers, which are standardized across platforms.
- Terraform configurations are stored in `.tf` files, such as:
  - `main.tf` (primary configuration)
  - `variables.tf` (variable definitions)
  - `networking.tf` (network configurations, if applicable)
  - `provider.tf` (cloud provider-specific settings)
- Sensitive files, such as `terraform.tfstate`, should be ignored in Git (`.gitignore`).

## Key Terraform Commands

- `terraform init`: Initializes the working directory and installs required provider plugins.
- `terraform plan`: Previews the changes Terraform will make based on the code.
- `terraform apply`: Applies the changes defined in the plan (can be destructive).
- `terraform destroy`: Destroys all resources created by Terraform.
- `terraform fmt`: Formats `.tf` files according to standard conventions.
- `terraform validate`: Checks for syntax errors in the configuration files.

## Orchestration

- Terraform manages the lifecycle of resources by determining the correct order of creation or deletion.
- If a change is made, Terraform may need to destroy and recreate resources to align with the desired state.

## Best Practices

- **Environment Variables**: A secure and recommended way to supply AWS credentials to Terraform.
- **AWS Credential Lookup Order**:
  1. Environment variables (e.g., `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`).
  2. Terraform variables.
  3. AWS shared credentials file.
  4. IAM role (if Terraform is running on an AWS instance with an attached role).
