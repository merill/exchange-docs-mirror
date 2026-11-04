---
layout: Conceptual
title: Manage mail-enabled security groups in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-mail-enabled-security-groups
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
description: A mail-enabled security group can be used to distribute messages and to grant access permissions to resources in Active Directory. For more information, see Recipients.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 80b3b537-4786-4d02-9202-44e373811a25
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
document_id: f0dd3fb4-76a1-4983-dc7a-f5cd7fb35507
document_version_independent_id: 469b3ec9-f9b1-ff8a-baaa-712114808755
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-mail-enabled-security-groups.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-mail-enabled-security-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-mail-enabled-security-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 83e97ed0-c0bc-7be1-7593-f0a05abfb679
---

# Manage mail-enabled security groups in Exchange Online | Microsoft Learn

A mail-enabled security group can be used to distribute messages and to grant access permissions to resources in Active Directory. For more information, see [Recipients in Exchange Online](recipients-in-exchange-online).

## What do you need to know before you begin?

- Estimated time to complete: 2 to 5 minutes.
- You need permissions before you can do this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../permissions-exo/feature-permissions) article.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).

## Use the Exchange admin center to manage a mail-enabled security group

### Use the EAC to create a mail-enabled security group

1. In the [EAC](https://admin.exchange.microsoft.com/), click **Recipients** &gt; **Groups** &gt; **Mail-enabled security**.
2. Click **Add a group** and follow the instructions in the details pane.

    - In the **Choose a group type** section, click **Mail-enabled security** and click **Next**.
    - In the **Set up the basics** section, enter the details and click **Next**.
3. In the **Assign owners** section, click **+ Assign owners**, select the group owner from the list, and click **Next**.
4. Click **Add members** &gt; **+ Add members**, select the group members from the list, and click **Next**.
5. In the **Edit settings** section, enter the group email address, configure the following and then click **Next**:

    - **Privacy**: Set it to either public or private.
    - **Add Microsoft Teams to your group**: Select this to create a Team for your group.
6. In the **Review and finish adding group** section, verify all the details, click **Create group**, and then click **Close**.

### Use the EAC to change mail-enabled security group properties

1. In the EAC, click **Recipients** &gt; **Groups** &gt; **Mail-enabled security**.
2. In the list of groups, select the mail-enabled security group that you want to view or change.
3. In the group's properties page, click one of the following sections to view or change properties.

    When you're finished, click **Save**.

#### General

    Use this section to view or change basic information about the group.

    - **Name**: This name appears in the address book, on the **To** line when email is sent to this group, and in the Groups list. The display name is required and should be user-friendly so people recognize what it is. It also has to be unique in your domain.
    - **Description**: Use this box to describe the group so people know what the purpose of the group is. This description appears in the address book and in the Details pane in the EAC.

#### Email options

    Use this section to view or change the email addresses associated with the group. This includes the group's primary SMTP addresses and any associated proxy addresses. In the **Edit email addresses** page, change/edit the **Primary email address**, add/delete **Aliases**, and then click **Save changes**.

    You can also select the group and then click **Edit email address** from the toolbar to change/edit the **Primary email address**, add/delete **Aliases**, and then click **Save changes**.

#### Members

    Use this section to change/edit the following:

    - In the **Owners** section, click **View all and manage owners** to add/remove group owners from the drop-down list and then click **Save changes**. The mail-enabled security group must have at least one owner.
    - In the **Members** section, click **View all and manage members** to add/remove group members from the drop-down list and then click **Save changes**. The mail-enabled security group must have at least one member.

#### Settings

    In the **General settings** section, select the checkbox **Allow external senders to email this group** if you want to allow the external users to send email to this group.

#### Delivery management

    Use this section to manage who can send email to this group.

    - **Sender options**

        By default, only people inside your organization can send messages to this group. You can also allow people outside the organization to send messages to this group.

        - **Only allow messages from people inside my organization**: Select this option to allow only senders in your organization to send messages to the group. This means that if someone outside your organization sends an email message to this group, it is rejected. This is the default setting.
        - **Allow messages from people inside and outside my organization**: Select this option to allow anyone to send messages to the group.
    - **Specified senders**

        You can further limit who can send messages to the group by allowing only specific senders to send messages to this group. Select/remove one or more recipients/group from the drop-down list. If you add senders to this list, they are the only ones who can send mail to the group. Mail sent by anyone not in the list will be rejected.

        Important

        If you've configured the group to allow only senders inside your organization to send messages to the group, email sent from a mail contact is rejected, even if they're added to this list.

#### Manage delegates

    Use this section to assign permissions to a user (called a delegate) to allow them to send messages as the group or send messages on behalf of the group. You can assign the following permissions:

    - **Send As**: This permission allows the delegate to send messages as the group. After this permission is assigned, the delegate has the option to add the group to the **From** line to indicate that the message was sent by the group.
    - **Send on Behalf**: This permission also allows a delegate to send messages on behalf of the group. After this permission is assigned, the delegate has the option to add the group to the **From** line. The message will appear to be sent by the group and will say that it was sent by the delegate on behalf of the group.

    To assign permissions to delegates in EAC, add the delegates in the **Edit delegates** page, select the **Permission type** from the drop-down list and click **Save changes**.

#### Message approval

    Use this section to set options for moderating the group. Moderators approve or reject messages sent to the group before they reach the group members.

    - **Require moderator approval for messages sent to this group**: This check box isn't selected by default. If you select this check box, incoming messages are reviewed by the group moderators before delivery. Group moderators can approve or reject incoming messages.
    - **Group moderators**: To add/remove group moderators, search/add users from the drop-down list. If you've selected **Require moderator approval for messages sent to this group** and you don't select a moderator, messages to the group are sent to the group owners for approval.
    - **Add senders who don't require message approval**: To add/remove users that can bypass moderation for this group, search/add users from the drop-down list.
    - **Notify a sender if their message isn't approved**: Use this section to set how users are notified about message approval.

        - **Only sender**: This is the default setting. Notify all senders, inside and outside your organization, when their message isn't approved.
        - **Only senders in your organization**: When you select this option, only users or groups in your organization are notified when a message that they sent to the group isn't approved by a moderator.
        - **No notifications**: When you select this option, notifications aren't sent to senders whose messages aren't approved by the group moderators.

#### Membership approvals

    Use this section to specify if group owner approval is needed for users to join this group.

## Use PowerShell to manage mail-enabled security groups

### Use Exchange Online PowerShell to create a mail-enabled security group

This example creates a security group with an alias fsadmin and the name File Server Managers. The security group is created in the default OU, and anyone can join this group with approval by the group owners.

```PowerShell
New-DistributionGroup -Name "File Server Managers" -Alias fsadmin -Type security
```

For more information about using Exchange Online PowerShell to create mail-enabled security groups, see [New-DistributionGroup](/en-us/powershell/module/exchangepowershell/new-distributiongroup).

### How do you know this worked?

To verify that you've successfully created a mail-enabled security group, do one of the following:

- In the EAC, click **Recipients** &gt; **Groups** &gt; **Mail-enabled security**. The new mail-enabled security group is displayed in the group list.
- In Exchange Online PowerShell, run the following command to display information about the new mail-enabled security group.

    ```PowerShell
    Get-DistributionGroup <Name> | Format-List Name,RecipientTypeDetails,PrimarySmtpAddress
    ```

### Use Exchange Online PowerShell to change mail-enabled security group properties

Use the **Get-DistributionGroup** and **Set-DistributionGroup** cmdlets to view and change properties for security groups. Advantages of using Exchange Online PowerShell are the ability to change the properties that aren't available in the EAC and to change properties for multiple security groups. For information about which parameters correspond to which distribution group properties, see the following articles:

- [Get-DistributionGroup](/en-us/powershell/module/exchangepowershell/get-distributiongroup)
- [Set-DistributionGroup](/en-us/powershell/module/exchangepowershell/set-distributiongroup)

Here are some examples of using Exchange Online PowerShell to change security group properties.

This example displays a list of all security groups in the organization.

```PowerShell
Get-DistributionGroup -ResultSize unlimited -Filter "RecipientTypeDetails -eq 'MailUniversalSecurityGroup'"
```

This example changes the primary SMTP address (also called the reply address) for the Seattle Administrators security group from admins@contoso.com to seattle.admins@contoso.com. The previous reply address will be kept as a proxy address.

```PowerShell
Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.admins@contoso.com,smtp:admins@contoso.com
```

This example hides all security groups in the organization from the address book.

```PowerShell
Get-DistributionGroup -ResultSize unlimited -Filter "RecipientTypeDetails -eq 'MailUniversalSecurityGroup'" | Set-DistributionGroup -HiddenFromAddressListsEnabled $true
```

### How do you know this worked?

To verify that you've successfully changed properties for a security group, do the following:

- In the EAC, select the group to view the property or feature that you changed. Depending on the property that you changed, it might be displayed in the details pane for the selected group.
- In Exchange Online PowerShell, use the **Get-DistributionGroup** cmdlet to verify the changes. One advantage of using Exchange Online PowerShell is that you can view multiple properties for multiple groups. In the example above where all security groups were hidden from the address book, run the following command to verify the new value.

    ```PowerShell
    Get-DistributionGroup -ResultSize unlimited -Filter "RecipientTypeDetails -eq 'MailUniversalSecurityGroup'" | Format-List Name,HiddenFromAddressListsEnabled
    ```