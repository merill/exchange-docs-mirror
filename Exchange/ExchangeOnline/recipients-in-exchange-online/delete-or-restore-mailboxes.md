---
layout: Conceptual
title: Delete or restore user mailboxes in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/delete-or-restore-mailboxes
Manager: serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.custom:
- has-azure-ad-ps-ref
description: Admins can learn about deleting and restoring mailboxes in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: be7f59a5-bbc9-4b7a-a28b-f47b26dd33a7
ms.reviewer: akprakash
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: eff7fa9f-2dec-34c3-e4b3-53614755499f
document_version_independent_id: 61e856b9-12fb-bdf6-0f49-0f6cc8b4b957
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/delete-or-restore-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/delete-or-restore-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/delete-or-restore-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 70f3b9bb-e3a5-501d-0794-9cdb43978374
---

# Delete or restore user mailboxes in Exchange Online | Microsoft Learn

There are several things you should consider before you decide to delete a user mailbox. There are different kinds of deletions that you can do on a user mailbox and some of them won't allow you to restore or recover the mailbox. This article walks you through the deleted mailbox scenarios, and how to delete, recover or permanently remove a mailbox from Exchange Online.

Note

You can't use EAC to delete or restore user mailboxes.

## Soft-deleted user mailboxes

A soft-deleted user mailbox is a mailbox that has been deleted using the Microsoft 365 admin center or the **Remove-Mailbox** cmdlet in Exchange Online PowerShell, and has still been in the Microsoft Entra ID recycle bin for less than 30 days.

A soft-deleted user mailbox is a mailbox that has been deleted in the following cases:

- The user mailbox's associated Microsoft Entra user account is soft-deleted (the Microsoft Entra user object is out of scope or in the recycle bin container).
- The user mailbox's associated Microsoft Entra user account has been hard-deleted but a Litigation Hold or an eDiscovery hold was placed on the Exchange Online mailbox before it was deleted.
- The user mailbox's associated Microsoft Entra user account has been purged within the last 30 days, which is the retention length Exchange Online keeps the mailbox in a soft-deleted state before it's permanently purged and unrecoverable.

Note

If you run the Microsoft Graph PowerShell cmdlet `Restore-MgDirectoryDeletedItem` to remove a user from the Microsoft Entra ID recycle bin, it will always put an existing Exchange Online mailbox associated with the Microsoft Entra user in a soft-deleted state, as long as the user's license was not removed. However, if you remove the user's license prior to removing the user from the recycle bin, the user will not go into a soft-deleted user mailbox state.

If in the 30-day time period a new Microsoft Entra user is synchronized from the original on-premises recipient account with the same ExchangeGuid or ArchiveGuid, this will result in an ExchangeGuid validation conflict error.

Check out [Overview of inactive mailboxes](/en-us/purview/inactive-mailboxes-in-office-365) for more info about creating an inactive mailbox by placing a Litigation Hold on a mailbox before deleting it.

## Hard-deleted user mailboxes

A hard-deleted user mailbox is a mailbox that has been deleted in the following cases:

- The user mailbox has been soft-deleted for more than 30 days, and the associated Microsoft Entra user has been hard-deleted. Check out the [Remove-MgUser](/en-us/powershell/module/microsoft.graph.users/remove-mguser) cmdlet. All mailbox content such as emails, contacts, and files will be permanently deleted.
- The user mailbox's associated user account has been hard-deleted in Microsoft Entra ID. The user mailbox is now soft-deleted in Exchange Online and stays in the soft deleted state for 30 days. If in the 30 days time period a new Microsoft Entra user is synchronized from the original on-premises recipient account with the same ExchangeGuid or ArchiveGuid, and that new account is licensed for Exchange Online, this results in a hard deletion of the original user mailbox. All mailbox content such as emails, contacts, and files will be permanently deleted.
- The soft deleted mailbox has been deleted using the **Remove-Mailbox** cmdlet with the *PermanentlyDelete* parameter in Exchange Online PowerShell.

The above scenarios assume that the user mailbox isn't in any of the hold states, like Litigation hold or eDiscovery hold. If there is any type of hold on the user mailbox the mailbox can't be removed from Exchange Online. For all mail user recipient types, Litigation hold or eDiscovery hold are ignored and have no impact on the mail users hard-deleted or soft-delete behavior. The mail user object can't be deleted if there is a journal mailbox associated with it. You can disable journaling on the mail user by using the **Disable-JournalArchiving** cmdlet.

## Delete a user mailbox

### Use the Microsoft 365 admin center to delete a user account

When you delete a user account, the corresponding Exchange Online mailbox is deleted and removed from the list of mailboxes in the EAC. After the user account is deleted, it's listed on the **Deleted Users** page in the Microsoft 365 admin center. It can be recovered within 30 days after being deleted. After 30 days, the user account and mailbox are permanently deleted and not recoverable.

