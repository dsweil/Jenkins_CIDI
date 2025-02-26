```markdown
# Jenkins CI/CD Infrastructure Setup

## Overview
This repository provides a Terraform-based infrastructure setup for a Jenkins-driven CI/CD environment on AWS. It provisions a five-server architecture to support continuous integration, deployment, and security workflows. Key integrated tools include:

- **Jenkins**: Central CI/CD orchestration.
- **Grafana**: Performance monitoring and visualization.
- **HashiCorp Vault**: Secrets management.
- **OWASP ZAP & Dastardly**: Dynamic application security testing (DAST).
- **SonarQube & Snyk**: Code quality and dependency security (post-deployment configuration required).

*Note*: This project focuses solely on the infrastructure layer. Comprehensive configuration details (e.g., Jenkins pipelines, tool integrations) are extensive and available upon request.

## Prerequisites
- **AWS Account**: With permissions for EC2, VPC, and security group management.
- **Terraform**: v1.5.0 or later installed locally.
- **AWS CLI**: Configured with credentials (`aws configure`).
- **Git**: For cloning the repository.

## Setup Steps for AWS
1. **Clone the Repository**
   ```bash
   git clone https://github.com/dsweil/Jenkins_CIDI.git
   cd Jenkins_CIDI
   ```

2. **Configure AWS Credentials**
   - Set up AWS CLI with an IAM user/role having necessary permissions.
   - Or export credentials as environment variables:
     ```bash
     export AWS_ACCESS_KEY_ID="your-access-key"
     export AWS_SECRET_ACCESS_KEY="your-secret-key"
     export AWS_DEFAULT_REGION="us-east-1"  # Adjust region as needed
     ```

3. **Initialize Terraform**
   ```bash
   terraform init
   ```

4. **Plan the Deployment**
   - Preview the infrastructure:
     ```bash
     terraform plan -out=tfplan
     ```

5. **Deploy to AWS**
   - Apply the saved plan to provision resources:
     ```bash
     terraform apply tfplan
     ```

6. **Verify Deployment**
   - Check `outputs.tf` for server IPs or DNS names post-deployment.
   - Access Jenkins (port 8080) or SSH into instances for further setup.

7. **Cleanup (Optional)**
   - Destroy the infrastructure when done:
     ```bash
     terraform destroy
     ```
   - Confirm with `yes`.

## Project Structure
```
.
├── Jenkinfile          # Sample Jenkins pipeline configuration
├── main.tf             # Core Terraform configuration (AWS provider, VPC, etc.)
├── outputs.tf          # Outputs (e.g., server IPs, DNS names)
├── scripts/            # Provisioning scripts for server setup
│   ├── dastardly.sh    # Dastardly security tool setup
│   ├── jenkins.sh      # Jenkins server configuration
│   ├── monitoring.sh   # Grafana monitoring setup
│   ├── vault.sh        # Vault server initialization
│   └── zap.sh          # OWASP ZAP configuration
├── security-groups.tf  # Security group definitions
└── servers.tf          # EC2 instance configurations
```

## Infrastructure Details
- **5 EC2 Instances**: 
  - Jenkins master (configured via `jenkins.sh`).
  - Grafana monitoring (via `monitoring.sh`).
  - Vault server (via `vault.sh`).
  - ZAP server (via `zap.sh`).
  - Dastardly server (via `dastardly.sh`).
- **Networking**: VPC and security groups defined in `security-groups.tf`.
- **Scripts**: Bash scripts in `scripts/` handle initial server provisioning.

## Next Steps
- Use the `Jenkinfile` as a starting point to build pipelines integrating SonarQube, Snyk, and ZAP.
- Configure Grafana dashboards for pipeline and server metrics.
- Request the full setup guide, including tool configurations and pipeline examples, by contacting [your-email@example.com].

## Contributing
Fork this repo, report issues, or submit pull requests to improve the setup.

## License
[Specify your license, e.g., MIT, Apache 2.0]
```
