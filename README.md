# oddball-code-challenge-repo-1761600126966-lambert-azure-devops-engineer

# Coding Challenge

## Problem Description
Tyler, for the Azure Devops Engineer position, we have crafted an intermediate level coding challenge that will test your skills in CI/CD pipelines, Azure services, and Terraform. You will be tasked with debugging and enhancing a set of starter files that are part of a deployment process.

## Requirements
1. Identify and fix the bugs in the provided starter files.
2. Enhance the Terraform configuration to include an additional Azure resource.
3. Write a CI/CD pipeline script that integrates with Azure DevOps to automate the deployment process.
4. Ensure that the pipeline is capable of deploying to multiple environments (staging and production).

## Technical Specifications  
- Use Terraform to define infrastructure in Azure.
- The CI/CD pipeline should be defined using YAML.
- Ensure that all code is properly commented and follows best practices.
- The challenge should be completable in 90 minutes.

## Starter Files

### File 1: `main.tf`
```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "West Europe"
}

resource "azurerm_storage_account" "example" {
  name                     = "examplestoracc"
  resource_group_name      = azurerm_resource_group.example.name
  location                 = azurerm_resource_group.example.location
  account_tier            = "Standard"
  account_replication_type = "LRS"
}

output "storage_account_name" {
  value = azurerm_storage_account.example.name
}
```

### File 2: `azure-pipelines.yml`  
```yaml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: TerraformInstaller@0
  inputs:
    command: 'install'
    terraformVersion: 'latest'

- script: |
    terraform init
    terraform apply -auto-approve
  displayName: 'Run Terraform'

- task: AzureCLI@2
  inputs:
    azureSubscription: 'YourServiceConnection'
    scriptType: 'bash'
    scriptLocation: 'inlineScript'
    inlineScript: |
      echo "Deployment completed successfully!"
```

### File 3: `variables.tf`
```hcl
variable "location" {
  description = "The Azure region to deploy resources."
  type        = string
  default     = "West Europe"
}

variable "storage_account_name" {
  description = "The name of the Azure storage account."
  type        = string
}
```

## Sample Data (if applicable)
No sample data is required for this challenge.

## Evaluation Criteria
- Correctness of the bug fixes and enhancements.
- Quality and clarity of the code.
- Adherence to best practices in Terraform and Azure DevOps.
- Successful execution of the CI/CD pipeline.

## Submission Instructions
Submit your completed files in a ZIP format including:
- `main.tf`
- `azure-pipelines.yml`
- `variables.tf`

Make sure that your files are well-organized and properly commented.