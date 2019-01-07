#### Setup

**Powershell / Azure modules on Mac:**

```
$ brew tap caskroom/cask
$ brew cask install powershell
$ pwsh # connect to powershell core
$ Install-Module -Name AzureRM.Netcore
```

```
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

#### Review Deployment Errors with Tracking ID:

```
Get-AzureRmLog -CorrelationId ed06c5cb-0e0d-4aaa-b85c-1fd4d1db4841 -DetailedOutput
```



