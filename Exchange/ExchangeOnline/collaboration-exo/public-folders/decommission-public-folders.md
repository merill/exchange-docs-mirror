---
layout: Conceptual
title: Decommission public folders in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/decommission-public-folders
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
description: Learn how to remove public folders in Exchange Online.
ms.topic: how-to
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
ms.date: 2024-05-15T00:00:00.0000000Z
locale: en-us
document_id: 9d3f1fcc-f607-8780-a125-1812ca4045ac
document_version_independent_id: f26c3098-0dff-5c3a-47b3-b2a53ef668ff
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/decommission-public-folders.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/decommission-public-folders
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/decommission-public-folders.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 929ac078-7619-32f7-2f73-81789fbeaa14
---

# Decommission public folders in Exchange Online | Microsoft Learn

Exchange Online users can access public folders homed in Exchange Online or Exchange Server (on-premises). There may be scenarios where you want to decommission public folder access for all Exchange Online users. The steps here apply to scenarios where EXO users are accessing public folders deployed locally in Exchange Online or public folders remotely deployed at on-premises servers.

Note

In case you want to partially remove public folder access for selected Exchange Online users who use Outlook for Windows desktop, check [this article.](https://techcommunity.microsoft.com/t5/exchange-team-blog/announcing-support-for-controlled-connections-to-public-folders/ba-p/608591)

Note

If you want to remove public folder deployment from Exchange on-premises, check [this article.](../../collaboration/public-folders/remove-public-folder-deployment-from-exchange-server-2013-later)

## Pre-requisites

Before you proceed, ensure that:

- Exchange Online users no longer need public folder data.
- If you're using Microsoft Entra Connect (formerly known as AAD connect) to synchronize your on-premises directory with Microsoft Entra (AAD), you need to perform the following steps (if you aren't using Microsoft Entra Connect, you can skip these steps):
    - Log in to the on-premises computer that has Entra Connect tool installed, open Microsoft Entra Connect, and then select **Configure**.
    - On the **Additional tasks** screen, select **Customize synchronization options**, and then select **Next**.
    - On the **Connect to Microsoft Entra ID** screen, enter the appropriate credentials, and then select **Next**. Once connected, keep clicking **Next** until you're on the **Optional Features** screen.
    - Make sure that **Exchange Mail Public Folders** isn't selected. If it isn't selected, you can continue to the next section. If it's selected, click to clear the check box, and then select **Next**. 
        Note

        If you don't see **Exchange Mail Public Folders** as an option on the **Optional Features** screen, you can exit Microsoft Entra Connect and proceed to the next section.
    - After you have cleared the **Exchange Mail Public Folders** selection, keep clicking **Next** until you're on the **Ready to configure** screen, and then select **Configure**.

After completing the above steps, you need to configure your tenant to remove public folders. All the following steps must be performed from Exchange Online PowerShell with an account that is assigned to the Organization Management role group.

## Disable public folder access on users

Use the following command to determine current public folder deployment state at the organization level:

```powershell
Get-OrganizationConfig | fl PublicFoldersEnabled,RemotePublicFolderMailboxes
```

Optional: If `PublicFoldersEnabled` is Remote with `RemotePublicFolderMailboxes` populated, it indicates that the public folders are deployed and active on-premises. In case you want to remove the on-premises public folder deployment, follow the steps [here.](../../collaboration/public-folders/remove-public-folder-deployment-from-exchange-server-2013-later)

Next, use the following command to update public folder deployment state at tenant level:

```powershell
Set-OrganizationConfig -PublicFoldersEnabled None -RemotePublicFolderMailboxes:$null
```

Next, use the following command to remove any admin-assigned public folder mailbox on the users:

```powershell
Get-Mailbox -ResultSize unlimited | where {$_.DefaultPublicFolderMailbox -ne $Null} | Set-Mailbox -DefaultPublicFolderMailbox $Null
```

Next, use the following command to ensure there's no public folder mailbox assignment present on the users:

```powershell
Get-Mailbox -ResultSize unlimited | where {$_.DefaultPublicFolderMailbox -ne $Null -OR $_.EffectivePublicFolderMailbox -ne $Null}
```

## Check for and remove mail enabled public folders

### Step 1: Check for the presence of Mail Enabled Public Folders (MEPFs)

Run the following command to see if MEPFs are present:

```powershell
Get-MailPublicFolder
```

If the command returns no output, go to Step 2. But, if MEPFs are present and listed in the above command, perform the following step to back up the MEPF details.

#### Optional: Back up the MEPF details

MEPFs don't hold any data themselves, but are objects in Active Directory that are linked to public folder that hosts the actual data.

Run the following command to take backup of MEPF properties:

```powershell
Get-MailPublicFolder -ResultSize Unlimited| Export-Clixml MEPF.XML
```

### Step 2: Disable MEPFs

Run the following command to remove the MEPFs:

```powershell
Get-MailPublicFolder -ResultSize Unlimited | Disable-MailPublicFolder
```

Now, run the `Get-MailPublicFolder` command again and ensure no MEPFs are listed.

## Check for and remove public folder mailboxes

To check for the presence of public folder mailboxes, run the following:

```powershell
Get-Mailbox -PublicFolder
```

If the above command returns no output, go to the next step Disable public folder access on users.

If public folder mailboxes are present and listed after running the above command, use the following commands to remove the public folder (PF) mailboxes:

Note

If there are any legacy or in-place holds on public folder mailboxes, clear them before proceeding to the next step. Check [this article](/en-us/purview/ediscovery-identify-a-hold-on-an-exchange-online-mailbox?source=recommendations) for detailed steps.

```powershell
$hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid

Get-Mailbox -PublicFolder | Where-Object {$\_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

Get-Mailbox -PublicFolder | Where-Object {$\_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
```

Note

The deleted public folder mailboxes can be recovered until the retention period is over. After the retention period is over, the public folder mailboxes will be permanently deleted. Check [this article](/en-us/exchange/collaboration-exo/public-folders/recover-deleted-public-folder-mailbox) for restoring public folder mailboxes.