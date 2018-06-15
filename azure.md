**List available VM images:**

```
az vm image list --output table
```

**List VM sku's:**

```
az vm list-skus --output table
```

OMS - Operations Management Suite

**Notes:**

Can't create the following with ARM Templates:

* Resource Groups
* Storage blob containers

When using a parameter file locally in ansible repo you have to remove the top level objects or it will fail.

I was able to get your code working by changing the parameters json. Apparently, when it's inline, the top level objects aren't needed.

**Storage:**

Get connection string:  
`az storage account show-connection-string --name tobystorage1973 --resource-group tobyS3`

Get list of items in a container:

`az storage blob list --container-name tobytest --connection-string "connection string here"`

Upload file to container:

`az storage blob upload -f createRG.yml -c tobytest --connection-string`



**Powershell / Azure modules on Mac:**

brew tap caskroom/cask

brew cask install powershell

pwsh

Install-Module -Name AzureRM.Netcore

