# Function App Deployment with ZipDeploy Run From Package

### ZipDeploy with ARM template

ZipDeploy is intended for xcopy or ftp style deployment. By default, It unzips the artifacts and lay them out exactly to d:\home\site\wwwroot. You can use any tooling (such as one coming with Windows) to zip your content.

It is recommended to set appSettings `WEBSITE_RUN_FROM_PACKAGE=1`, to allow Zip package deployed with ZipDeploy to mount as read-only virtual filesystem directly without deflating or extracting. The advantage is to allow atomic and reliable deployment (no more files being locked). 

NOTE: ZipDeploy with the appSetting `WEBSITE_RUN_FROM_PACKAGE=1` is not supported for Linux Consumption plan.

If you have an existing Function App with right appSettings and want to perform deployment with ZipDeploy extension, then here is the template:

[![Deploy to Azure](/images/deploytoazure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Ffunction-app-arm-templates%2Fmain%2Fzip-deploy-run-from-package%2Fazuredeploy.json)

The following example shows declartion of ZipDeploy extension in site resources along with the recommended WEBSITE_RUN_FROM_PACKAGE appSetting:

NOTE: Please include rest of the existing app settings in the template to preserve them.

```json
{
  "name": "[parameters('siteName')]",
  "type": "Microsoft.Web/sites",
  "apiVersion": "2021-02-01",
  "location": "[parameters('location')]",
  "properties": {
    "siteConfig": {
      "appSettings": [
        {
          "name": "WEBSITE_RUN_FROM_PACKAGE",
          "value": "1"
        }
      ]
    }
  },
  "resources": [
    {
      "name": "ZipDeploy",
      "type": "Extensions",
      "apiVersion": "2021-02-01",
      "dependsOn": [
        "[concat('Microsoft.Web/sites/', parameters('siteName'))]"
      ],
      "properties": {
        "packageUri": "[parameters('packageUri')]"
      }
    }
  ]
}
```

Since it will mount as read-only, app runtime will not be able to create or modify files under d:\home\site\wwwroot. In addition, Azure Functions Portal will also prevent you from modifying the Function Apps.

### For Linux Consumption plan:

1. Do not use ZipDeploy extension.
2. Set appSetting `WEBSITE_RUN_FROM_PACKAGE=URL` for deployment using the .zip package url. For example: 

NOTE: Please include rest of the existing app settings in the template to preserve them.

```json
{
  "name": "[parameters('siteName')]",
  "type": "Microsoft.Web/sites",
  "apiVersion": "2021-02-01",
  "location": "[parameters('location')]",
  "properties": {
    "siteConfig": {
      "appSettings": [
        {
          "name": "WEBSITE_RUN_FROM_PACKAGE",
          "value": "[parameters('packageUri')]"
        }
      ]
    }
  }
}
```
