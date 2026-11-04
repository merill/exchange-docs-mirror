---
layout: Conceptual
title: Convert a distribution list to a shared mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/convert-distribution-groups-to-shared-mailboxes
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
description: Use the Exchange admin center (EAC) or Exchange Online PowerShell to convert an existing distribution list to a shared mailbox.
ms.topic: how-to
author: serdars
ms.author: serdars
ms.reviewer: AkshayaPrakash-PM
f1.keywords:
- NOCSH
ms.custom: 
ms.collection:
- exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2023-05-17T00:00:00.0000000Z
locale: en-us
document_id: 16b3a63d-8f65-25c7-0184-2beed561932b
document_version_independent_id: 580e52c5-5a6a-af59-5802-7e0305c6b355
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/convert-distribution-groups-to-shared-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-distribution-groups/convert-distribution-groups-to-shared-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/convert-distribution-groups-to-shared-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 056e3547-705c-08a5-8c55-a97856904412
---

# Convert a distribution list to a shared mailbox in Exchange Online | Microsoft Learn

Use the Exchange admin center (EAC) or Exchange Online PowerShell to convert an existing distribution list to a shared mailbox. Shared mailboxes make it easy for a group of people in your company to monitor and send email from a common account, such as info@contoso.com or support@contoso.com. When a person in the group replies to a message sent to the shared mailbox, the email looks like it was sent by the shared mailbox, and not by the person who replied.

## Use the EAC to convert distribution list groups into shared mailboxes

Important

Prior to converting an existing distribution list group into a shared mailbox, replace your existing distribution list group's address with another address so that this distribution list group is free to be converted into a shared mailbox. An address being used for a distribution list group cannot be converted into a shared mailbox.

Once you've freed the existing distribution list group from the email address that's to be used for the shared mailbox, perform the following steps:

1. Create shared mailbox.
2. Add users to the shared mailbox.
3. Assign Full Access and Send As permissions to members of a shared mailbox

### Create shared mailbox

1. Go to **Recipients** &gt; **Mailboxes** &gt; **Add a shared mailbox**![Add icon.](../../exchangeonline/media/itpro_eac_addicon.png).
2. Fill in the required fields:

    - **Display name**: A display name based on your discretion
    - **Email address**: Specifically the email address that was freed from the distribution list group.
3. Click **Create** to save your changes and create the shared mailbox.

### Add users to the shared mailbox

1. Select the newly created shared mailbox by clicking anywhere in the row other than the button option that appears in the blank area next to the **Group name** column.
2. In the Distribution list group flyout that opens, click **View all and manage members**.
3. Click **Add members**![Add icon.](../../exchangeonline/media/itpro_eac_addicon.png).
4. In the **Search members list** text box, enter the names of the members who were part of the distribution list group that you had freed the email address from.
5. Once their names appear under Members, check the checkbox corresponding to the names of those persons you want to add as members of the shared mailbox.
6. Select **Save**.

### Assign Full Access and Send As permissions to members of a shared mailbox

1. Go to **Recipients** &gt; **Mailboxes**.
2. Select a mailbox and click **Mailbox delegation**
3. In the **Manage mailbox delegation** flyout that opens, click **Edit**![Edit icon.](../../exchangeonline/media/itpro_eac_editicon.png).
4. To grant **Full Access** and **Send As** permissions, click **Add members**![Add icon.](../../exchangeonline/media/itpro_eac_addicon.png) and then select the users you want to grant permissions to.

    Note

    The **Full Access** permission allows a user to open the mailbox as well as create and modify items in it. The **Send As** permission allows anyone other than the mailbox owner to send email from this shared mailbox. Both permissions are required for successful shared mailbox operation.
5. Click **Save** to save your changes.

## Use Exchange Online PowerShell to convert a distribution list group into a shared mailbox

There's no automated method for converting a distribution group into a shared mailbox. This section describes the manual steps for creating a shared mailbox with the same members, email addresses, and similar properties as the group in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Caution