To delete a Microsoft 365 or Office 365 work or school account, see [Delete or restore users](/en-us/microsoft-365/admin/add-users/delete-a-user).

### Use Windows PowerShell to permanently delete a user mailbox

This example permanently deletes the user account with UserId "d7ed3b4a-xxxx-4d15-bc2c-c6731803321d" from Microsoft Entra ID.

```PowerShell
Remove-MgDirectoryDeletedItem -DirectoryObjectId "d7ed3b4a-xxxx-4d15-bc2c-c6731803321d"
```

For more details, check out, [Remove-MgDirectoryDeletedItem](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/remove-mgdirectorydeleteditem).

### Use Exchange Online PowerShell to delete a mailbox

- You need permissions before you can perform this procedure or procedures. To see what permissions you need, see the"Recipients" entry in the [Feature permissions in Exchange Online](../permissions-exo/feature-permissions) article.
- To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

When you delete an Exchange Online mailbox using Exchange Online PowerShell, the corresponding Microsoft 365 or Office 365 user is deleted and removed from the list of users in the Microsoft 365 admin center. The user will still be recoverable for 30 days. After the 30 days time limit, the user is permanently deleted.

This example deletes an Exchange Online mailbox and the corresponding user account for Walter Harp.

```PowerShell
Remove-Mailbox -Identity "Walter Harp"
```

## Restore a user mailbox

When you delete a mailbox, Exchange Online retains the mailbox and all its contents until the deleted mailbox retention period expires, which is 30 days. After 30 days, the mailbox is permanently deleted and can't be recovered. The method for restoring a mailbox depends on whether the mailbox was deleted by deleting the user account or removing the Exchange Online license.

### To help understand the current status of a deleted mailbox

Note

This feature requires a Microsoft 365 administrator account. This feature isn't available for Microsoft 365 Government, Microsoft 365 operated by 21Vianet, or Microsoft 365 Germany.

To help you understand the current status of a recently deleted mailbox, we provide automated diagnostics in the Microsoft 365 admin center. To launch the diagnostics, select the following button:

Note

We strongly recommend restoring the mailbox from the same source (Microsoft Entra ID or Exchange Online) from where the user or mailbox was deleted. Failing to do so will result in a failed restore operation.

### Use the Microsoft 365 admin center to restore a user account

If the mailbox was deleted by deleting the corresponding user account, you can restore the mailbox by restoring the user account in the Microsoft 365 admin center.

To restore a user account, see [Delete or restore users](/en-us/microsoft-365/admin/add-users/delete-a-user).

### Use Exchange Online PowerShell to restore a user account

You can recover soft-deleted mailboxes using the PowerShell cmdlet below. The cmdlet example below restores the mailbox for Allie Bellew.

1. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell)
2. Run the **Undo-SoftDeletedMailbox** cmdlet. You're prompted to enter the password.

    ```PowerShell
    Undo-SoftDeletedMailbox allieb@contoso.com -WindowsLiveID allieb@contoso.com -Password (Read-Host "Enter password" -AsSecureString)
    ```

### License removal

When an Exchange Online license is removed from a user, Exchange Online data associated with that account is held for 30 days. After the 30-day grace period, the data is deleted and can't be recovered. If you add the license back to the user during the grace period, this will restore access, and the mailbox will become fully active.

Note

If the Microsoft 365 or Office 365 or Exchange Online license is removed from a user, the user's mailbox is no longer searchable by using an eDiscovery tool such as Content Search or eDiscovery (Premium). For more information, see the "Searching disconnected or de-licensed mailboxes" section in [Feature reference for Content search](/en-us/purview/ediscovery-content-search-reference#searching-disconnected-or-de-licensed-mailboxes).

## Restoring a user in a hybrid deployment

For user mailboxes in a hybrid scenario, if the mailbox has been soft-deleted and the Microsoft Entra user that was associated with the mailbox has been hard-deleted from Microsoft Entra ID, you can use **New-MailboxRestoreRequest** to recover the mailbox. Read [Configure Microsoft 365 Groups with on-premises Exchange hybrid](../hybrid-deployment/set-up-microsoft-365-groups) for more info. The procedures in this section explain how to restore the mailbox for a soft-deleted user.

1. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell)
2. Run the following cmdlet to identify the soft-deleted mailbox that you want to restore.

    ```PowerShell
    Get-Mailbox -SoftDeletedMailbox | Select-Object Name,ExchangeGuid
    ```

    For the soft-deleted mailbox that you want to restore, note its GUID value (you use the value in Step 4).
