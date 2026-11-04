---
layout: Conceptual
title: Create a public folder in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/create-public-folder
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
description: Public folders are designed for shared access and provide an easy and effective way to collect, organize, and share information with other people in your workgroup or organization.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms.reviewer: 
f1.keywords:
- CSH
ms.custom:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
- has-azure-ad-ps-ref
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-09-09T00:00:00.0000000Z
locale: en-us
document_id: df710546-0b34-fa69-ab77-71c39d79b430
document_version_independent_id: 29f63d53-77b5-e67b-9228-ec8912724297
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/create-public-folder.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/create-public-folder
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/create-public-folder.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 48d04d47-0773-a5e9-85c8-8465b47450f0
---

# Create a public folder in Exchange Online | Microsoft Learn

Public folders are designed for shared access and provide an easy and effective way to collect, organize, and share information with other people in your workgroup or organization.

By default, a public folder inherits the settings of its parent folder, including the permissions settings.

Note

For more information about the storage quotas and limits for public folders in Exchange Online, see [Exchange Online Limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- You can't create a public folder unless you've first created a public folder mailbox. For more information about how to create a public folder mailbox, see [Create a public folder mailbox](create-public-folder-mailbox).
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to create a public folder

When using the EAC to create a public folder, you'll only be able to set the name and the path of the public folder. To configure additional settings, you'll need to edit the public folder after it's created.

1. In the Exchange admin center, go to **Public folders** &gt; **Public folders**.
2. If you want to create this public folder as a child of an existing public folder, open the existing public folder in the list view. If you want to create a top-level public folder, skip this step.
3. Select **Add a public folder**.
4. Provide a **Name** for the public folder.

    Important

    Don't use a backslash ( **\** ) in the name when creating a public folder.
5. In the **Path** box, verify the path to the public folder. If this isn't the desired path, select **Close** and follow Step 2 of this procedure.
6. Select **Add**.

## Use Exchange Online PowerShell to create a public folder

[Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) before running the following commands.

This example creates a public folder named Reports in the path Marketing\2013.

```PowerShell
New-PublicFolder -Name Reports -Path \Marketing\2013
```

Important

Don't use a backslash (\) in the name when creating a public folder.

For detailed syntax and parameter information, see [New-PublicFolder](/en-us/powershell/module/exchangepowershell/new-publicfolder).

## How do you know this worked?

To verify that you've successfully created a public folder, do the following:

- In the EAC, select **Refresh** to refresh the list of public folders. Your new public folder should be displayed in the list.
- In Exchange Online PowerShell, run any of the following commands:

    ```PowerShell
    Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
    ```

    ```PowerShell
    Get-PublicFolder -Identity \Marketing\2013 -GetChildren
    ```

    ```PowerShell
    Get-PublicFolder -Recurse
    ```