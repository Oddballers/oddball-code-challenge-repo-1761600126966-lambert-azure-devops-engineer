# oddball-code-challenge-repo-1761600126966-lambert-azure-devops-engineer

# Coding Challenge

## Problem Description

Tyler, welcome to your coding challenge for the Azure Devops Engineer position. This task is designed to test your skills at an intermediate level. You will work with Azure Container Registry, a Docker application, and Terraform for infrastructure as code (IaC).

## Requirements

- Deploy an Azure Container Registry repository using Terraform. 
- Create a Docker container image utilizing the provided application code in the `app` directory.
- Create a script to push this created container image to the ACR repository.
- Deploy this container image to infrastructure Azure of your choice, ensuring to pull from the created ACR repository.

## Technical Specifications 

- Use Azure Container Registry for storing your Docker images.
- Use Terraform to define the infrastructure required to host the Docker container on Azure.
- The solution must be completable in 90 minutes.

## Example Files

The example files provided below are not intended to be deployed as is - rather, these are outlines to aid the candidate in crafting their own solution.

### File 1: `main.tf`

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "West Europe"
}

resource "azurerm_container_registry" "example" {
  name                = "exampleregistry123"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  sku                 = "Basic"
  admin_enabled       = true
}

resource "azurerm_linux_web_app" "example" {
  name                = "example-app"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  service_plan_id     = azurerm_service_plan.example.id

  app_settings = {
    "WEBSITES_CONTAINER_IMAGE" = "${azurerm_container_registry.example.login_server}/myapp:latest"
  }
}
```

## Sample Data

No additional sample data is required for this challenge.

## Evaluation Criteria

- Correctness of the Docker application and its deployment.
- Proper use of Terraform to provision resources in Azure.
- Clarity and organization of the codebase.
- Utilizing the Azure and Terraform documentation to utilize "best practice" approach.
