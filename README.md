# Infrastructure Repository

This repository contains the infrastructure code for our cloud-native platform across multiple environments (dev, stage, prod) using a GitOps approach.

## Repository Structure

This repository is organized into two main components:

### /iac (Infrastructure as Code)
Contains Terraform configurations to provision and manage cloud infrastructure:
- **dev-terraform/**: Development environment infrastructure
- **stage-terraform/**: Staging environment infrastructure
- **prod-terraform/**: Production environment infrastructure

Each environment is further divided into specialized components:
- **networking/**: Network infrastructure (VPCs, subnets, Transit Gateways)
- **workload/**: EKS clusters and application infrastructure
- **operation/**: CI/CD and operational tools
- **observability/**: Monitoring and observability stack
- **data/**: Database and data processing infrastructure

[See IAC README](/iac/README.md) for more details.

### /gitops
Contains Kubernetes manifest files managed through GitOps principles:
- **base/**: Shared configurations and resources
- **clusters/**: Cluster-specific configurations by environment and account
- **applications/**: Business application manifests with environment overlays

[See GitOps README](/gitops/README.md) for more details.

## Workflow

1. Infrastructure changes:
   - Make changes to Terraform code in the appropriate environment directory
   - Create a pull request for review
   - Approved changes are applied through CI/CD pipelines

2. Application deployment:
   - Update Kubernetes manifests in the gitops directory
   - Create a pull request for review
   - Approved changes are synced to clusters through GitOps controllers

## Getting Started

1. Clone this repository
2. Set up required credentials for your AWS environment
3. Follow environment-specific instructions in the respective directories

## Contributing

1. Create feature branches from main
2. Follow the PR template for submitting changes
3. Ensure all automated tests pass
4. Get approval from code owners before merging
