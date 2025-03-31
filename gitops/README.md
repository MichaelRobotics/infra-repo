# GitOps Repository

This repository contains Kubernetes manifests and configuration managed through GitOps principles for our infrastructure across development, staging, and production environments.

## Repository Structure

### /base
Contains global, reusable configurations that can be applied across clusters and environments:
- **policies/**: Security policies (PodSecurityPolicies, NetworkPolicies)
- **helm-charts/**: Shared Helm charts (e.g., ingress-nginx)
- **kustomization.yaml**: Base Kustomize config for shared resources

### /clusters
Environment and account-specific configurations:
- **dev/**: Development environment configs
- **stage/**: Staging environment configs
- **prod/**: Production environment configs

Each environment contains account-specific subdirectories:
- **networking/**: Network resources (VPCs, subnets)
- **workload/**: Application workloads and EKS cluster configs
- **operation/**: Operational tools
- **observability/**: Monitoring resources
- **data/**: Database and storage resources

### /applications
Business application manifests:
- **payment-gateway/**: Payment gateway service
- **fraud-detection/**: Fraud detection service

Applications follow a structure of:
- **base/**: Shared application config
- **overlays/**: Environment-specific configurations
  - **dev/**: Development configs (e.g., 1 replica)
  - **stage/**: Staging configs (production-like but isolated)
  - **prod/**: Production configs (HA, multi-AZ, etc.)

## Usage

1. Changes to this repository trigger CI/CD pipelines to apply them to the respective clusters
2. Use kustomize to combine base configurations with environment-specific overlays
3. Follow the GitOps workflow: changes should be made through pull requests, reviewed, and merged

## Best Practices

1. Never apply changes directly to clusters
2. Use sealed secrets for sensitive data
3. Version all changes through Git
4. Always verify changes in lower environments before promoting to production
5. Use the appropriate overlay for environment-specific configurations
