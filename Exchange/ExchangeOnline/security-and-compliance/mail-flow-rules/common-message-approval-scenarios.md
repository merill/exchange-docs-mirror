---
layout: Conceptual
title: Common message approval scenarios in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/common-message-approval-scenarios
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Admins can learn how to use mail flow rules (transport rules) for message approval scenarios that won't work with regular moderated recipients.
ms.topic: overview
author: AshaIyengar21
ms.author: serdars
ms.assetid: 5c13a07e-c21d-4502-a9f9-fb801197e1dd
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
document_id: 16793ac4-a5a2-f768-7e14-26f861ac24c8
document_version_independent_id: d9c2495f-c031-bb35-dee8-7c910cde6036
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/common-message-approval-scenarios.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/common-message-approval-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/common-message-approval-scenarios.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 04b343e9-c46d-aecc-a715-7ceb4aad258c
---

# Common message approval scenarios in Exchange Online | Microsoft Learn

Note

This article doesn't apply to the Built-in security add-on for on-premises mailboxes.

In Exchange Online organizations, a moderated recipient requires the approval of one or more moderators before messages are delivered to the recipient. For more information, see [Moderated recipients in Exchange Online](../../recipients-in-exchange-online/moderated-recipients-exo/moderated-recipients-exo).

But, other than exceptions from specific senders, when you configure the moderation settings in the properties of the recipient, **all** messages that are sent to the recipient require approval before they're delivered, regardless of the content or specifics of the messages.

For granular control over the type and circumstances of messages that require moderation, you can use mail flow rules (also known as transport rules). This article discusses examples of using mail flow rules for moderation to meet specific legal, compliance, or business requirements.

## Forward messages to a sender's manager for approval

Here are some common types of messages that might require manager approval:

- Messages sent from a user to certain distribution groups or recipients
- Messages sent to external users or partners
- Message sent between two groups
- Messages sent with specific content, such as the name of a specific customer
- Messages sent by a trainee

To require that messages need to be sent to the sender's manager for approval, follow these steps:

