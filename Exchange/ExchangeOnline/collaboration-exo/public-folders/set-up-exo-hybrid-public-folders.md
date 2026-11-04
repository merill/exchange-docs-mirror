---
layout: Conceptual
title: Configure Exchange Online public folders for a hybrid deployment | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/set-up-exo-hybrid-public-folders
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
ms.topic: article
author: serdars
ms.service: exchange-online
ms.assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- exchange-online
- M365-email-calendar
description: 'Summary: Use the steps in this article to enable on-premises Exchange Server users to access public folders in Exchange Online.'
audience: ITPro
f1.keywords:
- NOCSH
ms.date: 2026-06-03T00:00:00.0000000Z
locale: en-us
document_id: 9e5e98d1-4f1a-b0dc-5abc-218895903ecf
document_version_independent_id: a273e1f9-03e6-721d-e3f3-4af949a9c8c0
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/set-up-exo-hybrid-public-folders.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/set-up-exo-hybrid-public-folders
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/set-up-exo-hybrid-public-folders.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 77faf61f-0b1a-f1cd-8c97-1e34d5f779ae
---

# Configure Exchange Online public folders for a hybrid deployment | Microsoft Learn

**Applies to**

- Exchange Server 2016
- Exchange Server 2019
- Exchange Online

**Summary**: Use the steps in this article to enable on-premises Exchange Server users to access public folders in Exchange Online.

In a hybrid deployment, your users can be in Exchange Online, on-premises, or both, and your public folders are either in Exchange Online or on-premises.

This article describes how to enable users in your Exchange Server on-premises environment to access Exchange Online public folders. To enable Exchange Online users to access on-premises Exchange Server public folders, see [Configure Exchange Server public folders for a hybrid deployment](../../hybrid-deployment/set-up-modern-hybrid-public-folders).

Note

If you have Exchange 2010 public folders, see [Configure legacy on-premises public folders for a hybrid deployment](set-up-legacy-hybrid-public-folders).

## What do you need to know before you begin?

