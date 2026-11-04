---
layout: Conceptual
title: Configure message delivery restrictions for a mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/configure-message-delivery-restrictions
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
description: You can use the EAC or Exchange Online PowerShell to place restrictions on whether messages are delivered to individual recipients. Message delivery restrictions are useful to control who can send messages to users in your organization. For example, you can configure a mailbox to accept or reject messages sent by specific users or to accept messages only from users in your Exchange organization.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-30T00:00:00.0000000Z
locale: en-us
document_id: 6741bc8a-d256-b9a6-6497-ce0b7ce8900b
document_version_independent_id: d6334a6e-ef4b-8ffe-d146-32bbad2eaa60
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/configure-message-delivery-restrictions.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-user-mailboxes/configure-message-delivery-restrictions
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/configure-message-delivery-restrictions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 33c7071d-b64a-24bc-a5f6-003ecba6c5b0
---

# Configure message delivery restrictions for a mailbox in Exchange Online | Microsoft Learn

You can use the Exchange admin center (EAC) or Exchange Online PowerShell to place restrictions on whether messages are delivered to individual recipients. Message delivery restrictions are useful to control who can send messages to users in your organization. For example, you can configure a mailbox to accept or reject messages sent by specific users or to accept messages only from users in your Exchange organization.

Important

Message delivery restrictions do not impact mailbox permissions. A user with Full Access permissions on a mailbox will still be able to update the contents in that mailbox, such as by copying messages into the mailbox, even if that user has been restricted.

The message delivery restrictions covered in this article apply to all recipient types. To learn more about the different recipient types, see [Recipients in Exchange Online](../recipients-in-exchange-online).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to configure message delivery restrictions

1. In the EAC, navigate to **Recipients** &gt; **Mailboxes**.
2. In the list of user mailboxes, select the mailbox that you want to configure message delivery restrictions for. A display pane is shown for the selected user mailbox.
3. Under **Mailbox** settings &gt; **Message delivery restriction**, select the **Manage message delivery restriction** link.
4. In the **Message delivery restrictions** display pane, you'll see the following options:

    - **Accept messages from**: Use this section to specify who can send messages to this user.

        - **All senders**: This option specifies that the user can accept messages from all senders. This option is the default option.
        - **Selected senders**: This specifies that the user can only receive messages from a specific list of senders. Select ![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif)**Add sender** to display the list of all recipients in your Exchange organization. You can also search for a specific recipient by typing the recipient's name in the search box. Select the desired recipients, and then select **Confirm**.
        - **Require senders to be authenticated**: This option prevents anonymous users from sending messages to the user. This effectively prevents the mailbox from receiving messages from external users.
    - **Block messages from**: Use this section to block specific people from sending messages to this user.

        - **None**: This option specifies that the mailbox won't reject messages from any senders in the Exchange organization. This option is the default option.
        - **Selected senders**: Use this option to specify a list of senders that will be prevented from sending messages to this mailbox. Select ![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif)**Add sender** to display the list of all recipients in your Exchange organization. You can also search for a specific recipient by typing the recipient's name in the search box. Select the desired recipients, and then select **Confirm**.
5. Click **Save** to save your changes. Click **Close** to exit from the **Manage mail flow settings** display pane.

## Use Exchange Online PowerShell to configure message delivery restrictions

The following examples show how to use Exchange Online PowerShell to configure message delivery restrictions for a mailbox. For other recipient types, use the corresponding **Set-** cmdlet with the same parameters.

This example configures the mailbox of Robin Wood to accept messages only from the users Lori Penor, Jeff Phillips, and members of the distribution group Legal Team 1.

```PowerShell
Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"
```

This example adds the user named David Pelton to the list of users whose messages will be accepted by the mailbox of Robin Wood.

```PowerShell
Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}
```

This example configures the mailbox of Robin Wood to require all senders to be authenticated. This means the mailbox will only accept messages sent by other users in your Exchange organization.

```PowerShell
Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true
```

This example configures the mailbox of Robin Wood to reject messages from the users Joe Healy, Terry Adams, and members of the distribution group Legal Team 2.

```PowerShell
Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"
```

This example configures the mailbox of Robin Wood to also reject messages sent by members of the group Legal Team 3.

```PowerShell
Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}
```

For detailed syntax and parameter information related to configuring delivery restrictions for different types of recipients, see the following articles:

- [Set-DistributionGroup](/en-us/powershell/module/exchangepowershell/set-distributiongroup)
- [Set-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/set-dynamicdistributiongroup)
- [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox)
- [Set-MailContact](/en-us/powershell/module/exchangepowershell/set-mailcontact)
- [Set-MailUser](/en-us/powershell/module/exchangepowershell/set-mailuser)

**How do you know this worked?**

To verify that you've successfully configured message delivery restrictions for a user mailbox using PowerShell, run the following command which will show all the message delivery restrictions configured for the mailbox of Robin Wood:

```PowerShell
Get-Mailbox -Identity "Robin Wood" | Format-List AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled
```