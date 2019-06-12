# CloudAgent-Azure-ARMTemplate
Installing Cloud Agent on Azure Virtual Machines by using Azure Resource Manager template

## License
_**THIS SCRIPT IS PROVIDED TO YOU "AS IS."  TO THE EXTENT PERMITTED BY LAW, QUALYS HEREBY DISCLAIMS ALL WARRANTIES AND LIABILITY FOR THE PROVISION OR USE OF THIS SCRIPT.  IN NO EVENT SHALL THESE SCRIPTS BE DEEMED TO BE CLOUD SERVICES AS PROVIDED BY QUALYS**_


## Description
You can use Azure Resource Manager template to install Cloud Agent (CA) on Azure Linux or Windows VM using VM extension.

## Usage
`Using Azure Portal`
* Deploy CA on Linux VM [![Deploy to Azure Linux VM](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FQualys-Public%2FCloudAgent-Azure-ARMTemplate%2Fmaster%2FLinuxVm.json)

* Deploy CA on Windows VM [![Deploy to Azure Windows VM](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FQualys-Public%2FCloudAgent-Azure-ARMTemplate%2Fmaster%2FWindowsVm.json)

**OR** 

`Using Powershell`

PS C:\ New-AzureRmResourceGroupDeployment -VMName VM_NAME -ResourceGroupName RESOURCE_GROUP_NAME -Location VM_LOCATION -TemplateFile TEMPLATE_FILE_PATH -TemplateParameterFile TEMPLATE_PARAMETER_FILE_PATH

Where,

[TEMPLATE_FILE_PATH](LinuxVm.json) = the path of the template file

[TEMPLATE_PARAMETER_FILE_PATH](/Example/azuredeploy-parameters.json) = the path of parameter file for the template 

**Input Parameters:**
utilize [**azuredeploy-parameters.json**](/Example/azuredeploy-parameters.json) as an example to supply parameters field.

* _vmName: The name of the Virtual Machine where you want to install Qualys CA_
* _vmlocation: The location of the Virtual Machine_
* _LicenseCode: The License Code from your Qualys Subscription_

_**Ensure that you input all the required fields asked in parameters section.**_

## Important Links
**[How to Retrieve License Code from Qualys Subscription](https://community.qualys.com/docs/DOC-5823-deploying-qualys-cloud-agents-from-microsoft-azure-security-center)**
