---
description: This template provisions a function app on a Flex Consumption plan.
page_type: sample
products:
- azure
- azure-resource-manager
urlFragment: function-app-linux-flex-consumption
languages:
- json
---
# Azure Function App Hosted on Flex Consumption Plan (Linux)

This sample Azure Resource Manager template deploys an Azure Function App on Flex Consumption plan (Linux) and required resource including code package deployment with remote build option.

[![Deploy to Azure](/images/deploytoazure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Ffunction-app-arm-templates%2Fmain%2Ffunction-app-linux-flex-consumption%2Fazuredeploy.json)

### OS

This template is for Azure Function app hosted on **Flex Consumption plan (Linux)** only.

### Flex Consumption Plan

The Azure Function app provisioned in this sample uses an [Azure Functions Flex Consumption plan](https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-plan).

+ **Microsoft.Web/serverfarms**: The Azure Functions Flex Consumption plan

### Azure Function App

The Function App uses the [AzureWebJobsStorage__accountName](https://learn.microsoft.com/en-us/azure/azure-functions/functions-app-settings#azurewebjobsstorage__accountname) app setting to connect to a Storage Account and [configured deployment settings](https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-how-to?tabs=azure-cli%2Cvs-code-publish&pivots=programming-language-python#configure-deployment-settings) with system-assigned identity.

+ **Microsoft.Web/sites**: The function app instance.

### OneDeploy
To deploy/release new code with .ZIP package. It uses storage account and authentication method [configured in deployment settings](../function-app-linux-flex-consumption/azuredeploy.json#L220C5-L231C6)

+ **Microsoft.Web/sites/extensions**: Allows choosing remote build process (for example: to get Linux specific packages in python, node.js) in OneDeploy extension using the following property:
    + `"remoteBuild": true` => enable remote build
    + `"remoteBuild": false` => disable remote build

### Azure Storage account

The Storage account that the Function uses for operation and for file contents.

+ **Microsoft.Storage/storageAccounts**: [Azure Functions requires a storage account](https://docs.microsoft.com/azure/azure-functions/storage-considerations) for the function app instance.

### Application Insights

[Application Insights](https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview) is used to provide [monitor the Azure Function](https://docs.microsoft.com/azure/azure-functions/functions-monitoring).

+ **Microsoft.Insights/components**: The Application Insights instance used by the Azure Function for monitoring.

`Tags: Microsoft.Storage/storageAccounts, microsoft.insights/components, Microsoft.Web/serverfarms, Microsoft.Web/sites, Microsoft.Web/sites/extensions`
