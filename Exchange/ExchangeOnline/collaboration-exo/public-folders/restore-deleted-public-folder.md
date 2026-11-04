---
layout: Conceptual
title: Restore a deleted public folder in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/restore-deleted-public-folder
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
ms.reviewer: 
ms.collection:
- exchange-online
description: 'Summary: This article describes how to restore a public folder that was previously deleted in Exchange Online'
audience: ITPro
f1.keywords:
- NOCSH
ms.date: 2026-09-09T00:00:00.0000000Z
locale: en-us
document_id: c512b78f-0b0e-2a19-9537-820c7643fd0b
document_version_independent_id: eba02b04-6cd1-e3ed-1c82-171049c7719b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/restore-deleted-public-folder.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/restore-deleted-public-folder
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/restore-deleted-public-folder.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 0d75e68e-868d-6693-d1d2-15adac61d9a7
---

# Restore a deleted public folder in Exchange Online | Microsoft Learn

This article walks you through the steps to restore a deleted public folder in Exchange Online.

Public folders that have been deleted by users (using clients like Outlook) or admins (using administrative tools like PowerShell or the Exchange admin center) are normally stored in the public folder dumpster located in `\NON_IPM_SUBTREE\DUMPSTER_ROOT`. Deleted folders are preserved there until the retention period ends.

For the scenarios where [public folder contents are put on hold using retention policies](/en-us/purview/create-retention-policies), the folders that are removed from `\NON_IPM_SUBTREE\DUMPSTER_ROOT` are preserved under `\NON_IPM_SUBTREE\DiscoveryHolds` until the retention hold period ends.

You can restore folders that are preserved in the public folder dumpster or under the DiscoveryHolds folder using Exchange Online PowerShell. Restoring the public folder will restore all subfolders and items present in the folder.

In rare scenarios, you might also find folders under `\NON_IPM_SUBTREE\LOST_AND_FOUND`. [See this blog post](https://techcommunity.microsoft.com/t5/exchange-team-blog/introducing-public-folder-8220-lost-and-found-8221-functionality/ba-p/604043) for details on LOST\_AND\_FOUND and how to recover folders if you find them there.

Note

The folders in the dumpster are permanently deleted after the retention period ends. After a public folder has been permanently deleted, you can't restore it, unless the folder is preserved under DiscoveryHolds by a retention policy.

## Permissions required

The user restoring the public folder must have the **Public Folders** role assigned to them. By default, this role is assigned to users present in the **Organization Management** role group.

## Restore a deleted public folder

1. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
2. Determine if the public folder you want to restore is in the public folder dumpster.

    The following command lists all non-system public folders in the dumpster:

    ```PowerShell
    Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse -ResultSize Unlimited | where {$_.FolderClass -ne "$null"}
    ```

    Alternatively, you can search for specific folders. For example, the following command searches for a deleted public folder named `Marketing`:

    ```PowerShell
    Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse -ResultSize Unlimited | where {$_.Name -like "Marketing"}
    ```

    Public folders under `\NON_IPM_SUBTREE\DiscoveryHolds` have a GUID appended to their name that you'll need to account for in your search.

    For example, the following command searches for a deleted public folder named `Sales`:

    ```PowerShell
    Get-PublicFolder \NON_IPM_SUBTREE\DiscoveryHolds -Recurse -ResultSize Unlimited | where {$_.Name -like "*Sales*"}
    ```
3. Use the following syntax to restore a public folder:

    ```PowerShell
    Set-PublicFolder -Identity "Full path of folder to be restored" -Path "Parent folder path where folder needs to be restored"
    ```

    For example, run the following command to restore a public folder named `PF1` to the root of the public folder tree:

    ```PowerShell
    Set-PublicFolder -Identity \NON_IPM_SUBTREE\DUMPSTER_ROOT\DUMPSTER_EXTEND\RESERVED_1\RESERVED_1\9f32c468-4bc2-42aa-b979-16a057394b2f\PF1 -Path \
    ```

    The following alternate example restores a public folder named `Sales` to the root of the public folder tree:

    ```PowerShell
    Set-PublicFolder -Identity \NON_IPM_SUBTREE\DiscoveryHolds\Sales_774d775c-da53-4ee7-869c-353c8a6e3265 -Path \
    ```

    If you don't know the original path of the deleted folder, you can find the folder's original path before it was deleted.

    For example, the following commands reveal the original path of the deleted folder named `Marketing`:

    ```powershell
    $folder = Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse -ResultSize Unlimited | where {$_.Name -like "Marketing"}; Get-PublicFolder (Get-PublicFolder $folder.ParentPath).DumpsterEntryId
    ```

Note

Do not specify `\IPM_Subtree` in the path when restoring the public folder. For example:

Correct syntax:

`Set-PublicFolder \non_ipm_subtree\discoveryholds\Black_73e0bd95-7972-4599-a25b-cdf46345b62b -Path \Finance\`

Incorrect syntax:

`Set-PublicFolder \non_ipm_subtree\discoveryholds\Black_73e0bd95-7972-4599-a25b-cdf46345b62b -Path \IPM_Subtree\Finance\`

### Restore a specific subfolder

Restoring a folder restores all of its subfolders, but you can also restore only one subfolder.

For example, the following commands restore `Subfolder1` under `\Parent1`:

```PowerShell
$pf = Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | where {$_.Name -eq "Subfolder1"}; Set-PublicFolder $pf.identity -Path \Parent1
```

### Restore a public calendar folder

You can restore a public calendar folder using the same procedure as any other public folder, but there are special considerations.

When deleting a public calendar folder, a user sees the following options:

![Delete calendar dialog box.](../../exchangeonline/media/delete-public-calendar-folder.png)

If the user selected "Yes", the items were deleted. In this case, you can restore the public folder, but the items cannot be recovered.

Note

We don't recommend using Outlook to restore deleted public folders because Outlook truncates the public folder names. This issue is under investigation and this article will be updated when a fix is available.