1. Create a mail flow rule using the **Send messages to a moderator** template.

    [![Screenshot that shows the Send messages to a moderator template to create a new rule.](../../exchangeonline/media/ta_mod_scenario2_template.png)](../../exchangeonline/media/ta_mod_scenario2_template.png#lightbox)
2. Configure the action to send messages to the sender's manager for approval: **Do the following** &gt; **Forward the message for approval** &gt; **to the sender's manager**.
3. Configure the conditions that define the messages that require approval in **Apply this rule if**.

    Here's an example where all external messages sent by the trainee named Garth Fort require approval by their manager:

    - **Apply this rule if** &gt; **The sender** &gt; **is this person** &gt; **avinash@beta.nikey.in**

        and
    - **Apply this rule if** &gt; **The recipient** &gt; **is external/internal** &gt; **Outside the organization**
    - **Do the following** &gt; **Forward the message for approval** &gt; **to the sender's manager**

    [![Screenshot that shows the rule that forwards messages to the user's manager.](../../exchangeonline/media/ta_mod_scenario2_rule.png)](../../exchangeonline/media/ta_mod_scenario2_rule.png#lightbox)

    Note

    Some rule settings, including the ability to add multiple conditions or exceptions to the rule as in this example, are hidden by default. To see them, select **More options**.

## Set up a message approval chain

You can require multiple levels of approval for messages. For example, you can require that messages to a specific customer be approved first by a customer relationship manager and then by a compliance officer, or you can require that expense reports be approved by two levels of managers.

To create this type of multiple-level approval, create one mail flow rule for each level of approval. Each rule detects the same patterns in the messages, as follows:

- The first rule forwards the message to the first moderator. After the first moderator approves the message, a second rule forwards the message to the second moderator, and so on.
- If all moderators in the chain approve the message, the original message is sent to the intended recipients.
- If any of the moderators in the chain reject the approval request, the sender receives a rejection message.
- If any of the approval requests aren't approved within the expiration time (two days for Exchange Online), the sender receives an expiration message.

    Note

    The processing of expired moderated messages runs every seven days. This interval means that a moderated message can expire at any time between two and nine days.

The following example assumes that you have a customer named Blue Yonder Airlines, and you want both the customer relationship manager and the compliance officer to approve all messages that go to this customer.

As shown in the following screenshot, you create two rules. The first rule goes to the first-level approver. The second rule goes to the second-level approver.

[![Screenshot that shows the two rules used for two levels of approval.](../../exchangeonline/media/ta_mod_scenario3_2rules.png)](../../exchangeonline/media/ta_mod_scenario3_2rules.png#lightbox)

The first rule identifies all messages with the company name Blue Yonder Airlines in the subject or message, and it sends these messages to the internal customer relationship manager named Garret Vargas.

- **Name**: Blue Yonder Airlines: Approval #1 Relationship Manager
- **Priority**: Before the second rule.
- **Apply this rule if** &gt; **The sender** &gt; **is external/internal** &gt; **Inside the organization** &gt;.

    and
- **Apply this rule** &gt; **The subject or body** &gt; **subject or body includes any of these words** &gt; 'B.Y.A' or 'BYA' or 'Blue Yonder Airlines' or 'Blue Yonder'.
- **Do the following** &gt; **Forward the message for approval** &gt; **Forward the message for approval** &gt; Avinash P.

[![Screenshot that shows the rule for first-level approver.](../../exchangeonline/media/ta_mod_scenario3_rule1.png)](../../exchangeonline/media/ta_mod_scenario3_rule1.png#lightbox)

The second rule sends these messages to the compliance officer, Tony Krijnen, for approval:

- **Name**: Blue Yonder Airlines: Approval #2 Compliance Manager
- **Priority**: After the first rule.
- **Apply this rule if** &gt; **The sender is located** &gt; **Inside the organization**.

    and
- **Apply this rule if** &gt; **The subject or boy matches** &gt; 'B.Y.A' or 'BYA' or 'Blue Yonder Airlines' or 'Blue Yonder'.
- **Do the following** &gt; **Forward the message for approval to** &gt; Tony Krijnen.

[![Screenshot that shows the second-level approval rule, with same criteria.](../../exchangeonline/media/ta_mod_scenario3_rule2.png)](../../exchangeonline/media/ta_mod_scenario3_rule2.png#lightbox)

Note

You can assign [up to 10 moderators](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#moderation-limits-1) to approve or reject moderated emails. Normally one approval request is sent to all moderators. If moderators have different language or cultural settings, the system groups them by each language or cultural setting and sends one request per group.

## Forward messages that match one of several criteria

Within a mail flow rule, all conditions in the rule must be true for the rule to match (Condition1 AND Condition2). If you want the same action applied for multiple conditions (Condition1 OR Condition2), you need to create a separate rule for each condition.

To do this, on the **Rules** page in EAC, create a rule for the first condition. Then select the rule, select **Copy**, and change the conditions in the new rule to match the second condition.

For approval scenarios, be careful when you create multiple rules with the same action so that the same message isn't sent to the moderator multiple times. Add an exception to the second rule so that it ignores messages that matched the first rule.

For example, you want to send a message to a moderator if the message has "sales quote" in the subject line or message body **or** in the content of any attachments.

You need two rules. If the first rule checks the subject line or message body, the second rule that checks the attachment content needs an exception that checks for "sales quote" in the subject line or message body (the condition of the first rule).

- **Name**: Sales quote approval: Rule 2
- **Priority**: Lower than the first rule.
- **Apply this rule if** &gt; **Any attachment** &gt; **content includes any of these words** &gt; Sales quote.
- **Do the following** &gt; **Forward the message for approval** &gt; **to the sender's manager**
- **Except if** &gt; **The subject or body** &gt; **subject or body matches these text patterns** &gt; Sales quote.

[![Screenshot that shows the exception for the second rule.](../../exchangeonline/media/ta_mod_scenario4.png)](../../exchangeonline/media/ta_mod_scenario4.png#lightbox)

Note

As described previously, some rule settings, including the ability to add multiple conditions or exceptions to the rule as in this example, are hidden by default. To see them, select **More options**.