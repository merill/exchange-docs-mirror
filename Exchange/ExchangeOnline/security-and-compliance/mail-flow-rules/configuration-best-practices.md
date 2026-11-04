---
layout: Conceptual
title: Best practices for configuring mail flow rules in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/configuration-best-practices
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
description: Learn about the recommendations for mail flow rules in Exchange Online.
ms.topic: best-practice
author: AshaIyengar21
ms.author: serdars
ms.assetid: abd863c3-c0ce-42f3-9470-a573adc3cbba
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2023-05-31T00:00:00.0000000Z
locale: en-us
document_id: afb24bb1-b515-0aa4-2164-c8ea3360562f
document_version_independent_id: f1179e68-e17b-c287-3709-a2d098417e66
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/configuration-best-practices.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/configuration-best-practices
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/configuration-best-practices.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 3f2002d8-4cf1-5645-cf7c-7e78a5cb4c25
---

# Best practices for configuring mail flow rules in Exchange Online | Microsoft Learn

In cloud-based organizations, follow these best practice recommendations for Exchange mail flow rules (also known as transport rules) in order to avoid common configuration errors. Each recommendation links to a article with an example and step-by-step instructions.

## Test your rules

To make sure unexpected things don't happen to email messages, and to make sure you're really meeting the business, legal, or compliance intentions of your rule, be sure to test it thoroughly. There are many options, and rules can interact with each other, so it's important to test messages that you expect both will match the rule and won't match the rule in case you inadvertently made a rule too general. To learn all the options for testing rules, see [Test mail flow rules in Exchange Online](test-mail-flow-rules).

## Scope your rule

Make sure your rule applies only to the messages you intend it to. For example:

- **Restrict a rule to messages either coming into or going out of the organization**: By default, a new rule applies to messages that are sent by **and** received by people in your organization. So if you want the rule to apply only one way, be sure to specify that in the conditions for the rule. For examples, see [Use mail flow rules for attachment blocking scenarios in Exchange Online](common-attachment-blocking-scenarios)
- **Restrict a rule based on the sender's or receiver's domain**: By default, a new rule applies to messages sent from or received by any domain. Sometimes you want a rule to apply to all domains except for one, or to just one domain. See [Create sender blocklists for cloud mailboxes](/en-us/defender-office-365/create-block-sender-lists-in-office-365).

For a complete list of all the conditions and exceptions that are available for mail flow rules, see [Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions).

## Know when you need two rules

Sometimes it takes two rules to do what you want. Mail flow rules are processed in order, so multiple rules can apply to the same message. For example, if one of the actions is to block the message, and you also have another action you'd like to apply, such as copying the message to the sender's manager or changing the subject for the notification message, you would need two rules. The first rule could copy the message to the sender's manager and change the subject, and the second rule could block the message.

If you use two rules like this, be sure that the conditions are identical. For example:

- [Set up a message approval chain](common-message-approval-scenarios#set-up-a-message-approval-chain)
- [Modify the subject line for notifications](common-attachment-blocking-scenarios#example-3-modify-the-subject-line-for-notifications)

## Don't repeat an action on every email in a conversation

The chain of email in a conversation can include many individual messages, and repeating the action on each message in the thread might get annoying. For example, if you have an action such as adding a disclaimer, you might want it to apply only to the first message in the thread. If so, add an exception for messages that already include the disclaimer text. For an example, see [Organization-wide message disclaimers, signatures, footers, or headers in Exchange Online](disclaimers-signatures-footers-or-headers).

## Know when to stop rule processing

Sometimes it makes sense to stop rule processing once a rule is matched. For example, if you have one rule to block messages with attachments and one to insert a disclaimer in messages that match a pattern, you probably should stop rule processing once the message is blocked. There's no need for further action.

To stop rule processing after a rule is triggered, in the rule, select the **Stop processing more rules** check box.

## If you have lots of keywords or patterns to match, load them from a file

For example, you might want to prevent emails from being sent if they contain a list of unacceptable or bad words. You can create a text file containing these words and phrases, and then use PowerShell to set up a mail flow rule that blocks messages that use them.

The text file can contain regular expressions for patterns. These expressions are not case-sensitive. Common regular expressions include:

| Expression | Matches |
| --- | --- |
| **.** | Any single character |
| **\*** | Any additional characters |
| **\d** | Any decimal digit |
| [*character\_group*] | Any single character in *character\_group*. |

For an example that shows a text file with regular expressions and the Exchange module Windows PowerShell commands to use, see [Use mail flow rules to route email based on a list of words, phrases, or patterns in Exchange Online](use-rules-to-route-email).

To learn how to specify patterns using regular expressions, see [Regular Expression Reference](/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference).

## Don't chain DLP rule actions and mail flow rule conditions

In the transport pipeline, mail flow rules evaluate and act on message before DLP rules. Once a message has been evaluated by mail flow rules, the message isn't evaluated or acted upon by mail flow rules again during delivery.

If a DLP rule changes message properties that affect delivery (for example, by adding recipients), the message is resubmitted into the transport pipeline for delivery. Mail flow rules don't evaluate the message again, because the message has already been evaulated.

So, if a DLP rule add recipients to a message, the message containing those new recipients isn't evaluated by mail flow rules.