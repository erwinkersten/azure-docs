---
title: Deploy the MedTech service using an Azure Resource Manager template and Azure PowerShell or Azure CLI - Azure Health Data Services
description: In this article, you'll learn how to deploy the MedTech service using an Azure Resource Manager template and Azure PowerShell or Azure CLI
author: msjasteppe
ms.service: healthcare-apis
ms.subservice: fhir
ms.topic: quickstart
ms.date: 11/29/2022
ms.author: jasteppe
---

# Quickstart: Deploy the MedTech service using an Azure Resource Manager template and Azure PowerShell or the Azure CLI

In this quickstart, you'll learn how to:

> [!div class="checklist"]
> - Use Azure PowerShell or the Azure CLI to deploy an instance of the MedTech service using an Azure Resource Manager template (ARM template).

To implement infrastructure as code for your Azure solutions, use Azure Resource Manager templates (ARM templates). The template is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax, which lets you state what you intend to deploy without having to write the sequence of programming commands to create it. In the template, you specify the resources to deploy and the properties for those resources. 

For more information about ARM templates, see [What are ARM templates?](./../../azure-resource-manager/templates/overview.md)

## Deployment prerequisites

To begin your deployment and complete the quickstart, you must have the following prerequisites:

- An active Azure subscription account. If you don't have an Azure subscription, see [Subscription decision guide](/azure/cloud-adoption-framework/decision-guides/subscriptions/).

- Owner or Contributor and User Access Administrator role assignments in the Azure subscription. For more information, see [What is Azure role-based access control?](../../role-based-access-control/overview.md)

- The Microsoft.HealthcareApis and Microsoft.EventHub resource providers registered with your Azure subscription. To learn more about registering resource providers, see [Azure resource providers and types](../../azure-resource-manager/management/resource-providers-and-types.md).

- [Azure PowerShell](/powershell/azure/install-az-ps) and/or the [Azure CLI](/cli/azure/install-azure-cli) installed locally.

When you have these prerequisites, you're ready to deploy the ARM template.

## Review the ARM template

