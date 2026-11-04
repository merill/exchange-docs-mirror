---
layout: Conceptual
title: Manage user mailboxes in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes
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
description: After you create a user mailbox, you can make changes and set additional properties by using the EAC or Exchange Online PowerShell.
ms.topic: how-to
author: AshaIyengar21
f1.keywords:
- CSH
ms.custom:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailboxWizardForm.NewMailboxIntroductionWizardPage
ms.author: serdars
ms.assetid: 957ca61c-1fa1-42ab-a0e6-8488e4782566
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-07T00:00:00.0000000Z
locale: en-us
document_id: 5b6f1a1a-efb4-28f8-f3a5-498a791b14ed
document_version_independent_id: 09e95bf4-b434-6b27-c7bd-51b3a1ce079d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 7b8d2ce9-846d-32f3-5ffd-af83166eceb6
---

# Manage user mailboxes in Exchange Online | Microsoft Learn

After you create a user mailbox, you can make changes and set additional properties by using the Exchange admin center (EAC) or Exchange Online PowerShell.

## What do you need to know before you begin?

- Estimated time to complete each user mailbox task: 2 to 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" section in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to configure user mailbox properties

1. In the EAC, go to **Recipients** &gt; **Mailboxes**.
2. In the list of user mailboxes, click the mailbox that you want to change the properties for. A display pane is shown for the selected user mailbox.
3. The properties for user mailboxes that you can change are organized in multiple tabs on this pane. Let's go over each pane

### General

Use the **General** section to view or change basic information about the user. There are also the following options available:

- **Hide from global address list (GAL)**: Choose **Manage hide from GAL** link and use the toggle to prevent the recipient from appearing in the address book and other address lists in your organization. Users can still send messages to the recipient by using the email address.
- **Email Addresses**: Choose **Manage email address types** section to add, view or change the email addresses associated with the user mailbox. This includes the user's primary SMTP address and any associated alternative addresses. The primary SMTP address (also known as the default reply address) is displayed in bold text in the address list. Select **Add email address type** to add new email addresses. Choose **Edit** to change an existing address, and **Remove** to delete an existing address.
- **Mailbox Usage**: You can view the mailbox storage limit and current size of the mailbox. These storage settings are configured by default when the mailbox is created, and apply to all mailboxes in your organization, but you can also customize for specific mailboxes.
- **Email apps & mobile devices** Use this section to view and manage the default settings email apps and mobile devices. Choose **Manage email apps settings** to turn on or off mailbox access features. Choose **Manage mobile devices** to assign mobile device mailbox policies, block access, or wipe data for existing mobile devices.

### Organization

Use the **Organization** section to record detailed information about the user's role in the organization. This information is displayed in the address book. Also, you can create a virtual organization chart that is accessible from email clients such as Outlook. Choose the **Manage Organization Information** to make changes.

The one property you can't change is the **Direct reports** property. A direct report is a user who reports to a specific manager. If you've specified a manager for the user, that user appears as a direct report in the details of the manager's mailbox. For example, Kari manages Chris and Kate, so Kari's mailbox is specified in the **Manager** box of Chris's mailbox and Kate's mailbox, and Chris and Kate appear in the **Direct reports** box in the properties of Kari's mailbox.

### Delegation

Use this section to assign permissions to other users (also called delegates) to allow them to sign in to the user's mailbox or send messages on behalf of the user. You can assign the following permissions:

- **Send as**: This permission allows a delegate to use this mailbox to send messages. After this permission is assigned to a delegate, any messages sent by the delegate appear as if they were sent by the mailbox owner.
- **Send on behalf**: This permission also allows a delegate to use this mailbox to send messages. After this permission is assigned to a delegate, the **From:** address in any message sent by the delegate indicates that the message was sent by the delegate on behalf of the mailbox owner.
- **Read and manage (Full Access)**: This permission allows a delegate to sign in to the user's mailbox and view the contents of the mailbox. However, after this permission is assigned to a delegate, the delegate can't send messages from the mailbox. To allow a delegate to send email from the user's mailbox, you still have to assign the delegate the Send on behalf or Send as permission.

### Mailbox

Use the **Mailbox** section to view or change the following mailbox features and settings:

- **Message Size Restrictions**: These settings control the size of messages that the user can send and receive. Select **Manage message size restriction** to view maximum size for sent and received messages.
- **Email forwarding**: Email forwarding lets you set up a mailbox to forward email messages sent to that mailbox to another user's mailbox in or outside of your organization. Choose **Manage email forwarding** and turn the Email forwarding option to ON/OFF.
- **Message delivery restriction**: These settings control who can send emails to this user. Choose **Manage message delivery restriction** to view and change these restrictions.

    - **Accept messages from**: Use this section to specify who can send messages to this user.
        - **All senders**: Select this option to specify that the user can accept messages from all senders. This includes both senders in your Exchange organization and external senders. This option is selected by default. This option includes external users only if you clear the **Require senders to be authenticated** check box. If you select this check box, messages from external users will be rejected.
        - **Selected senders**: Select this option to specify that the user can accept messages only from a specified set of senders in your Exchange organization. Click ![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif)**Add sender** to display the **Accept messages from** page, which displays a list of all recipients in your Exchange organization. Select the recipients you want, add them to the list, and then click **Confirm**. You can also search for a specific recipient by typing the recipient's name in the search box and then clicking **Search**![Search icon](../../exchangeonline/media/itpro_eac_.gif).
    - **Block messages from**: Use this section to block people from sending messages to this user.
        - **None**: Select this option to specify that the mailbox won't reject messages from any senders in the Exchange organization. This option is selected by default.
        - **Selected senders**: Select this option to specify that the mailbox will reject messages from a specified set of senders in your Exchange organization. Click ![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif)**Add sender** to display the **Block messages from** page, which displays a list of all recipients in your Exchange organization. Select the recipients you want, add them to the list, and then click **Confirm**. You can also search for a specific recipient by typing the recipient's name in the search box and then clicking **Search**![Search icon](../../exchangeonline/media/itpro_eac_.gif).
