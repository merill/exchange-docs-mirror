---
layout: Conceptual
title: Remove completed migration batches | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/remove-completed-migration-batches
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
audience: ITPro
ms.topic: upgrade-and-migration-article
f1.keywords:
- CSH
ms.custom:
- O365E_HRCMoveRequest_FL312271
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
- M365-email-calendar
ms.assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms.reviewer: 
description: This article describes the steps by which you can remove a completed migration batch.
ms.date: 2024-10-03T00:00:00.0000000Z
locale: en-us
document_id: 0976231e-ce9a-1c0c-a30a-248b3519caba
document_version_independent_id: b50060be-3868-6885-5953-e8c5a28625df
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/remove-completed-migration-batches.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/remove-completed-migration-batches
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/remove-completed-migration-batches.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: 031d1320-5a80-d86d-d7f3-951e73936efc
---

# Remove completed migration batches | Microsoft Learn

After the "mailbox moves" process has been completed, we recommend removing the completed migration batches to minimize the likelihood of errors if the same users are moved again.

You can remove a migration batch using the following methods:

- EAC
- PowerShell

## EAC

To remove a completed migration batch using EAC (Exchange Online EAC or on-premises EAC), perform the following steps:

1. Go to **Home** &gt; **Migration**. The **Migration batches** page appears.
2. Select a completed migration batch that has the value **Completed** under the column titled **Status**. The dialog containing the details of the migration batch displays.
3. Select the **Delete** icon on the dialog. A prompt displays, seeking confirmation of whether the user wants to delete the migration batch.
4. Select **Confirm**. A notification message that reads **Operation successful** is displayed, indicating that the migration batch has been successfully deleted.

## PowerShell

For information on how to delete a migration batch using PowerShell, see [Remove-MigrationBatch](/en-us/powershell/module/exchangepowershell/remove-migrationbatch).