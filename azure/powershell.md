# powershell

## Setup

**Powershell / Azure modules on Mac:**

```text
$ brew tap caskroom/cask
$ brew cask install powershell
$ pwsh # connect to powershell core
$ Install-Module -Name AzureRM.Netcore
```

```text
 $ Login-AzureRmAccount
```

## Get current subscription info:

```text
Get-AzureRMContext
```

## Get available subscriptions:

```text
Get-AzureRmSubscription
```

## Set context to different subscription:

```text
Set-AzureRmContext -SubscriptionId <id>
```

## Review Deployment Errors with Tracking ID:

```text
Get-AzureRmLog -CorrelationId ed06c5cb-0e0d-4aaa-b85c-1fd4d1db4841 -DetailedOutput
```

