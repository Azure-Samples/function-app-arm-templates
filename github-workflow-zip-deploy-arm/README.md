# Github Workflow for deployment using ARM Template
This workflow can be used when the following conditions are met:
1. Function app is locked behind [private endpoint](https://docs.microsoft.com/en-us/azure/app-service/networking/private-endpoint).
2. Storage account is locked behind [private endpoints](https://docs.microsoft.com/en-us/azure/storage/common/storage-private-endpoints).
3. Want to setup [continuous deployment](https://docs.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment) pipeline for GitHub repo.

### Pre-requisite
1. Have a copy of the ARM template [azuredeploy.json](/github-workflow-zip-deploy-arm/azuredeploy.json) in the root of the repo.
2. Setup [Azure Service Principle for RBAC as Deployment Credential](/github-workflow-zip-deploy-arm#Azure-Service-Principle-for-RBAC-as-Deployment-Credential) using the steps below.
3. Update evironment variables in the `workflow.yml` with those of your app.
4. This template is for DotNet function app on Windows OS. Please refer [sample templates](https://github.com/Azure/actions-workflow-samples/tree/master/FunctionApp) for other languages and OS to modify this template accordingly.

### Azure Service Principle for RBAC as Deployment Credential
You have to create an [Azure Service Principal for RBAC](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview) and add them as a GitHub Secret in your repository.
1. Download Azure CLI from [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest), run `az login` to login with your Azure credentials.
2. Run Azure CLI command
```
   az ad sp create-for-rbac --name "myApp" --role contributor \
                            --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Web/sites/{app-name} \
                            --sdk-auth

  # Replace {subscription-id}, {resource-group}, and {app-name} with the names of your subscription, resource group, and Azure function app.
  # The command should output a JSON object similar to this:

  {
    "clientId": "<GUID>",
    "clientSecret": "<GUID>",
    "subscriptionId": "<GUID>",
    "tenantId": "<GUID>",
    (...)
  }
```
3. Paste the json response from above Azure CLI to your Github Repository > Settings > Secrets > Add a new secret > **AZURE_CREDENTIALS**

### Dependencies on other Github Actions
* [Checkout](https://github.com/actions/checkout) Checkout your Git repository content into GitHub Actions agent.
* [Azure Login](https://github.com/Azure/actions) Login with your Azure credentials for function app deployment authentication.
* To build app code in a specific language based environment, use setup actions:
  * [Setup DotNet](https://github.com/actions/setup-dotnet) Build your DotNet core function app or function app extensions.
  * [Setup Node](https://github.com/actions/setup-node) Resolve Node function app dependencies using npm.
  * [Setup Python](https://github.com/actions/setup-python) Resolve Python function app dependencies using pip.
  * [Setup Java](https://github.com/actions/setup-java) Resolve Java function app dependencies using maven.

If you are looking for a GitHub Action to deploy your customized container image into an Azure Functions container, use [`azure/functions-container-action`](https://github.com/Azure/functions-container-action).