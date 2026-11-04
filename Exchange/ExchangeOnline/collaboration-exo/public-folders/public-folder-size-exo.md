---
layout: Conceptual
title: Public folder size in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/public-folder-size-exo
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
description: Learn how to manage Public folder size in Exchange Online
ms.topic: article
author: serdars
ms.author: serdars
ms.assetid: c0c561cb-3d25-4a26-b94a-ba3876c49fbf
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-04-16T00:00:00.0000000Z
locale: en-us
document_id: edf1897c-07ae-cef2-831c-e9d3932105cc
document_version_independent_id: 77c44fce-f473-e134-6a0a-ae23967b94fd
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/public-folder-size-exo.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/public-folder-size-exo
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/public-folder-size-exo.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 4f00d8c2-d7ab-0f6b-db54-7dda5433d6cd
---

# Public folder size in Exchange Online | Microsoft Learn

A public folder is stored inside public folder mailbox in Exchange Online. So, the quota of public folder is governed by "quota of public folders" and "quota of public folder mailbox" in which they reside.

## Quotas for public folder mailbox

The types of quotas that govern a public folder mailbox are as follows:

- Public folder mailbox quota
- RecoverableItemsQuota

### Public folder mailbox quota

Exchange Online has a limit of 100 GB per public folder mailbox and you can have up to 1000 public folder mailboxes.

You can view the individual public folder mailbox quota using:

- Exchange Admin Center (EAC), and
- Exchange Online PowerShell

#### Exchange Admin Center (EAC)

