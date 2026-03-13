# test-project - Terraform Infrastructure

Infrastructure as Code for test-project using Terraform with modules from [templates repository](https://github.com/lucas-aversari/templates).

## 📁 Directory Structure

```
IAC/
├── Environments/
│   ├── dev/
│   │   ├── provider.tf           # Terraform & provider config for dev
│   │   └── variables.tfvars      # Dev environment configuration
│   ├── qa/
│   │   ├── provider.tf           # Terraform & provider config for qa
│   │   └── variables.tfvars      # QA environment configuration
│   └── prod/
│       ├── provider.tf           # Terraform & provider config for prod
│       └── variables.tfvars      # Prod environment configuration
├── .gitignore                    # Protects sensitive files
└── README.md                     # This file
```

## 🏗️ Configuration Pattern

Each environment directory contains two files:

### provider.tf
Defines Terraform version, required providers, backend configuration, and Azure provider settings.

### variables.tfvars
Defines the resources to be created and their configuration. All infrastructure is declared here using variables that reference modules from the templates repository.

## Deployed Resources

- Resource Group
- Storage Account
- Key Vault

## Usage

This infrastructure is automatically deployed via GitHub Actions workflow.

### Manual Deployment

```bash
cd IAC/Environments/dev
terraform init \
  -backend-config="resource_group_name=${{ secrets.TF_STATE_RG }}" \
  -backend-config="storage_account_name=${{ secrets.TF_STATE_STORAGE }}" \
  -backend-config="container_name=tfstate" \
  -backend-config="key=dev.tfstate"
terraform plan -var-file=variables.tfvars
terraform apply -var-file=variables.tfvars
```

## Created by Terraform Setup Wizard

Generated on: 2026-03-13T12:57:41.962Z
