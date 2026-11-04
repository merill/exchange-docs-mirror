---
layout: Conceptual
title: Test a mail flow rule in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/test-mail-flow-rules
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
description: Learn how to test mail flow rules in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 3d949e2a-8ba4-4261-8cfb-736fd2446ea1
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-03-11T00:00:00.0000000Z
locale: en-us
document_id: 0bee3e8b-4bee-48f8-be8e-bf6d67ed524f
document_version_independent_id: 0d8b0160-b753-e7ca-2f15-cfbef71a45dd
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/test-mail-flow-rules.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/test-mail-flow-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/test-mail-flow-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 027018ae-74e2-a57a-6106-ed589d93190f
---

# Test a mail flow rule in Exchange Online | Microsoft Learn

In cloud-based organizations, you should test new Exchange mail flow rules (also known as transport rules) before you turn them on. If a rule doesn't do exactly what you want or interacts with other rules in unexpected ways, you can avoid any unintended consequences.

Important

Wait at least 30 minutes after creating a rule before you test it. If you test immediately after you create the rule, you might get inconsistent behavior.

## Step 1: Configure a rule in test mode

You can evaluate the conditions for a rule without taking any actions that affect mail flow by choosing a test mode. Or you can look at the message trace for messages that might match the rule. There are two test modes:

- **Test without Policy Tips**: Use this mode together with a **Generate incident report and send it to** action to receive an email message each time an email message matches the rule.
- **Test with Policy Tips**: Use this mode together with a **Notify the sender with a Policy Tip** action to provide the sender with a policy tip each time an email message matches the rule.

    Here's what you see when a rule is matched if you include the incident report action:

    ![Screenshot of the message that is sent when a rule is detected.](../../exchangeonline/media/ta_ex_rule_detected.png)

1. In the Exchange admin center (EAC) at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. On the **Rules** page, do one of the following steps:

    - [Create a mail flow rule](manage-mail-flow-rules#create-a-mail-flow-rule):
        1. On the **Set rule conditions page**, add either of the following actions to the rule (in addition to the regular actions):
            - **Generate incident report and send it to** and specify the recipients and the message properties to include.
            - **Notify the sender with a Policy Tip** and specify the block/override options.
        2. On the **Set rule settings** page in the **Rule mode** section, select **Test with Policy Tips** or **Test without policy tips** based on the action you added to the rule in the previous step.
    - [Modify an existing mail flow rule](manage-mail-flow-rules#view-or-modify-a-mail-flow-rule):
        1. On the **Conditions**tab of the rule details flyout, add either of the following actions to the rule:
            - **Generate incident report and send it to** and specify the recipients and the message properties to include.
            - **Notify the sender with a Policy Tip** and specify the block/override options.
        2. On the **Settings** tab of the rule details flyout in the **Rule mode** section, select **Test with Policy Tips** or **Test without policy tips** based on the action you added to the rule in the previous step.

## Step 2: Evaluate whether your rule does what you intend

Be sure to evaluate the following types of messages as appropriate:

- Messages that you expect to match the rule.
- Messages that you don't expect to match the rule.
- Messages sent to and from people in your organization.
- Messages sent to and from people outside your organization.
- Replies to messages that match the rule.
- Messages that might cause interactions between multiple rules.

### Tips for sending test messages

One way to test is to sign in as both the sender and recipient of a test message.

- If you don't have access to multiple accounts in your organization, you can test in a [trial account](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-products) or create a few temporary users in your organization.
- Use [InPrivate browsing in Microsoft Edge](https://support.microsoft.com/edge/browse-inprivate-in-microsoft-edge) and the equivalent in other web browsers to sign in to multiple accounts on the same computer. Or, use a different computer or device, or web browser for each user.

### Look at the message trace

The [message trace](../../monitoring/trace-an-email-message/message-trace-modern-eac) includes an entry for each rule that is matched for the message, and an entry for each action the rule takes. Message trace is useful for tracking what happens to test messages, and also for tracking what happens to real messages going through your organization.

![Message trace showing mail flow rule actions.](../../exchangeonline/media/ta_ex_rule_trace.png)

1. In the EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Message trace**. Or, to go directly to the **Message trace** page, use https://admin.exchange.microsoft.com/#/messagetrace.
2. On the **Message trace** page, find the messages that you want to trace by using criteria such as the sender and the date sent. For help with specifying criteria, see [Run a Message Trace and View Results](../../monitoring/trace-an-email-message/run-a-message-trace-and-view-results).
3. After locating the message you want to trace, double-click it to view details about the message.
4. Look in the **Event** column for **Transport rule**. The **Action** column shows the specific action taken.

## Step 3: When you're done testing, set the rule to enforce

1. In the EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. [Modify an existing mail flow rule](manage-mail-flow-rules#view-or-modify-a-mail-flow-rule):

    1. On the **Conditions** tab of the rule details flyout, remove either of the following actions that you previously added to the rule:

        - **Generate incident report and send it to**.
        - **Notify the sender with a Policy Tip**.
    2. On the **Settings** tab of the rule details flyout in the **Rule mode** section, select **Enforce**.
3. When you're finished in the rule details flyout, select **Save**.

Tip

To avoid surprises, inform users about new rules that might affect them.

## Troubleshooting suggestions

Here are some common problems and resolutions:

- **Everything looks right, but the rule isn't working**

    Occasionally, it takes longer than 15 minutes for a new mail flow to be available. Wait a few hours, and then test again. Also check to see if another rule might be interfering. Try changing this rule to priority 0 by moving it to the top of the list.
- **Disclaimer is added to original message and all replies, instead of just the original message**

    To avoid this situation, add an exception to the disclaimer rule to look for a unique phrase in the disclaimer.
- **My rule has two conditions, and I want the action to happen when either of the conditions is met, but it only is matched when both conditions are met**

    You need to create two rules, one for each condition. You can easily copy the rule by selecting **Copy** and then remove one condition from the original and the other condition from the copy.
- **I'm working with distribution groups, and "The sender" &gt; "is this person" (*SentTo*) doesn't seem to be working**

    **SentTo** matches messages where a recipient is a mailbox, mail-enabled user, or contact. It doesn't work with distribution groups. Instead, use **The sender** &gt; **is a member of this group** (*SentToMemberOf*).

## Other testing options

The [Exchange transport rule report](../../monitoring/mail-flow-reports/mfr-exchange-transport-rule-report) shows the number of times a rule is matched. In order to be included in the report, a rule must have the **Severity** level set to any value other than **Not specified**. In cloud-based email organizations, you can check the number of times each rule is matched by using a rules report. In order to be included in the reports, a rule must have the **Audit this rule with severity level** check box selected. These reports help you spot trends in rule usage and identify rules that aren't matched.

Note

While most data is in the report within 24 hours, some data might take as long as five days to appear.

## Need more help?

[Manage mail flow rules](manage-mail-flow-rules)

[Mail flow rules (transport rules) in Exchange Online](mail-flow-rules)