This procedure requires you to delete the distribution group *before* you create the replacement shared mailbox. Record as much information as you can about the group as described in the early steps of the procedure. You can also use the Microsoft 365 admin center and the new Exchange admin center (new EAC) to record information about the group.

1. The following commands serve two purposes:

    - To see if the distribution group is a member of other groups. After you replace the group with a shared mailbox, you need to add the shared mailbox as a member of those groups.
    - To record the members of the group that you're going to convert.

    ```powershell
    $dgs = Get-DistributionGroup -ResultSize unlimited
    
    $dgs | foreach {Write-Output -InputObject `r`n,($_.Name),"Group Members",("-"*25); Get-DistributionGroupMember -Identity $_ -ResultSize unlimited}
    ```

    For detailed syntax and parameter information, see [Get-DistributionGroup](/en-us/powershell/module/exchangepowershell/get-distributiongroup) and [Get-DistributionGroupMember](/en-us/powershell/module/exchangepowershell/get-distributiongroupmember).
2. To record all properties of the distribution group to convert, use the following syntax:

    ```powershell
    Get-DistributionGroup -Identity <GroupIdentity> | Format-List
    ```

    Where &lt;GroupIdentity&gt; is the name, alias, or email address of the group.

    For example:

    ```powershell
    Get-DistributionGroup -Identity Marketing | Format-List
    ```

    To reveal the full value of a truncated property, replace &lt;PropertyName&gt; with the property name, and then run the following command:

    ```powershell
    Get-DistributionGroup -Identity Marketing | Select-Object -ExpandProperty <PropertyName>
    ```

    For detailed syntax and parameter information, see [Get-DistributionGroup](/en-us/powershell/module/exchangepowershell/get-distributiongroup).
3. Delete the distribution group by using the following syntax:

    ```powershell
    Remove-DistributionGroup -Identity <GroupIdentity>
    ```

    For example:

    ```powershell
    Remove-DistributionGroup -Identity marketing@contoso.com
    ```

    For detailed syntax and parameter information, see [Remove-DistributionGroup](/en-us/powershell/module/exchangepowershell/remove-distributiongroup).
4. Create the replacement shared mailbox using the following syntax and property values from the deleted distribution group.

    - At a minimum, set the PrimarySMTPAddress and DisplayName values of the new shared mailbox to the values from the deleted distribution group.
    - When you *create*the shared mailbox, you can also set the following properties to match the deleted distribution group:
        - Name
        - Alias
        - ModerationEnabled (the default value is $false)
        - ModeratedBy (the default value is empty)
        - SendModerationNotifications (the default value is Always)

    The additional properties that are available to configure in PowerShell *after* you create the shared mailbox are listed in Step 8.

    This example creates a new shared mailbox with the name, alias, display name, and primary email address of the deleted distribution group.

    ```powershell
    New-Mailbox -Shared -Name Marketing -Alias marketing -DisplayName "Marketing Group" -PrimarySMTPAddress marketing@contoso.com
    ```

    For detailed syntax and parameter information, see [New-Mailbox](/en-us/powershell/module/exchangepowershell/new-mailbox).
5. Use the list of groups that contain the deleted group from Step 1 to add the shared mailbox as a member of any required distribution groups or mail-enabled security groups by using the following syntax:

    ```powershell
    $m = "<GroupEmailAddress1>","<GroupEmailAddress2>",..."<GroupEmailAddressN>"
    
    $m | foreach {Add-DistributionGroupMember -Identity $_ -Member <SharedMailboxIdentity}
    ```

    For example:

    ```powershell
    $m = "allemployees@contoso.com","announcements@contoso.com"
    
    $m | foreach {Add-DistributionGroupMember -Identity $_ -Member marketing@contoso.com}
    ```

    For detailed syntax and parameter information, see [Add-DistributionGroupMember](/en-us/powershell/module/exchangepowershell/add-distributiongroupmember).
