# Azure Kubernetes Service (AKS) Deployment Tutorial

Hello everyone, and welcome to my AKS deployment tutorial!

In this guide, I will walk you through the end-to-end process of deploying an Azure Kubernetes Service (AKS) cluster from scratch. We'll leverage the [Azure DevOps Demo Generator](https://azuredevopsdemogenerator.azurewebsites.net/) as our starting point, which provides sample source code, Dockerfiles, Docker Compose files, and Kubernetes manifest files to make the process smoother.

By the end of this tutorial, you'll know how to set up and automate the deployment of key Azure resources, including:

- **Azure Container Registry (ACR)**
- **Azure Kubernetes Service (AKS)**
- **Azure SQL Server**
- **Azure SQL Database**
- **Infrastructure-as-Code using Terraform**

---

## Prerequisites

- An active [Azure DevOps](https://dev.azure.com/) account
- Azure subscription with sufficient permissions
- [Terraform](https://www.terraform.io/downloads.html) installed (or use Azure DevOps pipeline tasks)
- Basic knowledge of Git and Azure

---

## Step 1: Create a New Repository (Without README)

1. **Create a new repository** in your Azure DevOps project.
   - _Tip: Do **not** add a README file during creation._
   - This allows you to use the **Import** feature, which lets you pull in code and files from other public repositories, such as those provided by the Demo Generator.
2. After the repo is created, use the **Import** option (found under `Repos > Files > Import`) to bring in files or folders from a public repository URL.

---

## Step 2: Organize Required Files

Make sure your repository contains the following:

- **Source code** (application code)
- **Dockerfile** (to build your container images)
- **Docker Compose file** (for multi-container scenarios)
- **Kubernetes manifest files** (for AKS deployments)
- **Terraform code** (to provision Azure resources)

You can find these files in the repo you imported from the Demo Generator or add them manually if needed.

---

## Step 3: Prepare Terraform Code

Your Terraform scripts should define the following resources:

- `azurerm_resource_group` – Resource group for organizing resources
- `azurerm_container_registry` – Private container registry
- `azurerm_kubernetes_cluster` – AKS cluster
- `azurerm_mssql_server` and `azurerm_mssql_database` – SQL Server and Database for app data
- `azurerm_role_assignment` – To allow AKS access to pull images from ACR

Be sure to parameterize secrets and sensitive values using Terraform variables, and reference those variables using Azure DevOps variable groups for secure storage.

---

## Step 4: Set Up Azure DevOps Pipeline

1. **Create a new pipeline** in Azure DevOps, connecting it to your repository.
2. Use a YAML pipeline definition for better version control and flexibility.
3. Link any variable groups needed (e.g., for SQL admin credentials).
4. Add pipeline tasks for:
   - Terraform initialization (`terraform init`)
   - Terraform validation (`terraform validate`)
   - Terraform plan and apply (`terraform plan`, `terraform apply`)
   - (Optional) Docker build and push, Kubernetes deployment, SQL migrations, etc.

---

## Step 5: Run the Pipeline and Monitor Deployment

- Queue the pipeline and monitor the output.
- If you encounter errors (permissions, password complexity, etc.), review the error logs and adjust your configuration or Azure resource permissions as needed.

---

## Additional Tips

- **Use strong passwords and store them securely** in Azure DevOps variable groups.
- **Grant appropriate permissions** to the pipeline’s service principal or managed identity, especially for resource creation and role assignments.
- **Review Azure’s security and compliance recommendations** for production workloads.

---

## Conclusion

By following these steps, you will have a fully automated pipeline for deploying AKS and its supporting resources on Azure using best practices for infrastructure-as-code and DevOps.

---

Feel free to reach out or open an issue if you encounter any problems or have suggestions for improvement!

Happy deploying! 🚀
