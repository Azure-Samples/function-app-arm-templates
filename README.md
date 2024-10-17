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
- azure-functions
- azure
---

# ARM Templates for Function App Deployment

This repo contains currently available Azure Resource Manager templates for deploying Function App with recommended settings and best practices. 

Create and deploy Functions app for following OS and SKU combinations:

1. Create [Function App with Premium Plan](/function-app-premium-plan) on Windows/Linux
2. Create [Function App with Dedicated Plan](/function-app-dedicated-plan) on Windows/Linux
3. Create [Function App with Consumption Plan on Windows](/function-app-windows-consumption)
4. Create Function App with Consumption Plan on Linux:
    - [Deploy zip package with Run From Package](/function-app-linux-consumption)
    - [Deploy zip package with Remote Build](/function-app-linux-consumption-remote-build)
5. Create [Function App with Flex Consumption Plan on Linux](/function-app-linux-flex-consumption)

Create Functions app and resources for following networking scenarios:

1. Create [Function App with a Deployment Slot](/function-app-deployment-slot)
2. Create [Function App with Virtual Network Integration](/function-app-vnet-integration)
3. Create [Function App with Azure Storage private endpoints](/function-app-storage-private-endpoints)
4. Create [Function App with private endpoints and Azure Storage with private endpoints](/function-app-private-endpoints-storage-private-endpoints)
    
Deploy Functions app code for following scenarios:
1. Deploy [Function App with ZipDeploy using Run From Package](/zip-deploy-run-from-package)
2. If Function App with private endpoints and Azure Storage with private endpoints:
    - Deploy [Function App with ARM template using Az CLI](/zip-deploy-arm-az-cli)
    - Deploy [Function App with ARM template in GitHub Workflow](/zip-deploy-arm-github-workflow)

This repo also contains wiki pages on the following:

1. [Best Practices Guide](../../wiki/Best-Practices-Guide)
2. [Frequently Asked Questions (FAQs)](../../wiki/Frequently-Asked-Questions-(FAQs))
3. [Important App Settings for Function Apps](../../wiki/App-Settings-for-Function-Apps)
4. [ARM Templates for Function App with different Hosting Plans](../../wiki/ARM-Templates-for-Function-Apps-with-different-Hosting-Plans)

For more information on deploying ARM template, please refer: [Deploy resources with ARM templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/deploy-portal)


