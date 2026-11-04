---
layout: Conceptual
title: Restore deleted items from public folder in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/restore-deleted-items-from-public-folder
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.author: serdars
ms.topic: how-to
author: Benny-54
ms.service: outlook
ms.reviewer: 
ms.collection:
- exchange-online
description: Restore deleted items of public folder from the recycle bin of public folder.
audience: ITPro
f1.keywords:
- NOCSH
ms.date: 2021-01-29T00:00:00.0000000Z
locale: en-us
document_id: 8c860e4c-6407-06dd-0f52-045c4c7ccfbb
document_version_independent_id: 97516db0-b624-2911-61da-a765dd1c4f70
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/restore-deleted-items-from-public-folder.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/restore-deleted-items-from-public-folder
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/restore-deleted-items-from-public-folder.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: a6e94fb6-52fa-aa85-eed2-afe70a48f5b5
---

# Restore deleted items from public folder in Exchange Online | Microsoft Learn

The items deleted from public folders are stored in the recoverable items (dumpster) of public folder until the retention period is over.

## Permissions required

The user restoring items from the public folder must have at least the `Author` public folder client permission assigned. For more information on public folder client permissions, see [Add-PublicFolderClientPermission](/en-us/powershell/module/exchangepowershell/add-publicfolderclientpermission).

## Restore deleted items from public folder

1. In outlook, under **Public Folders**, select the folder from which items were deleted, and click **Recover Deleted Items**.

    ![recover deleted items.](../../exchangeonline/media/restore-pf-imag1.png)
2. Select the item to be restored, ensure **Restore Selected Items** option is selected and click **Ok**.

    ![restore selected items.](../../exchangeonline/media/restore-pf-imag2.png)
3. The item is restored.

    ![restored.](../../exchangeonline/media/restore-pf-imag3.png)

Note

To enable the **Recover Deleted Items** option for non-mail type (for example: Calendar, Contact, Tasks) of public folders, see [Can't recover deleted items from a non-mail public folder](/en-us/outlook/troubleshoot/user-interface/cannot-recover-deleted-items-from-non-mail-public-folder).