1. There should be no active public folder deployment in on-premises environment. The steps are meant for on-premises environment that doesn't have any public folders deployed.
2. These instructions assume that you use the Hybrid Configuration Wizard to configure and synchronize your on-premises and Exchange Online environments and that the DNS records used for most users' AutoDiscover references an on-premises endpoint. For more information, see [Hybrid Configuration Wizard](../../hybrid-configuration-wizard).
3. Implementing public folder coexistence for an Exchange Server hybrid deployment with Exchange Online might require you to fix conflicts during the import procedure. Conflicts can happen due to non-routable email address assigned to mail enabled public folders, conflicts with other users and groups in Microsoft 365, and other attributes.
4. On-premises users accessing Exchange Online public folders must have associated Mail Enabled User present in the cloud. Microsoft Entra Connect synchronization tool does this.

    For example:

    On-premises mailbox:

    [![Screenshot of on-premises mailbox.](../../exchangeonline/media/on-premises-mailbox.png)](../../exchangeonline/media/on-premises-mailbox.png#lightbox)

    Corresponding Mail Enabled User in Exchange Online:

    [![Screenshot of mail enabled user in Exchange Online.](../../exchangeonline/media/mail-enabled-user.png)](../../exchangeonline/media/mail-enabled-user.png#lightbox)
5. Use the supported version of Classic Outlook for Windows desktop.
6. Outlook 2016 and 2019 for Mac supports cross-premises public folders. For more information, see [Accessing public folders with Outlook 2016 and 2019 for Mac](access-public-folders-with-outlook-2016-for-mac).

    Note

    New Outlook, OWA, and Outlook for Mac for Microsoft 365 don't support accessing public folders in this configuration.
7. In case the on-premises environment has public folder deployed at any time, ensure that the following properties are set to true:

    ```powershell
    Get-OrganizationConfig | fl PublicFolderMailboxesLockedForNewConnections,PublicFolderMailboxesMigrationComplete
    ```

    **Expected output:**

    [![Screenshot of command to set property to true.](../../exchangeonline/media/set-prop-true-cmd.png)](../../exchangeonline/media/set-prop-true-cmd.png#lightbox)

    If the values aren't as per expected output, change the values using the following command:

    ```powershell
    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$true -PublicFolderMailboxesMigrationComplete:$true
    ```

Important

For this configuration (user with a mailbox on-premises accessing Exchange Online public folders), public folders aren't accessible using Outlook on the web (formerly known as Outlook Web App) or using New Outlook for Windows (code named Monarch).

## Step 1: Download the scripts

1. Download the following scripts:

    - [Import-PublicFolderMailboxes.ps1](https://aka.ms/Import-PublicFolderMailboxes)
    - [Sync-MailPublicFoldersCloudToOnprem.ps1](https://aka.ms/PublicFolderScripts#mail-public-folder-sync)
2. Save the files to the local computer on which you're running PowerShell. For example, C:\PFScripts.

## Step 2: Sync MEPFs from Exchange Online to on-premises

This step is required only if you have mail enabled public folders present in Exchange Online and on-premises users need to email the MEPFs.

Use the following command in EXO PowerShell to confirm if you have mail enabled public folders in Exchange Online:

```powershell
Get-MailPublicFolder
```

[![Screenshot of Get-MailPublicFolder command.](../../exchangeonline/media/get-mailpublicfolder-cmd.png)](../../exchangeonline/media/get-mailpublicfolder-cmd.png#lightbox)

If you don't see any MEPFs present in EXO, skip the next steps and go to step 3, otherwise continue.

Configure secure mail routing from on-premises to MEPFs in EXO.

Run the following steps at on-premises Exchange server.

1. Use the following command to create accepted domain for &lt;domain&gt;.onmicrosoft.com

    ```powershell
    New-AcceptedDomain -DomainName contoso.onmicrosoft.com -Name ForMEPFMailRouting
    ```
2. Add the &lt;domain&gt;.onmicrosoft.com to send connector created by HCW:

    ```powershell
    Get-SendConnector "*Outbound to Office 365*" |Set-SendConnector -AddressSpaces @{add="smtp:Contoso.onmicrosoft.com"}
    ```

    Note

    Re-run of HCW with the option to re-create connectors might overwrite the send connector. If that happens, re-add the domain with the above command.
3. Synchronize MEPF objects from EXO to on-premises:

    The `Sync-MailPublicFoldersCloudToOnprem.ps1` script synchronizes the mail-enabled public folders from Exchange Online to Exchange Server on-premises environment. Special permissions assigned to mail-enabled public folders need to be recreated in the cloud, since cross-premise permissions aren't supported in Hybrid Deployment scenarios. For more information, see [Exchange Server Hybrid Deployment](../../exchange-hybrid).

    Sign in to Exchange on-premises server as an organization admin and run the following script from Exchange Management Shell:

    ```powershell
    Sync-MailPublicFoldersCloudToOnprem.ps1
    ```

    Provide the tenant administrator credentials when prompted.

    Note

    Synchronized mail-enabled public folders appear as mail contact objects for mail flow purposes and aren't viewable in the Exchange admin center. See the `Get-MailPublicFolder` command. To recreate the SendAs permissions in the cloud, use the `Add-RecipientPermission` command.
4. In case the on-premises environment has public folder deployed at any time, ensure that the following properties are set to true:

    ```powershell
    Get-OrganizationConfig | fl PublicFolderMailboxesLockedForNewConnections,PublicFolderMailboxesMigrationComplete
    ```

    **Expected output:**

    [![Screenshot of command to set property to true.](../../exchangeonline/media/set-prop-true-cmd.png)](../../exchangeonline/media/set-prop-true-cmd.png#lightbox)

    If the values aren't as per expected output, change the values using the following command:

    ```powershell
    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$true -PublicFolderMailboxesMigrationComplete:$true
    ```

## Step 3: Configure on-premises users to access Exchange Online public folders

The final step in this procedure is to configure the Exchange Server on-premises organization to allow access to Exchange Online public folders.

The script `Import-PublicFolderMailboxes.ps1` imports public folder mailbox objects (not public folder object themselves) from the Exchange Online as mail-enabled users (MEU) to your on-premises environment. The script also configures the imported objects as remote public folder mailboxes. Exchange server automatically configures these MEUs as EffectivePublicfolderMailbox on the Exchange on-premises mailboxes.

The script imports public folder mailboxes from Exchange Online that aren't excluded from serving hierarchy and creates mail enabled users in on-premises environment. For environments that have more than 10 public folder mailboxes in Exchange Online, MEU is created for the first 10 public folder mailboxes that aren't excluded from serving hierarchy.

1. On Exchange Server, run the following command to import public folder mailbox objects from the cloud to your on-premises Active Directory.

    ```powershell
    Import-PublicFolderMailboxes.ps1
    ```

    Where Credential is your Microsoft 365 tenant admin username and password.

    Note

    The script should be run each time there's a change (like deletion or addition) in the public folder mailboxes in Exchange Online.
2. Run the following command in Exchange Management Shell to enable on-premises users to access the Exchange Online public folders:

    ```powershell
    Set-OrganizationConfig -PublicFoldersEnabled Remote
    ```

    Note

    You must wait until Active Directory synchronization is complete to see the changes. This process can take up to 30 minutes to complete. If you don't want to wait for the recurring synchronizations that occur every 30 minutes, you can force the active directory synchronization at any time.

## How do I know this worked?

1. Use following command at on-premises server to ensure `RemotePublicFolderMailbox` property is configured:

    ```powershell
    Get-OrganizationConfig | fl RemotePublicFolderMailboxes
    ```

    Expected output:

    [![Screenshot of RemotePublicFolderMailbox command.](../../exchangeonline/media/remote-public-folder-mailbox-cmd.png)](../../exchangeonline/media/remote-public-folder-mailbox-cmd.png#lightbox)

    If you don't see `RemotePublicFolderMailboxes` populated, re-run the `Import-PublicFolderMailboxes.ps1` script
2. Use the following command to ensure the EffectivePublicFolderMailbox property is populated on the Exchange on-premises mailbox:

    ```powershell
    Get-Mailbox | ft name,EffectivePublicFolderMailbox
    ```

    Expected output:

    [![Screenshot of EffectivePublicFolderMailbox command.](../../exchangeonline/media/effective-public-folder-mailbox-cmd.png)](../../exchangeonline/media/effective-public-folder-mailbox-cmd.png#lightbox)
3. Once you see EffectivePublicFolderMailbox, sign in to Classic Outlook for on-premises user and perform the following public folder tests:

    - View the hierarchy.
    - Check permissions.
    - Create and delete public folders.
    - Post content to and delete content from a public folder.

## Known Issues

**Repeated authentication prompt in Classic Outlook, after the steps in the article are followed.**

If the on-premises users are getting repeated authentication prompt, after the public folder access is configured, follow the steps in [this article](/en-us/microsoft-365/enterprise/modern-auth-for-office-2013-and-2016) to ensure the modern authentication isn't disabled at on-premises clients.