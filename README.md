# Security Baseline
 This repo contains Azure Policies to help establish a security baseline for resources that blocks local authentication during deployment. 

## Instructions
These are the general steps for importing the policy definitions.

1. Download this repo and extract all policy definitions.
1. If using Cloud Shell, upload the JSON definition files to the Cloud Shell mounted storage. If using local PowerShell, open and navigate to the directory where you extracted the definitions.
1. Run the following commands:

```PowerShell - Set Sub ID
$subid = "/subscriptions/yourSubscriptionID"
```

```PowerShell - Storage Accounts
New-AzPolicyDefinition -Name "Security Baseline - Storage Accounts" -Description "Prevents creating a storage account that has access keys enabled" -Policy 'StorageAccounts-KeyAccess.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - Storage Accounts" 
New-AzPolicyAssignment -Name "Security Baseline - Storage Accounts" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - Cognitive Services
New-AzPolicyDefinition -Name "Security Baseline - Cognitive Services" -Description "Modifies a Cognitive Service account to disable local authentication" -Policy 'CognitiveServices.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - Cognitive Services" 
New-AzPolicyAssignment -Name "Security Baseline - Cognitive Services" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - SQL Servers
New-AzPolicyDefinition -Name "Security Baseline - SQL Servers" -Description "Prevents a SQL server being deployed with local authentication" -Policy 'SQLServers.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - SQL Servers" 
New-AzPolicyAssignment -Name "Security Baseline - SQL Servers" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - Event Hub Namespaces
New-AzPolicyDefinition -Name "Security Baseline - Event Hub Namespaces" -Description "Prevents Event Hub Namespaces being deployed with local authentication" -Policy 'EventHubNamespaces.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - Event Hub Namespaces" 
New-AzPolicyAssignment -Name "Security Baseline - Event Hub Namespaces" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - Service Bus Namespaces
New-AzPolicyDefinition -Name "Security Baseline - Service Bus Namespaces" -Description "Prevents Service Bus Namespaces being deployed with local authentication" -Policy 'ServiceBusNamespaces.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - Service Bus Namespaces" 
New-AzPolicyAssignment -Name "Security Baseline - Service Bus Namespaces" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - CosmosDB
New-AzPolicyDefinition -Name "Security Baseline - CosmosDB" -Description "Prevents CosmosDB being deployed with local authentication" -Policy 'CosmosDB.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - CosmosDB" 
New-AzPolicyAssignment -Name "Security Baseline - CosmosDB" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - App Configurations
New-AzPolicyDefinition -Name "Security Baseline - App Configurations" -Description "Prevents App Configurations being deployed with local authentication" -Policy 'AppConfig.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - App Configurations" 
New-AzPolicyAssignment -Name "Security Baseline - App Configurations" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - IoT Hubs
New-AzPolicyDefinition -Name "Security Baseline - IoT Hubs" -Description "Prevents IoT Hubs being deployed with local authentication" -Policy 'IoTHubs.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - IoT Hubs" 
New-AzPolicyAssignment -Name "Security Baseline - IoT Hubs" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - Event Grid Topics
New-AzPolicyDefinition -Name "Security Baseline - Event Grid Topics" -Description "Prevents Event Grid Topics being deployed with local authentication" -Policy 'EventGrids.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - Event Grid Topics" 
New-AzPolicyAssignment -Name "Security Baseline - Event Grid Topics" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - Automation Accounts
New-AzPolicyDefinition -Name "Security Baseline - Automation Accounts" -Description "Prevents Automation Accounts being deployed with local authentication" -Policy 'AutomationAccounts.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - Automation Accounts" 
New-AzPolicyAssignment -Name "Security Baseline - Automation Accounts" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - SignalR
New-AzPolicyDefinition -Name "Security Baseline - SignalR" -Description "Prevents SignalR being deployed with local authentication" -Policy 'SignalR.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - SignalR" 
New-AzPolicyAssignment -Name "Security Baseline - SignalR" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - Container Registries
New-AzPolicyDefinition -Name "Security Baseline - Container Registries" -Description "Prevents Container Registries being deployed with local authentication" -Policy 'ContainerRegistries.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - Container Registries" 
New-AzPolicyAssignment -Name "Security Baseline - Container Registries" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - AKS Clusters
New-AzPolicyDefinition -Name "Security Baseline - AKS Clusters" -Description "Prevents AKS Clusters being deployed with local authentication" -Policy 'AKS.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - AKS Clusters" 
New-AzPolicyAssignment -Name "Security Baseline - AKS Clusters" -PolicyDefinition $policy -Scope $subid
```

```PowerShell - API Management
New-AzPolicyDefinition -Name "Security Baseline - API Management" -Description "Prevents API Management being deployed with local authentication" -Policy 'APIM.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - API Management" 
New-AzPolicyAssignment -Name "Security Baseline - API Management" -PolicyDefinition $policy -Scope $subid
```
> **Note**: The API Management policy is currently an Audit only policy and does not prevent deployment with a local account.

```PowerShell - AFD SKUs
New-AzPolicyDefinition -Name "Security Baseline - AFD SKU" -Description "Prevents non-premium SKUs of Azure Front Door" -Policy 'AFDSku.json'
$policy = Get-AzPolicyDefinition -Name "Security Baseline - AFD SKU" 
New-AzPolicyAssignment -Name "Security Baseline - AFD SKU" -PolicyDefinition $policy -Scope $subid
```

## Known impacts
The following are known impacts to how to deploy resources.

1. Cognitive Services - Local auth is not a configurable option for all AI services when deploying with the Azure portal. By enforcing the policy, you would have to deploy the resource by using a different method.
1. App Configuration - This operates a little differently than the rest of the services. Rather than denying your deployment, the Azure portal will automatically unselect the access keys checkbox during the UI steps.
1. Automation Accounts - They "appear" to pass validation in the Azure portal on the Review + Create screen, however when clicking create is when it fails due to policy. Additionally, the portal UI does not have the option to disable local authentication; deploy the resource by using a different method.
1. Container Registries - The Azure portal UI does not have the option to disable the local user account during deployment; use another method so that you can mark it disabled.
1. Azure Front Door SKUs - The Azure portal will say "Validation passed" but then fail when you select Create. 

## Future updates
These items are identified for future updates... please consider contributing:

1. Turn individual policy assignments into an initiative with deployment script
1. AFD WAF policy config that includes Bot Manager ruleset and Global Rate Limit custom rule
1. VMs and VMSS policy to enable automatic OS updates
1. Investigate whether the APIM policy can be changed to deny instead of audit.

## Warranty
> The policies, scripts, and other artifacts in this repo are provided AS-IS AND WITHOUT WARRANTY.