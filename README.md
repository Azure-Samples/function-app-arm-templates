---
page_type: sample
languages:
- csharp
- python
- java
- nodejs
- typescript
- json
products:
- azure-resource-manager
- azure-functions
- templates
- azure
---

# ARM Templates for Function App Deployment

This repo contains currently available Azure Resource Manager templates for deploying Function App with recommended settings and best practices. 

Templates for the following OS and SKU are available:

1. Create [Function App with Consumption Plan on Linux](/function-app-linux-consumption)
2. Create [Function App with Consumption Plan on Windows](/function-app-windows-consumption)
3. Create [Function App with Premium Plan](/function-app-premium-plan) on Windows/Linux
4. Create [Function App with Dedicated Plan](/function-app-dedicated-plan) on Windows/Linux

Templates for the following deployment and networking scenarios are available:

1. Create [Function App with a Deployment Slot](/function-app-deployment-slot)
2. Create [Function App with Virtual Network Integration](/function-app-vnet-integration)
3. Create [Function App with Azure Storage private endpoints](/function-app-storage-private-endpoints)
4. Deploy [Function App with ZipDeploy using Run From Package](/zip-deploy-run-from-package)

This repo also contains wiki pages on the following:

1. [Best Practices Guide](../../wiki/Best-Practices-Guide)
2. [Frequently Asked Questions (FAQs)](../../wiki/Frequently-Asked-Questions-(FAQs))
3. [Important App Settings for Function Apps](../../wiki/App-Settings-for-Function-Apps)
4. [ARM Templates for Function App with different Hosting Plans](../../wiki/ARM-Templates-for-Function-Apps-with-different-Hosting-Plans)

For more information on deploying ARM template, please refer: [Deploy resources with ARM templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/deploy-portal)


