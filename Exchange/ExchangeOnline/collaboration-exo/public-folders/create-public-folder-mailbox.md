---
layout: Conceptual
title: Create a public folder mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/create-public-folder-mailbox
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
description: Before you can create a public folder, you must first create a public folder mailbox. Public folder mailboxes contain the hierarchy information plus the content for public folders. The first public folder mailbox you create will be the primary hierarchy mailbox, which contains the only writable copy of the hierarchy. Any additional public folder mailboxes you create will be secondary mailboxes, which contain a read-only copy of the hierarchy.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-09-09T00:00:00.0000000Z
locale: en-us
document_id: a2386c45-f822-3941-2946-bbc56c6d6fd5
document_version_independent_id: 0809b905-0fde-a231-895f-29429614f508
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/create-public-folder-mailbox.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/create-public-folder-mailbox
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/create-public-folder-mailbox.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 64a70e16-8608-e589-6640-4d8eedd53421
---

# Create a public folder mailbox in Exchange Online | Microsoft Learn

Before you can create a public folder, you must first create a public folder mailbox. Public folder mailboxes contain the hierarchy information plus the content for public folders. The first public folder mailbox you create will be the primary hierarchy mailbox, which contains the only writable copy of the hierarchy. Any additional public folder mailboxes you create will be secondary mailboxes, which contain a read-only copy of the hierarchy.

Note

For more information about the storage quotas and limits for public folders, see [Exchange Online Limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits).

For additional management tasks related to public folders in Exchange Online, see [Public folder procedures in Microsoft 365 or Office 365 and Exchange Online](public-folder-procedures).

## What do you need to know before you begin?

- Estimated time to complete: less than 5 minutes.
- Exchange Server public folders and public folders on legacy Exchange servers can't exist in the same organization. If you try to create a public folder mailbox when you still have legacy public folders, you'll receive the error **An existing Public Folder deployment has been detected. To migrate existing Public Folder data, create new Public Folder mailbox using -HoldForMigration switch.**

    Before you can create public folders in Exchange Server, you need to migrate your legacy public folders to Exchange Server. To do this, follow the steps in [Migrate Public Folders to Exchange 2013 From Previous Versions](/en-us/previous-versions/exchange-server/exchange-150/jj150486%28v=exchg.150%29) for legacy versions. For newer versions, follow [Use batch migration to migrate Exchange Server public folders to Exchange Online](../../collaboration/public-folders/migrate-to-exchange-online). These steps will show you how to create a public folder mailbox that can be used to store your migrated public folders.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use the EAC to create a public folder mailbox

1. Go to **Public folders** &gt; **Public folder mailboxes**, and select **Add a public folder mailbox**.
2. Provide a **Name** for the public folder mailbox.
3. Select **Add**.

## Use Exchange Online PowerShell to create a public folder mailbox

This example creates the primary public folder mailbox.

```PowerShell
New-Mailbox -PublicFolder -Name MasterHierarchy
```

This example creates a secondary public folder mailbox. The only difference between creating the primary hierarchy mailbox and a secondary hierarchy mailbox is that the primary mailbox is the first one created in the organization. You can create additional public folder mailboxes for load balancing purposes.

```PowerShell
New-Mailbox -PublicFolder -Name Istanbul
```

For detailed syntax and parameter information, see [New-Mailbox](/en-us/powershell/module/exchangepowershell/new-mailbox).

## How do you know this worked?

To verify that you have successfully created the primary public folder mailbox, run the following command in Exchange Online PowerShell:

```PowerShell
Get-OrganizationConfig | Format-List RootPublicFolderMailbox
```

For detailed syntax and parameter information, see [Get-OrganizationConfig](/en-us/powershell/module/exchangepowershell/get-organizationconfig).