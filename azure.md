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



