---
layout: Conceptual
title: View statistics for public folders and public folder items in Exchange Online' in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/view-public-folder-statistics
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
description: This topic explains how to retrieve statistics about a public folder, such as the display name, creation time, last user modified time, last user access, and item size. You can use this information to make decisions about deleting or retaining public folders.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 4e412710-9a74-4649-ab01-502e969a7eda
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
document_id: 845109c5-1606-c9dc-b583-b846f3ba3663
document_version_independent_id: 63763f81-2a12-906a-b504-e4c7b1b9f5ee
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/view-public-folder-statistics.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/view-public-folder-statistics
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/view-public-folder-statistics.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: f3b1aebe-230d-2e3e-6dc9-d7265b4ecdbc
---

# View statistics for public folders and public folder items in Exchange Online' in Exchange Online | Microsoft Learn

This topic explains how to retrieve statistics about a public folder, such as the display name, creation time, last user modified time, last user access, and item size. You can use this information to make decisions about deleting or retaining public folders.

Note

In the Exchange admin center (EAC), you can view some of the quota and usage information for public folders by navigating to **Public Folders** &gt; **Edit**![Edit icon.](../../exchangeonline/media/itpro_eac_editicon.gif) &gt; **Mailbox usage**. However, this information is incomplete, and we recommend that you use Exchange Online PowerShell to view public folder statistics.

## What do you need to know before you begin?

- Estimated time to complete: 1 minute.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- You can't use the EAC to retrieve public folder statistics.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to retrieve public folder statistics

This example returns the statistics for the public folder Marketing with a piped command to format the list.

```PowerShell
Get-PublicFolderStatistics -Identity \Marketing | Format-List
```

Note

The value for the *Identity* parameter must include the path to the public folder. For example, if the public folder Marketing existed under the parent folder Business, you would provide the following value: `\Business\Marketing`

For detailed syntax and parameter information, see [Get-PublicFolderStatistics](/en-us/powershell/module/exchangepowershell/get-publicfolderstatistics).

## Use Exchange Online PowerShell to view statistics for public folder items

You can view the following information about items within a public folder:

- Type of item
- Subject
- Last user modification time
- Last user access time
- Creation time
- Attachments
- Message size

You can use this information to make decisions about what actions to take for your public folders, such as which public folders to delete. For example, you may want to delete a public folder if the items haven't been accessed for over two years, or you may want to convert a public folder that's being used as a document repository to another client access application.

This example returns default statistics for all items in the public folder Pamphlets under the path \Marketing\2013. Default information includes item identity, creation time, and subject.

```PowerShell
Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"
```

This example returns additional information about the items within the public folder Pamphlets, such as subject, last modification time, creation time, attachments, message size, and the type of item. It also includes a piped command to format the list.

```PowerShell
Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List
```

For detailed syntax and parameter information, see [Get-PublicFolderItemStatistics](/en-us/powershell/module/exchangepowershell/get-publicfolderitemstatistics).

## Use Exchange Online PowerShell to export the output of the Get-PublicFolderItemStatistics cmdlet to a .csv file

This example exports the output of the cmdlet to the PFItemStats.csv file that includes the following information for all items within the public folder \Marketing\Reports:

- Subject of the message ( `Subject`)
- Date and time that the item was last modified ( `LastModificationTime`)
- Whether the item has attachments ( `HasAttachments`)
- Type of item ( `ItemType)`
- Size of the item ( `MessageSize`)

```PowerShell
Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv
```

For detailed syntax and parameter information, see [Get-PublicFolderItemStatistics](/en-us/powershell/module/exchangepowershell/get-publicfolderitemstatistics).