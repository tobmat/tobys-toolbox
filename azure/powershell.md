#### Setup

```
 $ pwsh # connect to powershell core
 $ Login-AzureRmAccount
 
```



#### Get current subscription info:

```
Get-AzureRMContext
```

#### Get available subscriptions:

```
Get-AzureRmSubscription
```

#### Set context to different subscription:

```
Set-AzureRmContext -SubscriptionId <id>
```



