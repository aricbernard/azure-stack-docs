---
title: Disable-AksHciArcConnection
author: jessicaguan
description: The Disable-AksHciArcConnection PowerShell command disables the Arc connection on an AKS on Azure Stack HCI cluster.
ms.topic: reference
ms.date: 04/12/2021
ms.author: jeguan
---

# Disable-AksHciArcConnection

## Synopsis
Disables Arc connection on an AKS on Azure Stack HCI cluster.

## Syntax

```powershell
Disable-AksHciArcConnection -name <String> 
                            -tenantId <String>
                            -subscriptionId <String> 
                            -resourceGroup <String>
                            -credential <PSCredential>
                            -location <String>
```

## Description
Disables Arc connection an AKS on Azure Stack HCI cluster.

## Examples

### Disconnect an AKS on Azure Stack HCI cluster to Azure Arc for Kubernetes using Azure user login 
This command disconnects your workload cluster from Azure Arc using the subscription ID and resource group passed in the `Set-AksHciRegistration` command while registering the AKS host for billing. Make sure that you have access to the subscription on an "Owner" or "Contributor" role. You can check your access level by navigating to your subscription, clicking on "Access control (IAM)" on the left hand side of the Azure portal and then clicking on "View my access". If you have multiple tenants on your Azure account, it is recommended to disconnect your workload cluster to Arc using a service principal.

```PowerShell
Connect-AzAccount
Disable-AksHciArcConnection -name "myCluster"
```
If you do not have the right access to the subscription on which your AKS host was registered, but do have access to a different subscription on which you're an "Owner" or "Contributor", you can use the following command. You must pass in a location if the location of the Arc connected cluster is different from the location of the resource group. 

```PowerShell
Connect-AzAccount
Disable-AksHciArcConnection -name "myCluster" -subscriptionId "3000e2af-000-46d9-0000-4bdb12000000" -resourceGroup "myAzureResourceGroup"
```

### Disconnect an AKS on Azure Stack HCI cluster to Azure Arc for Kubernetes using a service principal
If you have multiple tenants on your Azure account, or if you do not have access to a subscription on which you're an "Owner" or "Contributor", it is recommended to connect your workload cluster to Arc using a service principal.

The first command prompts for service principal credentials and stores them in the $Credential variable. Enter your application ID for the username and service principal secret as the password when prompted. Make sure you get these values from your subscription admin. The second command connects the specified Azure tenant using the service principal credentials stored in the $Credential variable. 

```powershell
$Credential = Get-Credential
Disable-AksHciArcConnection -name "myCluster" -subscriptionId "3000e2af-000-46d9-0000-4bdb12000000" -resourceGroup "myAzureResourceGroup" -credential $Credential -tenantId "xxxx-xxxx-xxxx-xxxx"
```

Make sure the service principal used in the command above has the "Owner" or "Contributor" role assigned to it and that it has scope over the subscription ID and resource group used in the command. For more information on service principals, visit [creating service principals with Azure PowerShell](https://docs.microsoft.com/powershell/azure/create-azure-service-principal-azureps?view=azps-5.9.0#create-a-service-principal)


## Parameters

### -Name
The alphanumeric name of your AKS cluster.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```
### -tenantId
The tenant ID of your Azure service principal. Default value is the Azure login context.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -subscriptionId
Your Azure account's subscription ID. Default value is the subscription ID passed in `Set-AksHciRegistration`.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -resourceGroup
The name of the Azure resource group. Default value is the resource group passed in `Set-AksHciRegistration`.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -credential
The credential for the Azure service principal.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -location
The location or Azure region of your Azure resource. Default value is the location passed in `Set-AksHciRegistration`.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: Azure resource group's location
Accept pipeline input: False
Accept wildcard characters: False
```