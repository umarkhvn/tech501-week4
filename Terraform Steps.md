# Terraform Workflow
- [Terraform Workflow](#terraform-workflow)



1. **Create Repository for Terraform**

2. **Initialize Terraform**  
   Run `terraform init` in the correct directory (i.e., the repository that contains the `main.tf` file).

3. **Format and Plan**  
   - Use `terraform fmt` to standardise the format of the code.  
   - Run `terraform plan` to generate a plan (note that this is not saved yet).

4. **Apply Changes**  
   - Run the destructive command `terraform apply` and confirm by typing `yes` to create all resources.

5. **Success**  
   The result of the above commands will indicate the successful creation of resources.

6. **Destroy Resources**  
   - To destroy all resources, use the destructive command `terraform destroy` and confirm by typing `yes`.
