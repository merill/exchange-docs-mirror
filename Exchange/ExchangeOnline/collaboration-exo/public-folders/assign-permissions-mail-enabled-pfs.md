---
layout: Conceptual
title: Assign "Send As" or "Send on Behalf" permissions for mail-enabled public folders in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/assign-permissions-mail-enabled-pfs
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
description: 'Summary: How to assign "Send As" or "Send on Behalf" permissions to your Exchange Online public folders.'
audience: ITPro
f1.keywords:
- NOCSH
ms.date: 2026-09-09T00:00:00.0000000Z
locale: en-us
document_id: 2c3b94c4-3bbf-f63c-bb69-b1cb646179d5
document_version_independent_id: 32778712-d072-242d-4372-190ae6f37eb7
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/assign-permissions-mail-enabled-pfs.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/assign-permissions-mail-enabled-pfs
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/assign-permissions-mail-enabled-pfs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 18b8501e-558f-c6db-5e39-f9bd2303f1b0
---

# Assign "Send As" or "Send on Behalf" permissions for mail-enabled public folders in Exchange Online | Microsoft Learn

You can assign either "Send As" or "Send on Behalf" permissions for mail-enabled public folders to users in Microsoft Exchange Online.

## What do you need to know before you begin?

- Estimated time to complete this task: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in [Sharing and collaboration permissions](../../permissions/feature-permissions/sharing-and-collaboration-permissions).
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the Exchange admin center (EAC) to assign permissions

1. Sign in to Exchange admin center as an administrator.
2. Select **Public folders** &gt; **Public folders**.
3. In the list view, select the public folder that requires the permissions.
4. In the details pane, under **Delegation**, select **Edit**.
5. Select **Add members** and select the user from the list to grant send on behalf permission.
6. Select **Save**.

## Use Exchange Online PowerShell to assign permissions

The following example assigns "Send on Behalf" permissions for the mail-enabled public folder *NewPF1* to the user *Jason*.

`Set-MailPublicFolder -Identity '\\NewPF1' -GrantSendOnBehalfTo "Jason"`

The following example assigns "Send As" permissions for the mail-enabled public folder *NewPF1* to the user *Jason*.

`Add-RecipientPermission -Identity 'NewPF1' -Trustee "Jason" -AccessRights 'SendAs'`

For detailed syntax and parameter information, see the following articles:

- [Set-MailPublicFolder](/en-us/powershell/module/exchangepowershell/set-mailpublicfolder)
- [Add-RecipientPermission](/en-us/powershell/module/exchangepowershell/add-recipientpermission)

## Assign Send As permission to a mail-enabled public folder in a hybrid scenario

For Exchange Online mailboxes accessing public folders deployed at On-Premises:

1. Ensure Mail Enabled Public Folders are synced to Exchange Online:

    ```powershell
    Get-MailPublicFolder <MEPFName>
    ```

    Example:

    ```powershell
    Get-MailPublicFolder OnPremPF
    ```

    If the MEPF from On-Premises aren't showing in EXO, use the Sync-MailPublicFolders.ps1 (for Exchange Server 2010) or Sync-ModernMailPublicFolders.ps1 (For Exchange 2013/2016/2019) to sync the MEPF's first.
2. Use following command in EXO PowerShell to assign SendAs permission:

    ```powershell
    Add-RecipientPermission -Identity 'OnPremPF1' -Trustee "Richard" -AccessRights 'SendAs'
    ```