- **Sharing policy**: This box shows the sharing policy applied to the mailbox. A sharing policy controls how users in your organization can share calendar and contact information with users outside your Exchange organization.
- **Role assignment policy**: This box shows the role assignment policy assigned to the mailbox. The role assignment policy specifies the role-based access control (RBAC) roles that are assigned to the user and control what specific mailbox and distribution group configuration settings users can modify.
- **Retention policy**: This box shows the retention policy assigned to the mailbox. A retention policy is a group of retention tags that are applied to the user's mailbox. They allow you to control how long to keep items in users' mailboxes and define what action to take on items that have reached a certain age.
- **Address book policy**: This box shows the address book policy applied to the mailbox. An address book policy allows you to segment users into specific groups to provide customized views of the address book.

### Others

The following options are configurable in the Others section:

- **Custom attributes**: This section displays the custom attributes defined for the user mailbox. To specify custom attribute values, choose **Custom attributes**. You can specify up to 15 custom attributes for the recipient.
- **Member of**: Use this section to view a list of the distribution groups or security groups to which this user belongs. You can't change membership information on this page. You can change group membership by managing the groups directly.
- **Automatic replies**: Use these settings to create automatic reply (Out of Office) messages. This is the same setting that users can configure in Outlook themselves, but administrators can also do it for them.
- **Recover deleted items** Use this settings to recover deleted email messages in a user's mailbox. Administrators can search for deleted items based on Time or Subject Line or Item type by choosing **Recover deleted items**.
- **Convert to shared mailbox**: Use this settings to convert a mailbox from regular to shared.
- **Litigation hold**: This feature is disabled by default. Litigation hold preserves deleted mailbox items and records changes made to mailbox items. Deleted items and all instances of changed items are returned in a discovery search. Choose **Manage litigation hold** and turn **On** the Litigation hold toggle to put the mailbox on litigation hold. If the mailbox is on litigation hold, turn it **Off** to remove the litigation hold. Mailboxes on litigation hold can't be deleted. To delete the mailbox, you must first remove the litigation hold.
- **Mailbox archive**: If an archive mailbox doesn't exist for the user, this feature is disabled. To enable Mailbox archive, choose **Manage mailbox archive** and the enable the mailbox archive.
- **Recipient limit**: This setting controls the maximum number of recipients the user can send a message to. Choose **Set recipient limit** to limit the number of recipients allowed in the To:, Cc:, and Bcc: boxes of an email message and then specify the maximum number of recipients. The default limit is 500 recipients.
- **Mail tip**: Use the **Manage mail tip** setting to add a mail tip to give users more information if they send a message to this recipient. A mail tip is text that is displayed when this recipient is added to the To, Cc, or Bcc boxes of a new email message.

### Use the EAC to bulk edit user mailboxes

1. In the EAC, go to **Recipients** &gt; **Mailboxes**.
2. In the list of mailboxes, select two or more mailboxes.
3. This will change the list of available actions on the page. Choosing any of the options will open the pane to make changes to the corresponding setting.
4. Make the changes on the properties page and then choose **Save**.

## Use Exchange Online PowerShell to change user mailbox properties

Use the **Get-Mailbox** and **Set-Mailbox** cmdlets to view and change properties for user mailboxes. For information about what parameters correspond to mailbox properties, see the following topics:

- [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox)
- [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox)

Here are some examples of using Exchange Online PowerShell to change user mailbox properties.

This example shows how to forward Pat Coleman's email messages to Sunil Koduri's (sunilk@contoso.com) mailbox.

```PowerShell
Set-Mailbox -Identity patc -DeliverToMailboxAndForward $true -ForwardingAddress sunilk@contoso.com
```

This example uses the **Get-Mailbox** command to find all user mailboxes in the organization, and then uses the **Set-Mailbox** command to set the recipient limit to 500 recipients allowed in the To:, Cc:, and Bcc: boxes of an email message.

```PowerShell
Get-Mailbox -ResultSize unlimited -Filter "RecipientTypeDetails -eq 'UserMailbox'" | Set-Mailbox -RecipientLimits 500
```

This example uses the **Get-Mailbox** cmdlet to find all users in the Customer Service department, and then uses the **Set-Mailbox** cmdlet to change the maximum message size for sending messages to 2 MB.

```PowerShell
Get-Mailbox -Filter "Department -eq 'Customer Service'" | Set-Mailbox -MaxSendSize 2MB
```