6. Use the list of members from the deleted group that you recorded in Step 1 to give valid *mail-enabled security principals* (mailboxes, mail users, or mail-enabled security groups) FullAccess permission to the shared mailbox using the following syntax:

    ```powershell
    $u = "<UserOrGroupEmailAddress1>","<UserOrGroupEmailAddress2>",..."UserOrGroupEmailAddressN"
    
    $u | foreach {Add-MailboxPermission -Identity <SharedMailboxIdentity> -AccessRights FullAccess -User $_}
    ```

    For example:

    ```powershell
    $u = "julia@contoso.com","laura@contoso.com"
    
    $u | foreach {Add-MailboxPermission -Identity Marketing -AccessRights FullAccess -User $_}
    ```

    For detailed syntax and parameter information, see [Add-MailboxPermission](/en-us/powershell/module/exchangepowershell/add-mailboxpermission).
7. Use the list of members from the deleted group that you recorded in Step 1 to give valid *mail-enabled security principals* (mailboxes, mail users, or mail-enabled security groups) Send As permission in the shared mailbox using the following syntax:

    Tip

    The variable $u from the previous step should already identify the former group members who need Send As permission on the shared mailbox, so you can reuse that variable in this step. Otherwise, use the same syntax as the previous step to identify new users: `$u = "<UserOrGroupEmailAddress1>","<UserOrGroupEmailAddress2>",..."UserOrGroupEmailAddressN"`

    ```powershell
    $u | foreach {Add-RecipientPermission -Identity <SharedMailboxIdentity> -AccessRights SendAs -Trustee $_}
    ```

    For example:

    ```powershell
    $u | foreach {Add-RecipientPermission -Identity Marketing -AccessRights SendAs -Trustee $_}
    ```

    For detailed syntax and parameter information, see [Add-RecipientPermission](/en-us/powershell/module/exchangepowershell/add-recipientpermission).
8. Use the **Set-Mailbox** cmdlet or the new EAC to [configure other properties](../manage-user-mailboxes/manage-user-mailboxes#use-the-eac-to-configure-user-mailbox-properties) from the deleted group that weren't available when you created the shared mailbox in Step 4.

    For example, the following parameters are available on the **Set-Mailbox** cmdlet:

    - AcceptMessagesOnlyFrom
    - AcceptMessagesOnlyFromDLMembers
    - AcceptMessagesOnlyFromSendersOrMembers
    - BypassModerationFromSendersOrMembers
    - CustomAttribute1 to CustomAttribute10
    - EmailAddresses
    - ExtensionCustomAttribute1 to ExtensionCustomAttribute5
    - GrantSendOnBehalfTo
    - HiddenFromAddressListsEnabled
    - MailTip
    - MailTipTranslations
    - RejectMessagesFrom
    - RejectMessagesFromDLMembers
    - RejectMessagesFromSendersOrMembers
    - SendModerationNotifications

    The parameters that were mentioned in Step 4 on the **New-Mailbox** cmdlet are also available on the **Set-Mailbox** cmdlet.

    For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).
9. By default, messages sent from the shared mailbox by users with Send As permission aren't copied to the sender. To change the behavior so messages are copied to the sender, use the following syntax:

    ```powershell
    Set-Mailbox -Identity <SharedMailboxIdentity> -MessageCopyForSentAsEnabled $true
    ```

    For example:

    ```powershell
    Set-Mailbox -Identity Marketing -MessageCopyForSentAsEnabled $true
    ```

    For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).
10. Tell users to remove the deleted group entry from their AutoComplete list in Outlook. Even though the new shared mailbox and the deleted group have the same information, the current entry in the AutoComplete list is tied to the deleted group, so the current entry needs to be removed. For instructions, see [Remove AutoComplete list entries one at a time](/en-us/outlook/troubleshoot/contacts/information-about-the-outlook-autocomplete-list#remove-autocomplete-list-entries-one-at-a-time).