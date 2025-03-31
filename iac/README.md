# Infrastructure as Code (IaC) Repository

This repository contains Terraform configurations for provisioning and managing cloud infrastructure across development, staging, and production environments.

## Repository Structure

### /dev-terraform
Contains all Terraform configurations for the development environment:
- **networking/**: Network resources like VPCs, subnets, Transit Gateways
  - **eks/**: Development-specific network configurations for EKS
  - **modules/**: Development-specific network modules
- **workload/**: EKS clusters, node groups, and application resources
  - **eks/**: Development EKS clusters (using smaller instance types like t3.medium)
- **operation/**: CI/CD tools like Jenkins
- **observability/**: Monitoring tools (Grafana, Prometheus)
- **data/**: Database resources, Kafka, and other storage solutions

### /stage-terraform
Contains all Terraform configurations for the staging environment:
- Similar structure to development but with production-like configurations
- Larger instance types (e.g., m5.large)
- More resilient setups than development

### /prod-terraform
Contains all Terraform configurations for the production environment:
- **networking/prod/**: Production network resources
- **workload/prod/**: Production EKS clusters (HA setup with larger instances)
- **operation/prod/**: Production CI/CD tools
- **observability/prod/**: Production monitoring stack
- **data/prod/**: Production data resources

## Usage

1. Each environment has its own state files
2. Use backend configurations appropriate for each environment
3. Apply changes through CI/CD pipelines after review
4. Validate all changes in lower environments before production

## Best Practices

1. Use modules for reusable infrastructure components
2. Keep sensitive data in secure parameter stores, not in the repository
3. Use remote state storage with locking
4. Apply infrastructure changes through pull requests
5. Leverage terragrunt for DRY configurations across environments
6. Document all infrastructure components and their relationships 