3. Create a target mailbox for the restored mailbox. For more information, see [Create user mailboxes in Exchange Online](create-user-mailboxes). After you create the target mailbox, run the following command to get the GUID value of the target mailbox that you'll need in the next step.

    ```PowerShell
    Get-Mailbox -Identity <NameOrAliasOfNewTargetMailbox> | Format-List ExchangeGuid
    ```
4. Replace &lt;SoftDeletedMailboxGUID&gt; with the GUID value from Step 2, and &lt;NewTargetMailboxGUID&gt; with the GUID value from Step 3, and run the following cmdlet to restore the mailbox:

    ```PowerShell
    New-MailboxRestoreRequest -SourceMailbox <SoftDeletedMailboxGUID> -TargetMailbox <NewTargetMailboxGUID>
    ```

For other mailbox restoring scenarios related to hybrid infrastructures, refer to [Common mailbox recovery scenarios for hybrid environments](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/Common-mailbox-recovery-scenarios-for-hybrid-environments/ba-p/604681).

## Restoring disconnected on-premises mailboxes to Exchange Online

If you need to restore a disconnected on-premises mailbox to an Exchange Online mailbox, follow the steps in this section.

1. [Open the Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell) or [Connect to Exchange servers using remote PowerShell](/en-us/powershell/exchange/connect-to-exchange-servers-using-remote-powershell).
2. Run the following command to show the required **MailboxGuid** value of the disconnected mailbox:

    ```PowerShell
    Get-MailboxDatabase | Get-MailboxStatistics | where {$_.DisconnectReason -eq "Disabled"} | Format-Table DisplayName,MailboxGuid,LegacyDN,Database
    ```
3. Run the following command to show the required **GUID** value of the mailbox database that holds the disconnected mailbox:

    ```PowerShell
    Get-MailboxDatabase | Format-List Identity,GUID
    ```
4. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell)
5. Replace &lt;MailboxIdentity&gt; with the name, alias, or email address of the target Exchange Online mailbox, and then run one of the following commands:

    - **Restore to Exchange Online mailbox**: Run the following command to show the required **ExchangeGuid** value:

        ```PowerShell
        Get-Mailbox -Identity "<MailboxIdentity>" | Format-List Name,ExchangeGuid,LegacyExchangeDN
        ```
    - **Restore to Exchange Online archive mailbox**: Run the following command to show the required **ArchiveGuid** value:

        Note

        Restoring into a large archive is not supported.

        ```PowerShell
        Get-Mailbox -Identity "<MailboxIdentity>" -TargetIsArchive | Format-List Name,LegacyExchangeDn,ExchangeGuid,ArchiveGuid
        ```
6. Now that we have all the required details, run one of the following commands to start the restore request. In both commands, use the following values:

    - *RemoteHostName* is the FQDN of the Exchange server (for example, mail.contoso.com)
    - *RemoteCredential* is the credentials of an on-premises Exchange administrator account.
    - *RemoteDatabaseGuid* is the **GUID** value of the mailbox database from step 3.
    - *SourceStoreMailbox* is the **MailboxGuid** value of the disconnected mailbox from step 2.
    - **Restore to Exchange Online mailbox**: *TargetMailbox* is the **ExchangeGuid** value of the target Exchange Online mailbox from step 5.

        ```PowerShell
        New-MailboxRestoreRequest -RemoteRestoreType DisconnectedMailbox -RemoteHostName <ServerFQDN> -RemoteCredential (Get-Credential) -RemoteDatabaseGuid <GUID> -SourceStoreMailbox <MailboxGUID> -TargetMailbox <ExchangeGUID>
        ```
    - **Restore to Exchange Online archive mailbox**: *TargetMailbox* is the **ArchiveGuid** value of the target Exchange Online archive mailbox from step 5.

        Note

        Restoring into a large archive is not supported.

        ```PowerShell
        New-MailboxRestoreRequest -RemoteRestoreType DisconnectedMailbox -TargetIsArchive -RemoteHostName <ServerFQDN> -RemoteCredential (Get-Credential) -RemoteDatabaseGuid <GUID> -SourceStoreMailbox "<MailboxGuid>" -TargetMailbox <ArchiveGuid>
        ```
7. To check the status of the restore request, do the following steps:

    1. Run the following command to get the **Identity** value of the mailbox restore request:

        ```PowerShell
        Get-MailboxRestoreRequest
        ```
    2. Replace &lt;MailboxRestoreRequestIdentity&gt; with the **Identity** value of the mailbox restore request from the previous step, and run the following command:

        ```PowerShell
        Get-MailboxRestoreRequestStatistics -Identity <MailboxRestoreRequestIdentity> -IncludeReport
        ```

    After the **PercentComplete** value of the restore request has reached 100, you have successfully restored the disconnected on-premises mailbox to an Exchange Online mailbox.