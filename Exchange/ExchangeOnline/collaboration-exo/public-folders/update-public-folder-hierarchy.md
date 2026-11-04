---
layout: Conceptual
title: Update the public folder hierarchy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/update-public-folder-hierarchy
Manager: serdars
ms.subservice: exo-groups
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.custom:
- has-azure-ad-ps-ref
description: You only need to update the public folder hierarchy if you want to manually invoke the hierarchy synchronizer and the mailbox assistant. Both these are invoked at least once every 24 hours for each public folder mailbox in the organization. The hierarchy synchronizer is invoked every 15 minutes if any users are logged on to a secondary mailbox through Microsoft Outlook or a Microsoft Exchange Web Services client.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 09692d91-7cd5-7c05-0c0b-72cc7f74b338
document_version_independent_id: 146a8a57-6685-968b-103f-5e92f9e19240
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/update-public-folder-hierarchy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/update-public-folder-hierarchy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/update-public-folder-hierarchy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/390894b2-8646-4f7e-b8cd-2209156272a9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/12b23b77-ab37-4318-a036-4f6690586386
platformId: a1ccbd2d-dd5a-474f-564c-f2827e75395f
---

# Update the public folder hierarchy in Exchange Online | Microsoft Learn

You only need to update the public folder hierarchy if you want to manually invoke the hierarchy synchronizer and the mailbox assistant. Both these are invoked at least once every 24 hours for each public folder mailbox in the organization. The hierarchy synchronizer is invoked every 15 minutes if any users are logged on to a secondary mailbox through Microsoft Outlook or a Microsoft Exchange Web Services client.

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- You can't perform this procedure in the EAC. You must use Exchange Online PowerShell.
- We recommend that when you run this command with the *InvokeSynchronizer* parameter, you use the *SuppressStatus* parameter. If you don't use this parameter in the command, the output will display status messages every 3 seconds for up to one minute. Until the minute passes, you can't use that instance of Exchange Online PowerShell.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Update the public folder hierarchy

This example updates the public folder hierarchy on the public folder mailbox PF\_marketing and suppresses the command's output.

```PowerShell
Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus
```

This example updates all public folder mailboxes and suppresses the command's output.

```PowerShell
Get-Mailbox -PublicFolder | Update-PublicFolderMailbox -InvokeSynchronizer -SuppressStatus
```