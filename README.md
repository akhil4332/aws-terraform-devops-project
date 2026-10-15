# AWS DevOps Project Using Terraform

## Project Overview
This project demonstrates AWS infrastructure provisioning using Terraform and continuous integration using GitHub Actions. The application is hosted on AWS and accessed through an Application Load Balancer.

## Technologies Used
- AWS
- Terraform
- Git and GitHub
- GitHub Actions
- Linux
- EC2 Auto Scaling
- Application Load Balancer
- Amazon RDS (MySQL)
- Amazon S3
- AWS Secrets Manager

## Architecture
The infrastructure includes a VPC with public and private subnets across multiple Availability Zones.

- **Application Load Balancer:** Receives HTTP traffic from users.
- **EC2 Auto Scaling Group:** Runs the application instances in private subnets.
- **Amazon RDS:** Provides a private MySQL database.
- **Amazon S3:** Stores project logs.
- **AWS Secrets Manager:** Stores database credentials.
- **Terraform:** Provisions and manages the infrastructure.
- **GitHub Actions:** Runs Terraform formatting, initialization, and validation checks.
- **OIDC:** Allows GitHub Actions to authenticate to AWS without storing long-lived AWS access keys in GitHub secrets.

## CI/CD Workflow
The GitHub Actions workflow performs:
1. Checkout the repository.
2. Configure AWS credentials through OIDC.
3. Verify the AWS identity.
4. Check Terraform formatting.
5. Initialize Terraform.
6. Validate Terraform configuration.

**Note:** The current workflow validates Terraform configuration but does not automatically run `terraform apply`.

## Deployment
Run the following commands from the `terraform` directory:

```bash
terraform init
terraform fmt -check -recursive
terraform validate
terraform plan
terraform apply
```

Review the execution plan before applying changes.

## Testing
- Open the Application Load Balancer URL in a browser.
- Confirm the demo application page loads.
- Check the latest GitHub Actions run for successful Terraform validation and AWS authentication.

## Security
- Do not commit AWS credentials, private keys, Terraform state files, or secret values.
- Use IAM roles and least-privilege permissions.
- Keep the database in private subnets.
- The demo currently uses HTTP; HTTPS requires appropriate certificate and domain configuration.

## Cleanup
After testing, remove the infrastructure when it is no longer needed:

```bash
terraform destroy
```

Review the resources in the destruction plan before confirming. This removes project resources and may permanently delete the database and other data.

## Project Status
- AWS infrastructure provisioned using Terraform.
- Demo application accessible through an Application Load Balancer.
- GitHub Actions Terraform validation successful.
- AWS OIDC authentication verified.
- Automated infrastructure deployment using `terraform apply` is not configured in the current workflow.
