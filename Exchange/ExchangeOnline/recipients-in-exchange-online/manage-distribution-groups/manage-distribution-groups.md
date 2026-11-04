---
layout: Conceptual
title: Create and manage distribution groups in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups
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
description: Use the Exchange admin center (EAC) or Exchange Online PowerShell to create a new distribution group in your Exchange Online organization or to mail-enable an existing group.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: c4c43493-55e1-46d2-bd4b-d6f6cecd747f
ms.reviewer: AkshayaPrakash-PM
f1.keywords:
- CSH
ms.custom:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDistributionGroupWizardForm.CreateDistributionGroupIntroductionWizardPage
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-17T00:00:00.0000000Z
locale: en-us
document_id: 6f4e18b1-5821-73a0-eef8-5cdafb3b8401
document_version_independent_id: b3534855-b60a-797f-4d65-65b514397ab5
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 0653494e-7001-b972-9452-3d681139cab0
---

# Create and manage distribution groups in Exchange Online | Microsoft Learn

Use the Exchange admin center (EAC) or Exchange Online PowerShell to create, modify, or remove distribution lists in your Exchange Online organization.

Exchange Online supports four types of groups that can be used to distribute messages:

- Distributions lists that can be used only to distribute messages. The article only contains procedures for managing this type of group. You can also convert a distribution list to a shared mailbox. For more information, see [Convert a distribution list to a shared mailbox in Exchange Online](convert-distribution-groups-to-shared-mailboxes).
- Dynamic distribution groups that can be used to distribute messages to recipients matching the membership rules that you define. The membership list is calculated dynamically rather than maintained as a static list. For more information, see [Create and manage dynamic distribution groups in Exchange Online](../manage-dynamic-distribution-groups/create-manage-dynamic-distribution-groups).
- Security groups that can be used to distribute messages and to grant access permissions to resources. For more information, see [Manage mail-enabled security groups](../manage-mail-enabled-security-groups).
- Microsoft 365 groups that can be used to set up a space for people to collaborate and work together on files, chat, calls, and online meetings. For more information, see [Overview of Microsoft 365 Groups](/en-us/microsoft-365/admin/create-groups/office-365-groups)

## What do you need to know before you begin?

- Estimated time to complete: 2 to 5 minutes.
- If you're planning to use Exchange admin center, see [Exchange admin center in Exchange Online](../../exchange-admin-center).
- If you're planning to use Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need permissions before you can do this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- If your organization uses group naming policies, see:

    - [Create a distribution group naming policy](create-group-naming-policy)
    - [Override the distribution group naming policy](override-group-naming-policy)

## Use the Exchange admin center to manage distribution lists

### Use the EAC to create distribution list groups

