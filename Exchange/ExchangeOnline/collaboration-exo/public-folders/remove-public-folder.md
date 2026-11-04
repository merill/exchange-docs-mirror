---
layout: Conceptual
title: Remove a public folder in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/remove-public-folder
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
description: You may need to remove public folders that are no longer being used in your organization. To help determine which public folders should be removed, see View statistics for public folders and public folder items.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
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
document_id: 79bd814b-da7f-7870-9854-9323502d66f5
document_version_independent_id: c1c2cd29-0853-0d1a-7983-b74e714578a6
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/remove-public-folder.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/remove-public-folder
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/remove-public-folder.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 6f26ab38-4097-f0e0-04f8-7ccac8b04175
---

# Remove a public folder in Exchange Online | Microsoft Learn

You may need to remove public folders that are no longer being used in your organization. To help determine which public folders should be removed, see [View statistics for public folders and public folder items](view-public-folder-statistics).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- You can't delete a mail-enabled public folder. Before you can delete it, you must first disable email for the public folder. For more information, see [Mail-enable or mail-disable a public folder](enable-or-disable-mail-for-public-folder).
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to remove a public folder

1. Go to **Public folders** &gt; **Public folders**.
2. In the list view, select the public folder you want to delete. You can click **Open a public folder**![](../../exchangeonline/media/openafolder.jpg) to open the subfolders of that folder, where you can click to select a specific subfolder to remove.

    To delete a folder or subfolder, select the checkbox of the intended folder and click **Delete**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.gif). If you click the underlined name of the folder, the **Delete** option won't be available to select.

    ![Screenshot that shows openapublicfolder](../../exchangeonline/media/publicfolders.png)
3. A warning message displays asking if you're sure you want to delete the public folder. Click **Confirm** to continue.

## Use Exchange Online PowerShell to delete a public folder

This example deletes the public folder Help Desk\Resolved. This command assumes that the Resolved public folder doesn't have any subfolders.

```PowerShell
Remove-PublicFolder -Identity "\Help Desk\Resolved"
```

This example tests the previous command without making any modifications.

```PowerShell
Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf
```

This example removes the public folder Marketing and all its subfolders because the command runs recursively.

```PowerShell
Remove-PublicFolder -Identity "\Marketing" -Recurse:$True
```

For detailed syntax and parameter information, see [Remove-PublicFolder](/en-us/powershell/module/exchangepowershell/remove-publicfolder).