The ARM template used for this deployment is available from the [Azure Quickstart Templates](/samples/azure/azure-quickstart-templates/iotconnectors/) site using the *azuredeploy.json* file located on [GitHub](https://github.com/azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.healthcareapis/workspaces/iotconnectors/). 

## Deploy the MedTech service with the Azure Resource Manager template and Azure PowerShell

Complete the following five steps to deploy the MedTech service using Azure PowerShell:

1. Sign-in into Azure.

   ```azurepowershell
   Connect-AzAccount
   ```

2. Set your Azure subscription deployment context using your subscription ID. To learn how to get your subscription ID, see [Get subscription and tenant IDs in the Azure portal](/azure/azure-portal/get-subscription-tenant-id).

   ```azurepowershell
   Set-AzContext <AzureSubscriptionId>
   ```

   For example: `Set-AzContext abcdef01-2345-6789-0abc-def012345678`

3. Confirm the location you want to deploy in. See the [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=health-data-services) site for the current Azure regions where Azure Health Data Services is available.

   You can also review the **location** section of the *azuredeploy.json* file.

   If you need a list of the Azure regions location names, you can use this code to display a list:

   ```azurepowershell
   Get-AzLocation | Format-Table -Property DisplayName,Location
   ```

4. If you don't already have a resource group created for this quickstart, you can use this code to create one:

   ```azurepowershell
   New-AzResourceGroup -name <ResourceGroupName> -location <AzureRegion>
   ```

   For example: `New-AzResourceGroup -name ArmTestDeployment -location southcentralus`

   > [!IMPORTANT]
   > For a successful deployment of the MedTech service, you'll need to use numbers and lowercase letters for the basename of your resources. The minimum basename requirement is three characters with a maximum of 16 characters.

5. Use the following code to deploy the MedTech service using the ARM template:

   ```azurepowershell
   New-AzResourceGroupDeployment -ResourceGroupName <ResourceGroupName> -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.healthcareapis/workspaces/iotconnectors/azuredeploy.json -basename <BaseName> -location <AzureRegion>
   ```

   For example: `New-AzResourceGroupDeployment -ResourceGroupName ArmTestDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.healthcareapis/workspaces/iotconnectors/azuredeploy.json -basename abc123 -location southcentralus`

## Deploy the MedTech service with the Azure Resource Manager template and the Azure CLI

Complete the following five steps to deploy the MedTech service using the Azure CLI:

1. Sign-in into Azure.

   ```azurecli
   az login
   ```

2. Set your Azure subscription deployment context using your subscription ID. To learn how to get your subscription ID, see [Get subscription and tenant IDs in the Azure portal](/azure/azure-portal/get-subscription-tenant-id).

   ```azurecli
   az account set <AzureSubscriptionId>
   ```

   For example: `az account set abcdef01-2345-6789-0abc-def012345678`

3. Confirm the location you want to deploy in. See the [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=health-data-services) site for the current Azure regions where Azure Health Data Services is available.

   You can also review the **location** section of the *azuredeploy.json* file. 

   If you need a list of the Azure regions location names, you can use this code to display a list:

   ```azurecli
   az account list-locations -o table
   ```

4. If you don't already have a resource group created for this quickstart, you can use this code to create one:

   ```azurecli
   az group create --resource-group <ResourceGroupName> --location <AzureRegion>
   ```

   For example: `az group create --resource-group ArmTestDeployment --location southcentralus`

   > [!IMPORTANT]
   > For a successful deployment of the MedTech service, you'll need to use numbers and lowercase letters for the basename of your resources.

5. Use the following code to deploy the MedTech service using the ARM template:

   ```azurecli
   az deployment group create --resource-group <ResourceGroupName> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.healthcareapis/workspaces/iotconnectors/azuredeploy.json --parameters basename=<BaseName> location=<AzureRegion>
   ```

   For example: `az deployment group create --resource-group ArmTestDeployment --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.healthcareapis/workspaces/iotconnectors/azuredeploy.json --parameters basename=abc123 location=southcentralus`

## Review deployed resources and access permissions

When deployment is completed, the following resources and access roles are created in the ARM template deployment:

- Azure Event Hubs namespace and device message event hub. In this deployment, the device message event hub is named *devicedata*.

- An event hub consumer group. In this deployment, the consumer group is named *$Default*.

- The Azure Event Hubs Data Sender role. In this deployment, the sender role is named *devicedatasender*.

- A Health Data Services workspace.

- A Health Data Services Fast Healthcare Interoperability Resources (FHIR&#174;) service.

- An instance of the MedTech service for Health Data Services, with the required [system-assigned managed identity](../../active-directory/managed-identities-azure-resources/overview.md) roles:

  - For the device message event hub, the Azure Events Hubs Data Receiver role is assigned in the [Access control section (IAM)](../../role-based-access-control/overview.md) of the device message event hub.

  - For the FHIR service, the FHIR Data Writer role is assigned in the [Access control section (IAM)](../../role-based-access-control/overview.md) of the FHIR service.

## Post-deployment mappings

After you've successfully deployed an instance of the MedTech service, you'll still need to provide conforming and valid device and FHIR destination mappings.

 - To learn about device mappings, see [How to configure device mappings](how-to-use-device-mappings.md).

 - To learn about FHIR destination mappings, see [How to configure FHIR destination mappings](how-to-use-fhir-mappings.md).

## Clean up Azure PowerShell resources

When your resource group and deployed Bicep file resources are no longer needed, delete the resource group, which deletes the resources in the resource group.

```azurepowershell
Remove-AzResourceGroup -Name <ResourceGroupName>
```

For example: `Remove-AzResourceGroup -Name ArmTestDeployment`

## Clean up the Azure CLI resources

When your resource group and deployed Bicep file resources are no longer needed, delete the resource group, which deletes the resources in the resource group.

```azurecli
az group delete --name <ResourceGroupName>
```

For example: `az group delete --resource-group ArmTestDeployment`

> [!TIP]
> For a step-by-step tutorial that guides you through the process of creating an ARM template, see [Tutorial: Create and deploy your first ARM template](../../azure-resource-manager/templates/template-tutorial-create-first-template.md).

## Next steps

In this quickstart, you learned how to use Azure PowerShell or Azure CLI to deploy an instance of the MedTech service using an ARM template. To learn more about other methods of deploying the MedTech service, see

> [!div class="nextstepaction"]
> [Choose a deployment method for the MedTech service](deploy-iot-connector-in-azure.md)

> [!div class="nextstepaction"]
> [Deploy the MedTech service using an Azure Resource Manager template](deploy-02-new-button.md)

> [!div class="nextstepaction"]
> [Deploy the MedTech service manually using the Azure portal](deploy-03-new-manual.md)

FHIR&#174; is a registered trademark of Health Level Seven International, registered in the U.S. Trademark Office and is used with their permission.
