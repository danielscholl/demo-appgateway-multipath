# Proof of Concept - Application Gateway using Multipath

This proof of concept implements a 3 region multi path website controlled by Traffic Manager to route traffic to the proper location. 



![[0]][0]
_Architecture Diagram_

This proof of concept uses the following Azure load-balancing and services portfolio:  Traffic Manager, Application Gateway, App Service Plan, and Web Apps.

- __Traffic Manager__ provides global DNS load balancing.  It looks at incoming DNS requests and responds with a healthy endpoint. Performance is the currently selected routing option.

- __Application Gateway__ provides the delivery controller using the Layer 7 load balancing capabilities to route traffic based on the URI to different Web Apps.

- __App Services__ provides the hosting of the Web App and API App.

The following design goals were achieved by this POC.

- __Multi-geo redundancy:__  If one region goes down, Traffic Manager routes traffic seamlessly to the closest region without any involvment from the application owner.

- __Reduced Latency:__ Traffic Manager automatically directs the customer to the closet region

- __Application Seperation:__ The application is deployed as seperate websites but are presented as a single website and solves for complex CORS rules and presents the ability to do SSL offloading.


>Note: This proof of concept automatically deploys a small hello world sample PHP app to the web and api sites to show what backend is delivering the content.

__Automatically Deploy the Solution:__

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdanielscholl%2Fpoc-appgateway-multipath%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>


__Manually Deploy the Solution:__

```powershell
# Azure CLI Instructions
az group create  --name demo --location southcentralus
az group deployment create --name appgw-path-demo `
 --template-file azuredeploy.json `
 --resource-group demo

# Azure Powershell Instructions
New-AzureRmResourceGroup -Name demo -Location southcentralus
New-AzureRmResourceGroupDeployment -Name appgw-path-demo `
  -TemplateFile azuredeploy.json `
  -ResourceGroupName demo
```

[0]: ./images/architecture.png "Architecture Diagram"