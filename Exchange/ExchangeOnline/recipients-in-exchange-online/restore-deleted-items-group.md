---
layout: Conceptual
title: Restore deleted email conversations from Microsoft 365 Groups | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/restore-deleted-items-group
Manager: Serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: Benny-54
audience: ITPro
f1.keywords: 
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: 
ms.collection: 
ms.custom: 
description: Learn how to restore deleted items from Microsoft Group.
ms.date: 2023-05-14T00:00:00.0000000Z
locale: en-us
document_id: 54e82104-829f-d66b-2833-0c106875f752
document_version_independent_id: c5464236-1a57-9641-3592-7c8f27c6bb3a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/restore-deleted-items-group.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/restore-deleted-items-group
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/restore-deleted-items-group.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 40e61732-2edb-b7b9-f631-aa1f7fbb5070
---

# Restore deleted email conversations from Microsoft 365 Groups | Microsoft Learn

If you have accidentally deleted any email conversations from Microsoft 365 Group and are looking for a way to restore the email conversation, you can restore them using one of the following options:

- Restore deleted items from OWA
- Use `Restore-RecoverableItems` command

## Restore the deleted items from Outlook Web Application (OWA)

**Prerequisite**:

- Ensure [Folders and Rules feature for Microsoft 365 groups](/en-us/microsoft-365/enterprise/manage-folders-and-rules-feature) is enabled.
- Ensure you're the owner of the group to and from which you're trying to restore the deleted items.

1. Sign in to OWA.
2. Select the Microsoft 365 Group.
3. If **Deleted Items** folder isn't visible, right click on the group, and select **Create new subfolder** option.
4. Enter the name of the folder, and select **Save** to create a folder.

    You can expand the group now and see the **Deleted Items** folder along with the new folder you created.
5. Select the **Deleted Items** folder, select the messages that need to be restored, and select **Restore**.

    ![restored-item-in-outlook](../exchangeonline/media/restored-deleted-item-group.jpg)

    The messages are restored under **Inbox** folder of the Microsoft 365 group.

## Use Restore-RecoverableItems command

If the deleted messages aren't present under **Deleted Items** folder, do the following:

Prerequisite:

- Ensure you're a tenant admin to use this command.

    1. Sign in to EXO PowerShell.
    2. Use the following command to restore all emails from `RecoverableItems` folder to **Inbox**:

    ```PowerShell
    Restore-RecoverableItems -Identity <M365GroupEmailAddress>
    ```

You can further filter the message to be restored by using various options mentioned in [`Restore-RecoverableItems`](/en-us/powershell/module/exchangepowershell/restore-recoverableitems).

For example:

![example-of-the-command-to-restore](../exchangeonline/media/example-restored-items.png)

## Related article

[Restore a deleted Microsoft 365 group](/en-us/microsoft-365/admin/create-groups/restore-deleted-group)