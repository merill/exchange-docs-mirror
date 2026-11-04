---
layout: Conceptual
title: Hybrid management in Exchange 2013/Exchange 2010 hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/exchange-2013-and-2010-hybrid/hybrid-management
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
ms.assetid: 613ad2c2-bb7a-4810-b572-71945bd103f1
ms.reviewer: 
description: "When you install a server running Microsoft Exchange Server 2013 in your Exchange 2010 on-premises organization, the Exchange 2013 management tools are automatically installed on the server. You'll use the following tools to configure and manage hybrid functionality for both the on-premises Exchange and the Exchange Online organization:"
ms.date: 2018-06-26T00:00:00.0000000Z
locale: en-us
document_id: daade52e-d3f3-215e-6a45-ac89d7d02e5a
document_version_independent_id: 856ca336-27bd-d33a-7472-e6bab44bcebb
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/exchange-2013-and-2010-hybrid/hybrid-management.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: exchange-2013-and-2010-hybrid/hybrid-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/exchange-2013-and-2010-hybrid/hybrid-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: e24179ff-e18b-b4c8-4076-46ae1346cd3f
---

# Hybrid management in Exchange 2013/Exchange 2010 hybrid deployments | Microsoft Learn

When you install a server running Microsoft Exchange Server 2013 in your Exchange 2010 on-premises organization, the Exchange 2013 management tools are automatically installed on the server. You'll use the following tools to configure and manage hybrid functionality for both the on-premises Exchange and the Exchange Online organization:

- **Exchange admin center**: The EAC is a web-based management console included with Exchange 2013 that's easy to use and is optimized for on-premises, online, or hybrid Exchange deployments. The EAC supplements the Exchange Management Console (EMC) and the Exchange Control Panel (ECP) interfaces that you use to manage Exchange Server 2010.
- **Exchange Management Shell**: The Exchange Management Shell is a Windows PowerShell-based command-line interface.

## The Exchange admin center

The EAC enables you to perform many deployment tasks and most common day-to-day administrative tasks on both the on-premises Exchange servers and the Exchange Online organization. It's installed by default on every Exchange 2013 server. In addition, because it's a web-based management console, you can also access it by using a web browser on other computers in your network or via the Internet by using the ECP virtual directory URL.

Important

If you want to access the EAC using an account with a mailbox located on an Exchange 2010 Mailbox server (such as a domain administrator account), you must use the following address in your browser to access the EAC: &gt; https://*&lt;FQDN of Exchange 2013 Client Access server&gt;*/ECP?ExchClientVer=15

You access the Exchange Online organization in the EAC by selecting the Office 365 cross-premises navigation tab. The cross-premises navigation allows you to easily switch between your Exchange Online and your on-premises Exchange organizations. If you've configured a hybrid deployment, selecting the tab allows you to manage the Exchange Online organization and recipient objects. If you don't have an Exchange Online organization, selecting the Office 365 link will direct you to the sign-up page.

For more information about the EAC, see [Exchange admin center in Exchange 2013](../exchange-admin-center-in-exchange-2013-exchange-2013-help).

## The Exchange Management Shell

The Exchange Management Shell enables you to perform any task that the EAC does and some additional tasks that can only be performed in the Exchange Management Shell. The Exchange Management Shell is a collection of Windows PowerShell scripts and cmdlets that are installed on a computer when the Exchange 2013 management tools are installed. These scripts and cmdlets are only loaded when you open the Exchange Management Shell using the Exchange Management Shell icon. If you open Windows PowerShell directly, the Exchange scripts and cmdlets aren't loaded and you won't be able to manage your on-premises organization.

Note

You can create a manual Windows PowerShell connection to your local on-premises organization, similar to how you manually connect to the Exchange Online organization below. However, we strongly recommend that you use the Exchange Management Shell icon to open the Exchange Management Shell to manage your on-premises Exchange servers.

When you open the Exchange Management Shell using the Exchange Management Shell icon on a computer that has the management tools installed, you can manage your on-premises organization. However, you can't manage the Exchange Online organization when you open the Exchange Management Shell using this icon. This is because opening the Exchange Management Shell using the Exchange Management Shell icon automatically connects you to a local Exchange server.

If you want to manage the Exchange Online organization using Windows PowerShell, you must open Windows PowerShell directly and not via the Exchange Management Shell icon. When you open Windows PowerShell, you can then manually specify where you want to connect. When you create a manual connection, you specify an administrator account in the Microsoft 365 or Office 365 organization, and then you run a command to create a connection. When the connection is established, the Exchange cmdlets you have permissions to run are made available to you. Learn more at [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

If you're new to the Exchange Management Shell and want to learn the basics about how the Exchange Management Shell works, command syntax, and more, see [Exchange Management Shell](/en-us/powershell/exchange/exchange-management-shell).