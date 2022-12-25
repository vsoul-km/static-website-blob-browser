---
services: storage
platforms: javascript
author: David Zheng
---

# Static Website Sample - File Browser app for Blob Storage 

This sample application can be used as a static website on Azure Storage to list the contents of a Blob container (anonymously). The project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app). The sample assumes your blob container is made public, however it can be modified to use Azure Active Directory authentication. The file browser also allows downloading each file with a single click.

## Demo
Try the app here: https://mscssstatic.blob.core.windows.net/staticwebsite/index.html

## Pre-requsites
- Create an [Azure Storage account](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM.3.0.5) (GPv2) 
- (Optional)Enable [Static Websites](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website)
- Install VSCode
- Install git/TortoiseGit
- install Node.js https://nodejs.org/en/download/ (without Chocolatey)
- Git clone the project

## Prepare VS Code
- Install Azure Storage extension
- Open the project folder in VS Code and install React Scripts using VS Code terminal: npm install react-scripts --save
- [optional] Add NPM commands to VS Code: View -> open view -> npm scripts
- Log on to the Azure Storage extension.


## Deploy the sample - step by step
Follow the following steps to deploy the sample on your Azure Storage account. Once deployed, the sample app will provide you a file browser view of your **$web** container. If you desire so, you can change the container in the `index.js` to any other public container.
- Open index.js and change in the code
`const account = 'staticwebsitedemo'`
`const container = '$web'`

'staticwebsitedemo' - to your Azure Storage Account
'$web' - container in a blob storage to list files

- [optional] web page title in index.html (<title>...</title)

- Build the app by clicking run in in the NPM Scripts -> build menu
- Right click `build` folder in VSCode, and click `Deploy to Static Website`
- Choose your storage account to deploy the static website

Once you have deployed, configure the container as public, and set the CORS settings to allow access from the static website endpoint.
- Go to Azure Portal, select your storage account
- Click CORS on the menu. And add a new row
  * Allowed origin: https://staticwebsitedemo.z20.web.core.windows.net (your static website endpoint) *Note: in CORS there is needed to use static web site link without a slash / at the and of the url (go to storage account → static website to detect static web site name)
  * Allowed methods: GET, OPTIONS, HEAD
  * Allowed headers and exposed headers: *
- Go to Blobs menu
- Click on the `...` next to the desired blob container (in the sample, $web is used)
- Click on `Access Policy` and configure `Public Access for the Container`. This is required for anonymously listing blobs using the SDK.
- Go to storage account → Access Control IAM → Role Assignments → Add (role assignment) → Storage Blob Data Owner → Members → Select Members → Start writing the name of your storage account and then select service application subscription user (like SomeName-ee7d8ff34-1d38-4c50-9ea6-ae07586ad769) → Assign

![Blob browser - Static website](https://raw.githubusercontent.com/seguler/static-website-blob-browser/master/staticwebsitedemo.jpg)


## More information
- [Azure Storage SDK for JS](https://github.com/azure/azure-storage-js)
- [Static Websites on Azure Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website)
- [Deploy a Static Website with VSCode](https://code.visualstudio.com/tutorials/static-website/getting-started)
