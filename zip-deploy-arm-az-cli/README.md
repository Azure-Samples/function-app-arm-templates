# Az CLI commands for deployment using ARM Template
This workflow can be used when the following conditions are met:
1. Function app is locked behind [private endpoint](https://docs.microsoft.com/en-us/azure/app-service/networking/private-endpoint).
2. Storage account is locked behind [private endpoints](https://docs.microsoft.com/en-us/azure/storage/common/storage-private-endpoints).
3. Want to deploy from your local machine that is not in the Virtual Network.

### PRe-requisite
1. Build and create [.zip package](https://github.com/Azure-Samples/function-app-arm-templates/wiki/Best-Practices-Guide#deployment-zip-file-requirements) of your code in a folder.
2. Have a copy of the ARM template [azuredeploy.json](/zip-deploy-arm-github-workflow/azuredeploy.json) in the same folder.
3. Have a copy of the ARM template [azuredeploy.parameters.json](/zip-deploy-arm-github-workflow/azuredeploy.parameters.json) in the same folder.

### Steps:

1. Run the following commands in PowerShell Command prompt: 

```
az login  

az ad sp create-for-rbac --name <function-app-name> --role contributor --scopes /subscriptions/<subscription-id>/resourceGroups/<resource-group-name> --sdk-auth  

az storage account create -n <new-deployment-storage> -g <resource-group-name>  

az storage container create -n <new-deployment-container> --account-name <new-deployment-storage>  

az storage blob upload -f <local-zip-path> --account-name <new-deployment-storage> -c <new-deployment-container> -n package.zip --overwrite true  

az storage blob generate-sas --full-uri --permissions r --expiry (get-date).AddMinutes(30).ToString("yyyy-MM-ddTHH:mm:ssZ") --account-name <new-deployment-storage> -c <new-deployment-container> -n package.zip 
```

2. Copy paste the SAS URL generated above and your function app name in the azuredeploy.parameters.json

3. Run rest of the commands in PowerShell Command prompt:

```
az deployment group create --name <name-for-deployment> --resource-group <resource-group-name> --template-file azuredeploy.json --parameters azuredeploy.parameters.json 

az storage container delete -n <new-deployment-container> --account-name <new-deployment-storage> 
```
