**Point to different subscription**

`az account set --subscription <subscription name>`

**List accounts**

```
az account list --output table
```

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

**Post to webhook for azure automation:**

curl -d "" -X POST [https://s1events.azure-automation.net/webhooks?token=v56W%2fxYfwnbXmFQJA8xrQ0N%2fP%2fakiORMwHEwONoWG4g%3d](https://s1events.azure-automation.net/webhooks?token=v56W%2fxYfwnbXmFQJA8xrQ0N%2fP%2fakiORMwHEwONoWG4g%3d)

**Service Endpoints:**

Storage - Enable access to storage blob from all VMs in a virtual network.  Also reduces hops and should increase speed of downloads.  To validate:   `traceroute tobystorage1973.blob.core.windows.net -T`

From network:

1. select subnet to enable service endpoint
2. select Microsoft.Storage
3. save  

From storage account: under 'Firewalls and virtual networks'

1. change 'Allow access from' to Selected networks
2. click '+ Add existing virtual network', select network/subnet that you added storage endpoint to.
3. save



