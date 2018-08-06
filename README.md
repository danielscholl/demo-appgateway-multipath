# Proof of Concept - Application Gateway using Multipath

This proof of concept implements a 3 region multi path website controlled by Traffic Manager to route traffic to the proper location. 

Includes a template and links web deployment to github.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdanielscholl%2Fpoc-appgateway-multipath%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

![[0]][0]
_Architecture Diagram_

__Manually Deploy the Solution:__

```powershell
# Azure CLI
az group create  --name demo --location southcentralus
az group deployment create --name appgw-path-demo `
 --template-file azuredeploy.json `
 --resource-group demo

# Azure Powershell
New-AzureRmResourceGroup -Name demo -Location southcentralus
New-AzureRmResourceGroupDeployment -Name appgw-path-demo `
  -TemplateFile azuredeploy.json `
  -ResourceGroupName demo
```

[0]: ./images/architecture.png "Architecture Diagram"