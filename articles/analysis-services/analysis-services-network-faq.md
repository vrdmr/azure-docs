---
title: Frequently asked questions about Analysis Services network connectivity | Microsoft Docs
description: This article provides answers to some of the more common questions about Analysis Services network connectivity.
author: minewiskan
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 04/29/2020
ms.author: owend
ms.reviewer: minewiskan
---

# Frequently asked questions about Analysis Services network connectivity

This article provides answers to common questions about connecting to storage accounts, data sources, firewalls, and IP addresses.

## Backup and restore

**Question** - How can I backup and restore using a storage account that is behind a firewall?   
**Answer** - Azure Analysis Services does not use fixed IP addresses or Service Tags. The range of IP addresses your Analysis Services servers use can be anything in the range of IP addresses for the *Azure region*. Because your server IP addresses are variable and can change over time, your firewall rules need to allow for the entire range of Azure region IP addresses your server is in.

**Question** - My Azure storage account is in a different region from my Analysis Services server. How do I configure storage account firewall settings?   
**Answer** - If the storage account is in a different region, firewall settings must be configured to allow access from **All networks**. Firewall settings configured for Selected networks with whitelisted IP addresses and Allow trusted Microsoft services exception is not supported.

## Data source connections

**Question** - I have a VNET for my data source system. How can I allow my Analysis Services servers to access the database from the VNET?   
**Answer** - Azure Analysis Services is unable to join a VNET. The best solution here is to install and configure an On-premises Data Gateway on the VNET, and then configure your Analysis Services servers with the **AlwaysUseGateway** server property. To learn more, see [Use gateway for data sources on an Azure Virtual Network (VNet)](analysis-services-vnet-gateway.md).

**Question** - I have a source database behind a firewall. How can I configure the firewall to allow my Analysis Services server to access it?   
**Answer** - Azure Analysis Services does not use fixed IP addresses or Service Tags. The range of IP addresses your Analysis Services servers use can be anything in the range of IP addresses for the *Azure region*. You  have to provide the *full range* of IP addresses for the Azure region of your server in the source database firewall rules. Another, and possibly more secure, alternative is to configure an On-premises Data Gateway. You can then configure your Analysis Services servers with the [AlwaysUseGateway server property](analysis-services-vnet-gateway.md#configure-alwaysusegateway-property), and then ensure the On-premises Data Gateway has an IP address allowed by the firewall rules of the data source.

## Azure apps with IP address

**Question** - I use an Azure-based application (for example, Azure Functions, Azure Data Factory) with an IP address that changes on the fly. How can I manage the Azure Analysis Services firewall rules to dynamically allow the IP address where my app is executing?   
**Answer** - Azure Analysis Services does not support Private Links, VNETs, or Service Tags. There are some open-source solutions (for example, https://github.com/mathwro/Scripts/blob/master/Azure/AllowAzure-AnalysisServer.ps1) that detect the IP address of the client application, and automatically and temporarily update the firewall rules.


## Next steps

[Install and configure an on-premises data gateway](analysis-services-gateway-install.md)   
[Connecting to on-premises data sources with On-premises data gateway](analysis-services-gateway.md)   
[Use gateway for data sources on an Azure Virtual Network (VNet)](analysis-services-vnet-gateway.md)