1. In the [EAC](https://admin.exchange.microsoft.com), click **Recipients** &gt; **Groups** &gt; **Distribution list**.
2. Click **Add a group** which will open the group creation wizard.
3. On **Choose a group type** page, select **Distribution**, click **Next**, and then follow the instructions on the remaining pages of the wizard.
4. On the **Review and finish adding group** page, verify all the details, click **Create group**, and then click **Close**.

### Use the EAC to modify distribution list groups

1. In the [EAC](https://admin.exchange.microsoft.com), click **Recipients** &gt; **Groups** &gt; **Distribution list**.
2. Select an individual group by clicking anywhere in the row.
3. On the **Distribution list group** properties page, click one of the following tabs to view or change properties.

    - General
    - Members
    - Settings
4. When you're finished, click **Save**.

Let's take a look at the settings available in these tabs:

#### General

Use this section to view or change basic information about the group like its display name or description. You can also add, change, remove the email addresses associated with this distribution list.

#### Members

Use this section to manage owners and members for this distribution list. Each distribution list must have at least one owner.

Note

When filtering members in distribution groups with more than 5,000 members, the Exchange Admin Center may display inconsistent results. Until this issue is resolved, use Exchange Online PowerShell or the Microsoft Admin Center to filter and search for members in large distribution groups.

Following are supported member types that can be added in a distribution group:

- UserMailbox
- SharedMailbox
- RoomMailbox
- EquipmentMailbox
- MailUser
- MailContact
- MailUniversalDistributionGroup
- MailUniversalSecurityGroup

And following type of members are not supported to be added:

- Microsoft 365 Group
- Non-mail-enabled Entra user

#### Settings

Select the checkbox **Hide this group from the global address list** if you don't want your users to see this distribution list in the address book. Even when hidden, people will still be able to send emails to this list by typing the email address.

##### Delivery management

Use this section to manage who can send email to this group.

**Sender options**:

- **Only allow messages from people inside my organization**: Select this option to allow only senders in your organization to send messages to the group. This means that if someone outside your organization sends an email message to this group, it is rejected. This is the default setting.
- **Allow messages from people inside and outside my organization**: Select this option to allow anyone, including people on the Internet, to send messages to the group.
- **Specified senders**: You can further limit who can send messages to the group by allowing only specific senders to send messages to this group. Select/remove one or more recipients/group from the drop-down list. If you add senders to this list, they are the only ones who can send mail to the group. Mail sent by anyone not in the list will be rejected.

    Important

    While adding senders, ensure that the sender address is the 'Reply to' field in an email and not the 'From' field, else the email will be rejected.

    If you've configured the group to allow only senders inside your organization to send messages to the group, email sent from a mail contact is rejected, even if they're added to this list.

##### Manage delegates

Use this section to assign permissions to a user (called a delegate) to allow them to send messages as the group or send messages on behalf of the group. You can assign the following permissions using the dropdown for each delegate:

- **Send As**: This permission allows the delegate to send messages as the group. After this permission is assigned, the delegate has the option to add the group to the **From** line to indicate that the message was sent by the group.
- **Send on Behalf**: This permission allows a delegate to send messages on behalf of the group. After this permission is assigned, the delegate has the option to add the group to the **From** line. The message will appear to be sent by the group, and will indicate that it was sent by the delegate on behalf of the group.

To assign permissions to delegates in EAC, add the delegates under the **Edit delegates** page, select the **Permission type** from the drop-down list and click **Save changes**.

##### Message approval

Use this section to set options for moderating the group. Moderators approve or reject messages sent to the group before they reach the group members.

- **Require moderator approval for messages sent to this group**: This check box isn't selected by default. If you select this check box, incoming messages are reviewed by the group moderators before delivery. Group moderators can approve or reject incoming messages.
- **Group moderators**: To add/remove group moderators, search/add users from the drop-down list. If you've selected **Require moderator approval for messages sent to this group** and you don't select a moderator, messages to the group are sent to the group owners for approval.
- **Add senders who don't require message approval**: To add/remove users that can bypass moderation for this group, search/add users from the drop-down list.
- **Notify a sender if their message isn't approved**: Use this section to set how users are notified about message approval.
- **Only sender**: This is the default setting. Notify all senders, inside and outside your organization, when their message isn't approved.
- **Only senders in your organization**: When you select this option, only users or groups in your organization are notified when a message that they sent to the group isn't approved by a moderator.
- **No notifications**: When you select this option, notifications aren't sent to senders whose messages aren't approved by the group moderators.

##### Membership approvals

Use this section to edit membership approvals and to specify if group owner approval is needed for users to join or leave this group.

- **Joining the group**: View/Edit who are allowed to join the group.

    1. **Open**: Anyone can join this group without owner approval.
    2. **Closed**: Only group owners can add members. All requests to join are automatically denied.
    3. **Owner approval**: Anyone can request to join this group and owners must approve the request.
- **Leaving the group**: View/Edit who are allowed to leave the group.

    1. **Open**: Anyone can leave this group without group owner approval.
    2. **Closed**: Only group owners can remove members. All requests to leave are automatically denied.

### Use the EAC to remove distribution list groups

1. In the [EAC](https://admin.exchange.microsoft.com), click **Recipients** &gt; **Groups** &gt; **Distribution list**.
2. In the list of groups, select the distribution list that you want to remove, and then click **Delete group**.

## Use PowerShell to manage distribution list groups

### Use Exchange Online PowerShell to create distribution list groups

This example creates a distribution list group with an alias **itadmin** and the name **IT Administrators**. Anyone can join this group without approval by the group owners.

```PowerShell
New-DistributionGroup -Name "IT Administrators" -Alias itadmin -MemberJoinRestriction open
```

For detailed syntax and parameter information, see [New-DistributionGroup](/en-us/powershell/module/exchangepowershell/new-distributiongroup).

### Use Exchange Online PowerShell to modify distribution list groups

Use the **Get-DistributionGroup** and **Set-DistributionGroup** cmdlets to view and change properties for distribution lists. Advantages of using Exchange Online PowerShell are the ability to change the properties that aren't available in the EAC and to change properties for multiple groups. For information about which parameters correspond to distribution list group properties, see the following articles:

- [Get-DistributionGroup](/en-us/powershell/module/exchangepowershell/get-distributiongroup)
- [Set-DistributionGroup](/en-us/powershell/module/exchangepowershell/set-distributiongroup)

Here are some examples of using Exchange Online PowerShell to change distribution group properties.

This example enables moderation for the distribution group Customer Support and sets the moderator to Amy. In addition, this moderated distribution group will notify senders who send mail from within the organization if their messages aren't approved.

```PowerShell
Set-DistributionGroup -Identity "Customer Support" -ModeratedBy "Amy" -ModerationEnabled $true -SendModerationNotifications 'Internal'
```

This example gives the list of members of the IT Administrators distribution group in a tabular format.

```PowerShell
Get-DistributionGroupMember -Identity "IT Administrators" | Format-Table Name,PrimarySMTPAddress,RecipientType
```