1. Sign in to [Exchange admin center (EAC)](https://admin.exchange.microsoft.com/) with the credentials of a tenant administrator or of a user who has the "public folders" role assigned to them.
2. Choose **Public Folders &gt; Public folder mailboxes**.
3. Select **PF mailbox**. The page displaying mailbox usage and maximum quota for a public folder mailbox appears.

[![Screenshot that shows the page displaying the mailbox usage and maximum quota for a public folder mailbox.](../../exchangeonline/media/mailbox-usage-maximum-quota.png)](../../exchangeonline/media/mailbox-usage-maximum-quota.png#lightbox)

#### Exchange Online PowerShell

1. To view the individual public folder mailbox quota using PowerShell, run the following command:

    ```powershell
       Get-Mailbox -PublicFolder pubmbx2 | fl IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota
    ```

    [![Screenshot that shows the CLI command interface that enables you to view the size of the public folder mailbox.](../../exchangeonline/media/size-of-one-public-folder-mailbox.png)](../../exchangeonline/media/size-of-one-public-folder-mailbox.png#lightbox)
2. To view how much space has been occupied currently within the public folder mailbox, run the following command:

    `Get-MailboxStatistics pubmbx2 | fl TotalItemSize`

    Note

    This command works only if public folder deployment is active in Exchange Online, that is, the public folder size cannot be viewed if there's migration in progress.

    [![Screenshot that shows the CLI command interface that enables you to view the space occupied currently within the public folder mailbox.](../../exchangeonline/media/space-occupied-currently-public-folder-mailbox.png)](../../exchangeonline/media/space-occupied-currently-public-folder-mailbox.png#lightbox)

### RecoverableItemsQuota

There's another quota named **RecoverableItemsQuota** on each public folder mailbox. The deleted public folders or public folder items make up this quota.

Note

You can view the **RecoverableItemsQuota** only through Exchange Online PowerShell.

1. Run the following command to view the **RecoverableItemsQuota**:

    ```powershell
       Get-Mailbox -PublicFolder pubmbx2 | fl RecoverableItemsWarningQuota,RecoverableItemsQuota
    ```

    The following screenshot is an example of the **RecoverableItemsQuota** data:

    [![Screenshot that shows the output of **RecoverableItemsQuota**.](../../exchangeonline/media/recoverable-items-quota.png)](../../exchangeonline/media/recoverable-items-quota.png#lightbox)
2. Run the following command to view the data regarding the size occupied by deleted public folders/public folder items:

    `Get-MailboxStatistics pubmbx2 | fl TotalDeletedItemSize`

    [![Screenshot that shows the output regarding the size occupied by deleted public folders/public folder items.](../../exchangeonline/media/size-deleted-items.png)](../../exchangeonline/media/size-deleted-items.png#lightbox)

    The regular maintenance purges the deleted public folders/items once the retention period is over. If the **TotalDeletedItemSize** reaches or exceeds the **RecoverableItemsQuota**, users can't delete items from public folders. They'll see an error, or the deleted item reappears in the original folder. For information on how to troubleshoot this issue, see [Can't delete items from public folder in Outlook on the web](/en-us/exchange/troubleshoot/public-folders/cannot-delete-items-public-folder).

## Public folder size

Each individual public folder has a size limit assigned to it. In Exchange Online, the default public folder size is limited to 2 GB, which is controlled by **DefaultPublicFolderIssueWarningQuota** and **DefaultPublicFolderProhibitPostQuota** parameters at the organization level.

[![Screenshot that shows the data regarding the public folder size.](../../exchangeonline/media/public-folder-size.png)](../../exchangeonline/media/public-folder-size.png#lightbox)

### Check size and item count of individual public folder

You can check an individual public folder's size and its item count by using:

1. EAC
2. PowerShell

#### EAC

1. Sign in to [EAC](https://admin.exchange.microsoft.com/).
2. Select **Public Folders**.
3. Select the public folder for which you want to view its data such as its size, the number of items in it. A screen, with the **General** tab selected by default, is displayed. This screen shows data such as the total number of items in the chosen public folder and the size of the public folder.

    [![Screenshot that shows the data such as the item count and size of the public folder.](../../exchangeonline/media/display-size-item-count-of-public-folder.png)](../../exchangeonline/media/display-size-item-count-of-public-folder.png#lightbox)

#### PowerShell

To know the individual public folder size and the total number of items using PowerShell, run the following command:

`Get-PublicFolderStatistics \publicfolder1 | fl ItemCount,TotalItemSize`

[![Screenshot that shows the command interface triggered by running PowerShell, showing data such as the item count and size of the public folder.](../../exchangeonline/media/item-count-size-pf-powershell.png)](../../exchangeonline/media/item-count-size-pf-powershell.png#lightbox)

### Check size of total number of deleted items within individual public folder

Note

You can check the size of the total number of deleted items within the public folder only using Exchange Online PowerShell.

To check the size of the total number of deleted items within the public folder, run the following command:

`Get-PublicFolderStatistics \publicfolder1 | fl TotalDeletedItemSize`

[![Screenshot that shows the command interface triggered by running PowerShell, showing data such as the deleted items size.](../../exchangeonline/media/deleted-item-size-powershell.png)](../../exchangeonline/media/deleted-item-size-powershell.png#lightbox)

### Change quota of individual public folder

When the quota of an individual public folder is set to unlimited, the system applies organizational quota as the individual public folder's quota, as shown in the following screenshot:

[![Screenshot that shows the individual public folder's quota being set to unlimited.](../../exchangeonline/media/individual-pf-quota-unlimited.png)](../../exchangeonline/media/individual-pf-quota-unlimited.png#lightbox)

You can use the following methods to change the quota on an individual folder:

- EAC
- PowerShell

##### EAC

To change the quota of an individual public folder using the EAC, perform the following steps:

1. Sign in to [EAC](https://admin.exchange.microsoft.com/).
2. Select **Public Folders**.
3. Select the public folder for which you want to change the quota.
4. Select **Limits** tab. The page shown in the following screenshot appears:

    [![Screenshot that shows the basic permissions for a user role](../../exchangeonline/media/changing-quota-of-individual-pf-using-eac.png)](../../exchangeonline/media/changing-quota-of-individual-pf-using-eac.png#lightbox)
5. Uncheck the **Use organization quota defaults** checkbox.
6. Select **Manage storage quotas**.

We recommend keeping the size of an individual public folder to under 10 GB as larger public folders create issues during the auto-split process.

##### PowerShell

To change the quota of an individual public folder using PowerShell, run the following command:

`Set-PublicFolder \publicfolder1 -IssueWarningQuota 4.5GB -ProhibitPostQuota 5GB`