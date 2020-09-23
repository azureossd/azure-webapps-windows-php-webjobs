
# Azure PHP Web Jobs with Storage SDK

This repository contains a simple sample project to help you getting started with Azure storage using PHP as the development language. This code sample was taken from https://github.com/Azure-Samples/storage-blobs-php-quickstart and adapted to work with Azure Web Jobs.

## Prerequisites

To complete this tutorial:

To complete this quickstart: 
* Install [PHP](http://php.net/downloads.php)
* Install [The Azure SDK for PHP](../../php-download-sdk.md)

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

## Create a storage account using the Azure portal

First, create a new general-purpose storage account to use for this quickstart. 

1. Go to the [Azure portal](https://portal.azure.com/#create/Microsoft.StorageAccount-ARM) and log in using your Azure account. 
2. Enter a unique name for your storage account. Keep these rules in mind for naming your storage account:
    - The name must be between 3 and 24 characters in length.
    - The name may contain numbers and lowercase letters only.
3. Make sure that the following default values are set: 
    - **Deployment model** is set to **Resource manager**.
    - **Account kind** is set to **General purpose**.
    - **Performance** is set to **Standard**.
    - **Replication** is set to **Locally Redundant storage (LRS)**.
4. Select your subscription. 
5. For **Resource group**, create a new one and give it a unique name. 
6. Select the **Location** to use for your storage account.
7. Check **Pin to dashboard** and click **Create** to create your storage account. 

After your storage account is created, it is pinned to the dashboard. Click on it to open it. Under **Settings**, click **Access keys**. Select **key1** to the clipboard followed by the storage account name, then paste it into a text editor for the next step.

## Configure your storage connection string

In the application, you must provide your storage account name and account key to create the BlobRestProxy instance for your application. It is recommended to store these identifiers within an environment variable on the local machine running the application. Use one of the following examples depending on your Operating System to create the environment variable. Replace the youraccountname and youraccountkey values with your account name and key.

### Linux

```bash
export ACCOUNT_NAME=<youraccountname>
export ACCOUNT_KEY=<youraccountkey>
```
### Windows

```bash
set ACCOUNT_NAME=<youraccountname>
set ACCOUNT_KEY=<youraccountkey>
```

## Create and configure WebJob

1. Go to WebJobs section in your web app in portal.
2. Generate a .zip file with all the content of this folder.
3. Uploading and select Triggered Type.
4. Select Triggers -> Manual
5. Go to Application settings and add the following two environment variables

```bash
    ACCOUNT_NAME=<youraccountname>
    ACCOUNT_KEY=<youraccountkey>
```

## Install libraries using KUDU site
1. Navigate through `D:\home\site\wwwroot\App_Data\jobs\triggered\<WebJobName>`
2. Review if your files are there and then run `php composer.phar install`
3. Start the webjob from Azure Portal and check status on `https://<sitename>.scm.azurewebsites.net/azurejobs/#/jobs`

## Implement delete operation
This sample will create randome container names and upload the content of HelloWorld.txt, you can uncomment these lines in index.php and this will delete the containers.

```php
        //Delete container.
        //echo "Deleting Container". $containerName;
        //echo "<br />"
        //$blobClient->deleteContainer($containerName);
```