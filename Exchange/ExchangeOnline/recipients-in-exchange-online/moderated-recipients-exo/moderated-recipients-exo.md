---
layout: Conceptual
title: Manage message approval in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/moderated-recipients-exo/moderated-recipients-exo
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
description: Learn about message approval in Exchange Online
ms.topic: overview
author: AshaIyengar21
ms.author: serdars
ms.assetid: 43a89f71-8002-4cb0-b3c8-1c2b2597f227
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2021-05-05T00:00:00.0000000Z
locale: en-us
document_id: f9389be9-edde-da61-e370-7939c1d7cf4f
document_version_independent_id: 98df220c-0e27-9498-7cee-86d8ef0f91e5
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/moderated-recipients-exo/moderated-recipients-exo.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/moderated-recipients-exo/moderated-recipients-exo
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/moderated-recipients-exo/moderated-recipients-exo.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: f03d50ac-8263-3dbe-39c1-69f18ec057b2
---

# Manage message approval in Exchange Online | Microsoft Learn

Sometimes it makes sense to have a second set of eyes on a message before the message is delivered. As an Exchange Online admin, you can set this up. Requiring approval before a message is delivered is called *moderation*, and the approver of the message is called the *moderator*.

There are two basic ways to do moderated mail flow in Exchange Online:

- **Require the approval of a moderator for messages sent to a specific recipient**: You can configure groups for moderation in the Exchange admin center (EAC). For other recipient types, you need to use Exchange Online PowerShell. For instructions, see [Configure moderated recipients in Exchange Online](configure-moderated-recipients-exo)
- **Require approval for messages that match specific criteria**: You use mail flow rules (also known as transport rule) to specify the message criteria (for example, message content, the message sender, or message recipients) and who needs to approve the message for delivery (which might include multiple levels of approval). For instruction, see [Use mail flow rules for message approval scenarios in Exchange Online](../../security-and-compliance/mail-flow-rules/common-message-approval-scenarios).

The rest of this article describes how moderation works in Exchange Online.

## How the message approval process works

When you send a message to a moderated recipient in Outlook on the web (formerly known as Outlook Web App), you're notified that your message might be delayed as shown in the following screenshot:

![Message showing message approval notification.](../../exchangeonline/media/ta_mod_sender_notification.png)

The moderator receives an email notification to approve or reject the delivery of the message. The text of the notification includes buttons to approve or reject the message, and the attachment includes the original message to review.

Note

If an admin with the appropriate RBAC permissions joins a moderated distribution group that's configured with auto-approval, no email notifications will be sent to the moderator or to owners.

You can assign [up to 10 moderators](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#moderation-limits-1) to approve or reject moderated emails. Normally one approval request is sent to all moderators. If moderators have different language or cultural settings, the system groups them by each language or cultural setting and sends one request per group.

Example: If 8 Moderators use en-us and 2 use en-gb, two approval requests are sent—one to the 8 en-us Moderators and one to the 2 en-gb Moderators.

![Approval request message, including attachment.](../../exchangeonline/media/ta_mod_approval_request.png)

A message that's waiting for approval is temporarily stored in a system mailbox called the *arbitration mailbox*. The original message is kept in the arbitration mailbox until a moderator takes action on the message. The moderator can take one of the following actions:

- **Approve**: The message goes to the original intended recipients. The original sender isn't notified.
- **Reject**: A rejection message is sent to the sender. The moderator can add an explanation as shown in the following screenshot:

    ![Rejection notice, with comments from moderator.](../../exchangeonline/media/ta_mod_rejection.png)
- **Ignore or delete the approval message** An expiration message is sent to the sender. In Exchange Online, the approval request expires after two days.

    Note

    The processing of expired moderated messages runs every seven days. This means that a moderated message can expire at any time between two and nine days.

The message flow and result of a moderator's actions are described in the following diagram:

![Workflow showing options for approving a message.](../../exchangeonline/media/ta_moderationworkflow.png)

## Moderated recipient FAQ

### Q: What's the difference between a group moderator and a group owner?

A: The owner of a distribution group is responsible for managing the membership of the group. For example, an IT admin might be the owner of the All Employees distribution group, but the Human Resources manager might be set up as the moderator who's responsible for approving messages that are sent to the group.

Also, messages that the owner sends to the distribution group don't need to be approved by a moderator.

### Q: What happens when the moderator sends a message to the distribution group?

A: The message goes directly to the group, bypassing the approval process.

### Q: What happens when only a subset of recipients need approval?

A: Consider a message that's sent to 12 recipients, one of which is a moderated distribution group. The message is automatically split into two copies. One message is delivered immediately to the 11 recipients that don't require approval, and the second message is submitted to the approval process for the moderated distribution group.

If a message is intended for more than one moderated recipient, a separate copy of the message is automatically created for each moderated recipient and each copy goes through the appropriate approval process.

### Q: What if a distribution group contains moderated recipients that require approval?

A: A distribution group can include moderated recipients that also require approval. In this case, after the message to the distribution group is approved, a separate approval process occurs for each moderated recipient that's a member of the distribution group. However, you can also enable the automatic approval of the distribution group members after the message to the moderated distribution group is approved. To do this, you use the *BypassNestedModerationEnabled* parameter on the [Set-DistributionGroup](/en-us/powershell/module/exchangepowershell/set-distributiongroup) cmdlet.

### Q: Is this process different if we have our own Exchange servers?

A: By default, one arbitration mailbox is used for each on-premises Exchange organization. If you have your own Exchange servers and need more arbitration mailboxes for load balancing, follow the instructions for adding arbitration mailboxes in [Reassign and remove arbitration mailboxes that are used for moderated recipients](/en-us/exchange/architecture/mailbox-servers/reassign-and-remove-arbitration-mailboxes-for-moderation). Arbitration mailboxes are system mailboxes and don't require an Exchange license.

### Q: What is the name of arbitration mailboxes used in Moderation in Exchange Online?

A: In Exchange Online, unlike the on-premises version where arbitration mailboxes follow a standard naming convention, there isn't a predefined default name for the arbitration mailboxes used in the moderation process.