# Qualys Cloud Agent installation using Azure Resource Manager (ARM) template

Install Qualys Cloud Agent on Azure VMs using Azure Resource Manager template either through Azure Portal or using Powershell.

## License
***THIS SCRIPT IS PROVIDED TO YOU "AS IS." TO THE EXTENT PERMITTED BY LAW, QUALYS HEREBY DISCLAIMS ALL WARRANTIES AND LIABILITY FOR THE PROVISION OR USE OF THIS SCRIPT. IN NO EVENT SHALL THESE SCRIPTS BE DEEMED TO BE CLOUD SERVICES AS PROVIDED BY QUALYS***

## Description
You can use these ARM templates to deploy and install Qualys Cloud Agent on list of Azure Virtual machines (Windows and Linux) as Virtual Machine extension. VM extensions can be used whenever a virtual machine requires software installation, anti-virus protection or run a script inside of it.

## Usage:
Extensions can be bundled with a new VM deployment, or run against any existing virtual machine(s). The scope of these Azure ARM Templates is to install Qualys Cloud Agent (CA) as VM extension on existing Virtual machine(s).

### PLEASE NOTE : With this approach, i.e installing Cloud Agent (CA) as VM extension, users will be able to see Vulnerability Assessment findings in their Qualys Subscriptions and not in Azure Security Center.

## Pre-Requisites:
1. User should have an active Qualys subscription.
2. User should have have License Code available with them. To know more about retrieving License code, click here.
3. Ensure you have sufficient permissions to create and deploy Azure ARM templates using Azure Portal. To know more about the permissions required, please refer the [permissions](https://github.com/Qualys/CloudAgent-Azure-ARMTemplate/blob/master/Readme.md#permissions-required-for-deploying-azure-arm-template) section.
4. If using Powershell to deploy the ARM template, ensure Azure powershell cmdlets is installed in you system.

## Permissions required for deploying Azure ARM template:
The following are permissions required specific to list, deploy, validate and update Azure ARM template:
```
- Microsoft.Resources/deployments/read                      | Get or lists deployments.
- Microsoft.Resources/deployments/write                     | Creates or updates an deployment.
- Microsoft.Resources/deployments/validate/action           | Validates an deployment.
- Microsoft.Resources/deployments/operations/read           | Gets or lists deployment operations.
- Microsoft.Resources/deployments/operationstatuses/read    | Gets or lists deployment operation statuses.
```
Apart from this access permissions specific to Virtual Machines extensions are required as well, i.e :
```
- Microsoft.Compute/virtualMachines/extensions/read         | Get the properties of a virtual machine extension
- Microsoft.Compute/virtualMachines/extensions/write        | Creates a new virtual machine or updates an existing one.
```
For further understanding, refer the **Understanding the different roles** and **Azure Built-in roles** in [Reference Links](https://github.com/Qualys/CloudAgent-Azure-ARMTemplate/blob/master/README.md#reference-links) section.

## How to Use
### Using Azure portal
1. To deploy through Azure portal, click on the respective buttons **Deploy To Azure**. This approach will deploy templates from our Github repository.

Deploy Cloud Agent on Windows VM(s)

[![Deploy To Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fqualys%2FCloudAgent-Azure-ARMTemplate%2Fmaster%2FWindowsQCA.json)

Deploy Cloud Agent on Linux VM(s)

[![Deploy To Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fqualys%2FCloudAgent-Azure-ARMTemplate%2Fmaster%2FLinuxQCA.json)

2. This will open a pane within Azure portal that allows you to easily provide input parameter values

![image](https://user-images.githubusercontent.com/51158720/93367892-c2676800-f86a-11ea-81d5-51a55d9af7ef.png)

**Input Parameters:**
- *vmName: This is a required field. This input parameter accepts name of Virtual Machine or Virtual Machines where you want to install Qualys Cloud Agent.*
- *vmLocation: This is also a required field which accepts input as the location of the Virtual machine.*
- *LicenseCode: This field accepts input as the license code that was retrieved from Qualys subscription.*

3. Once, you complete with filling of all the required input parameter fields. click **Review + create**.
4. The portal navigates to **Review + create** pane where template gets validated.
5. Once, you get **Validation Passed** status, click **Create** to deploy the template.

### Using Powershell
To deploy to **resource group**, use the following Azure powershell command:

#### `A. For templates Stored in local system`

***PS C:\New-AzResourceGroupDeployment -Name Example_deployment -ResourceGroupName Example_resourcegroup -TemplateFile c:\MyTemplates\azuredeploy.json -TemplateParameterFile c:\MyTemplates\azuredeploy.paramters.json***

Please note that the pre-requisite is to have a template to deploy. If you don't already have one , create and save. Also, if you are using your local system, you should:
- ***Install Azure Powershell cmdlets on your local computer.*** for more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps?view=azps-4.6.1)
- ***Connect to Azure by using [`Connect-AzAccount`](https://docs.microsoft.com/en-us/powershell/module/az.accounts/connect-azaccount?view=azps-4.6.1) Azure powershell cmdlet.***

For the example script above, we are referring local file name as **c:\MyTemplates\azuredeploy.json** and **c:\MyTemplates\azuredeploy.parameters.json** for ARM template and parameter file respectively and this command can be executed from your local system.


#### `B. In case, your template file and parameter file are stored on external locations (such as Github, Azure Storage, etc.)`

***PS C:\New-AzResourceGroupDeployment -Name Example_deployment -ResourceGroupName Example_resourcegroup -TemplateUri https://raw.githubusercontent.com/Azure/master/azuredeploy.json -TemplateParameterUri https://raw.githubusercontent.com/Azure/master/azuredeploy.parameters.json***

Where,
- ***[TemplateFile](https://github.com/Qualys/CloudAgent-Azure-ARMTemplate/tree/master/Example_templates_parameter_file/exampleTemplate.json)***: Will accept the local file path of the ARM JSON template is stored.
- ***[TemplateParameterFile](https://github.com/Qualys/CloudAgent-Azure-ARMTemplate/tree/master/Example_templates_parameter_file/example.parameters.json)***: will accept the local file path where Parameter JSON file is stored.
- ***TemplateUri***: Is the external location of the template file and
- ***TemplateParameterUri***: Is the external location of the parameter file.

**NOTE: THE POWERSHELL SCRIPTS MENTIONED ABOVE ARE AN EXAMPLE, PLEASE REPLACE THE VALUES AS PER THE REQUIREMENTS**

For further more detailed information on how parameters can be passed as Inline values or deploy from Azure cloud shell, please refer the [Reference Links](https://github.com/Qualys/CloudAgent-Azure-ARMTemplate/blob/master/README.md#reference-links) section.

## Reference Links
- [How to Retrieve License Code from Qualys Subscription](https://qualys-secure.force.com/discussions/s/article/000005837#license), please refer **Retrieve the License Code and Public Key from your Qualys Subscription** section.
- [Deploy from Powershell/Azure CloudShell](https://qualys-secure.force.com/discussions/s/article/000005837#license)
- [Deploy from Portal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/deploy-portal)
- [Understanding the different roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-roles)
- [Azure Built-in roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)
- [Get Started with Azure Powershell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps?view=azps-4.6.1)
- [Powershell cmdlet for Resources](https://docs.microsoft.com/en-us/powershell/module/az.resources/?view=azps-4.6.1#resources)
