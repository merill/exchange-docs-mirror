---
layout: Conceptual
title: Recover a deleted public folder mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/recover-deleted-public-folder-mailbox
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
ms.author: serdars
ms.topic: how-to
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: b293b7e5-f9f7-4322-8d56-e30c75af6845
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
description: "Summary: This article describes how to recover a public folder mailbox in Microsoft 365 or Office 365 that was previously soft-deleted, meaning the mailbox retention period hasn't yet elapsed and the recycle bin hasn't been purged."
audience: ITPro
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 0270eaa2-a997-c320-f21a-e190bb7ce2ef
document_version_independent_id: ecfd33e4-23c7-e84c-d34c-3358d7cf4c5e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/recover-deleted-public-folder-mailbox.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/recover-deleted-public-folder-mailbox
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/recover-deleted-public-folder-mailbox.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: cfdd1000-2974-cabb-58ff-77b1b678be0f
---

# Recover a deleted public folder mailbox in Exchange Online | Microsoft Learn

**Summary**: This article describes how to recover a public folder mailbox in Microsoft 365 or Office 365 that was previously soft-deleted, meaning the mailbox retention period hasn't yet elapsed and the recycle bin hasn't been purged.

You can delete public folder mailboxes either in the EAC or through the `Remove-Mailbox -PublicFolder` cmdlet. To delete a primary mailbox, all other mailboxes must be deleted first. After a mailbox is deleted, it will no longer be visible in the EAC.

Deleted Public Folder mailboxes are recoverable for a period of up to 90 days.

## What do you need to know before you begin?

- Estimated time to complete: 5-10 minutes.
- A public folder mailbox can only be deleted once all folders within that mailbox have been deleted. However, you can bypass this restriction by using the `-Force` switch, as in `Remove-Mailbox -PublicFolder -Force`.
- A deleted public folder mailbox is only recoverable for a period of 90 days after the mailbox is soft-deleted. The retention period for a soft-deleted mailbox is 90 days, after which the mailbox is permanently deleted and you won't be able to restore it.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Note

For deleted public folder mailboxes that contain folders, the folders will be automatically recovered along with the mailbox that contains them when you use one of the following procedures to recover the mailbox.

## Restore a primary mailbox

To restore a primary public folder mailbox:

1. Type the following command to find the soft-deleted mailbox:

    ```PowerShell
    Get-Mailbox -PublicFolder -SoftDeletedMailbox
    ```
2. Type the following command to restore the chosen mailbox:

    ```PowerShell
     Undo-SoftDeletedMailbox -PublicFolder
    ```

## Restore a primary mailbox and secondary mailboxes

The **Type** field, part of the information returned by the `Get-Mailbox` cmdlet, identifies public folder mailboxes as either **Primary** or **Secondary**. Primary public folder mailboxes must be restored first.

Perform the following steps to restore both a primary public folder mailbox and any relevant secondary mailboxes.

1. Type the following command to find the soft-deleted mailboxes:

    ```PowerShell
    Get-Mailbox -PublicFolder -SoftDeletedMailbox
    ```
2. Type the following command to restore the primary mailbox:

    ```PowerShell
    Undo-SoftDeletedMailbox -PublicFolder
    ```
3. Type the following for each secondary public folder mailbox that you want to restore (once per mailbox).

    ```PowerShell
    Undo-SoftDeletedMailbox -PublicFolder
    ```

## Restore secondary mailboxes

Use this procedure if you want to restore one or more secondary public folder mailboxes that were soft-deleted, and the primary mailbox still exists within your organization.

1. Type the following command to find the soft-deleted mailboxes:

    ```PowerShell
    Get-Mailbox -PublicFolder -SoftDeletedMailbox
    ```

    You'll be able to distinguish primary from secondary public folder mailboxes by the information in the **Type** field.
2. Type the following for each secondary public folder mailbox that you want to restore (once per mailbox).

    ```PowerShell
    Undo-SoftDeletedMailbox -PublicFolder
    ```

Note

If a primary public folder has been deleted from an organization, any secondary mailbox associated with it can't be restored.