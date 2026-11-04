---
layout: Conceptual
title: Hybrid management in Exchange hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-management
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: install-set-up-deploy
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
ms.assetid: 233f9f34-3ff5-47e1-a9e8-3244ee868d6e
ms.reviewer: 
description: "When you install an Exchange server, the Exchange management tools are automatically installed on the server. You'll use the following tools to configure and manage both the on-premises Exchange and the Exchange Online organization:"
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 3f04cfb3-566e-a54d-b9ff-7e0a3a3ca7a8
document_version_independent_id: 8e8f96fb-3f69-2be4-11c4-eed3f7ed11a2
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-management.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 0a3605ac-d9e8-b1ce-5f50-4bfa6ac9347b
---

# Hybrid management in Exchange hybrid deployments | Microsoft Learn

When you install an Exchange server, the Exchange management tools are automatically installed on the server. You'll use the following tools to configure and manage both the on-premises Exchange and the Exchange Online organization:

- **Exchange admin center**: The EAC is a web-based management console that allows for ease of use and is optimized for on-premises, online, or hybrid Exchange deployments. The EAC replaces the Exchange Management Console (EMC) and the Exchange Control Panel (ECP), which were the interfaces used to manage Exchange Server 2010.
- **Exchange Management Shell**: The Exchange Management Shell is a Windows PowerShell-based command line interface.

## The Exchange admin center

The EAC enables you to perform many deployment tasks and most common day-to-day administrative tasks on both the on-premises Exchange servers and the Exchange Online organization. It's installed by default on every Exchange 2013 or newer server. In addition, because it's a web-based management console, you can also access it by using a web browser on other computers in your network or via the Internet by using the ECP virtual directory URL.

You access the Exchange Online organization in the EAC by selecting the Office 365 tab. If you've configured a hybrid deployment, selecting the Office 365 tab allows you to open the Exchange admin center of Exchange Online organization in new browser tab. If you don't have an Exchange Online organization, selecting the Office 365 link will direct you to the Microsoft 365 and Office 365 sign-up page.

For more information about the EAC, see [Exchange admin center](architecture/client-access/exchange-admin-center).

## The Exchange Management Shell

The Exchange Management Shell enables you to perform any task that the EAC does and some additional tasks that can only be performed in the Exchange Management Shell. The Exchange Management Shell is a collection of Windows PowerShell scripts and cmdlets that are installed on a computer when the Exchange management tools are installed. These scripts and cmdlets are only loaded when you open the Exchange Management Shell using the Exchange Management Shell icon. If you open Windows PowerShell directly, the Exchange scripts and cmdlets aren't loaded and you won't be able to manage your on-premises organization.

Note

You can create a manual Windows PowerShell connection to your local on-premises organization, similar to how you manually connect to the Exchange Online organization below. However, we strongly recommend that you use the Exchange Management Shell icon to open the Exchange Management Shell to manage your on-premises Exchange servers.

When you open the Exchange Management Shell using the Exchange Management Shell icon on a computer that has the management tools installed, you can manage your on-premises organization. However, you can't manage the Exchange Online organization when you open the Exchange Management Shell using this icon. This is because opening the Exchange Management Shell using the Exchange Management Shell icon automatically connects you to a local Exchange server.

If you want to manage the Exchange Online organization using Windows PowerShell, you must open Windows PowerShell directly and not via the Exchange Management Shell icon. When you open Windows PowerShell, you can then manually specify where you want to connect. When you create a manual connection, you specify an administrator account in the Microsoft 365 or Office 365 organization, and then you run a command to create a connection. When the connection is established, the Exchange cmdlets you have permissions to run are made available to you. Learn more at [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

If you're new to the Exchange Management Shell and want to learn the basics about how the Exchange Management Shell works, command syntax, and more, see [Exchange Management Shell](/en-us/powershell/exchange/exchange-management-shell).