---
layout: Conceptual
title: Common attachment blocking scenarios for mail flow rules in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios
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
description: Admins can learn how to use mail flow rules to block attachments in Exchange Online.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
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
document_id: e6db6edb-0ce9-5250-0e22-d42907394489
document_version_independent_id: 57d853a0-407f-01e5-4a6f-cdbaf7fa4fff
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 47dd463a-b346-fae3-ce42-304881b2ec01
---

# Common attachment blocking scenarios for mail flow rules in Exchange Online | Microsoft Learn

In a cloud-based organization, you might need to block or reject certain types of messages to meet legal or compliance requirements, or to meet specific business needs. This article discusses examples of common scenarios for blocking all attachments which you can set up using mail flow rules (also known mail flow rules).

**Notes**:

- For more examples showing how to block specific attachments by using mail flow rules, see [Use mail flow rules to inspect message attachments in Exchange Online](inspect-message-attachments).
- [Anti-malware polices](/en-us/defender-office-365/anti-malware-protection-about#anti-malware-policies) allow you to block specific file types by turning on and configuring the **common attachment types** filter. For instructions, see [Configure anti-malware policies](/en-us/defender-office-365/anti-malware-policies-configure).

To get started using mail flow rules to block certain message types, do the following steps:

1. Open the Exchange admin center (EAC). For more information, see [Exchange admin center in Exchange Online](../../exchange-admin-center).
2. Go to **Mail flow** &gt; **Rules**.
3. Select **+ Add a rule** and then select **Create a new rule**.
4. In the **Set rule conditions**page that opens, configure the following settings:
    - In the **Name** box, specify a name for the rule.
    - Select the conditions and actions you want.

Note

In the EAC, the smallest attachment size that you can enter is 1 kilobyte, which should detect most attachments. However, if you want to detect every possible attachment of any size, you need to use PowerShell to adjust the attachment size to 1 byte after you create the rule in the EAC. To connect to PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Embedded images are treated as attachments (for example, messages with a picture in the signature). For this reason, we don't recommend using a very small value for the attachment size since unexpected messages will be blocked.

## Example 1: Block messages with attachments, and notify the sender

If you don't want certain people in your organization to send or receive attachments greater than 10 Megabytes, you can set up a mail flow rule to block messages with attachments of this size.

In this example, all messages sent to or from the organization with attachments greater than 10 Megabytes are blocked.

![Screenshot of rule that blocks all attachments.](../../exchangeonline/media/example1.jpg)

If all you want to do is block the message, you might want to stop rule processing once this rule is matched. Scroll down the rule dialog box, and select the **Stop processing more rules** checkbox.

## Example 2: Notify intended recipients when an inbound message is blocked

If you want to reject a message but let the intended recipient know what happened, you can use the **Notify the recipient with a message** action.

You can include placeholders in the notification message so that it includes information about the original message. The placeholders must be enclosed in two percent signs (%%), and when the notification message is sent, the placeholders are replaced with information from the original message. You can also use basic HTML such as &lt;br&gt;, &lt;b&gt;, &lt;i&gt;, and &lt;img&gt; in the message.

| Type of information | Placeholder |
| --- | --- |
| Sender of the message. | %%From%% |
| Recipients listed on the "To" line. | %%To%% |
| Recipients listed on the "Cc" line. | %%Cc%% |
| Subject of the original message. | %%Subject%% |
| Headers from the original message. This list is similar to the list of headers in a delivery status notification (DSN) generated for the original message. | %%Headers%% |
| Date the original message was sent on. | %%MessageDate%% |

In this example, all messages that contain attachments and are sent to people inside your organization are blocked, and the recipient is notified.

![Screenshot of rule that notifies recipients when an inbound message is blocked.](../../exchangeonline/media/example2.jpg)

## Example 3: Modify the subject line for notifications

When a notification is sent to the recipient, the subject line is the subject of the original message. If you want to modify the subject so that it's clearer to the recipient, you must use two mail flow rules:

- The first rule adds the word "undeliverable" to the beginning of the subject of any messages with attachments.
- The second rule blocks the message and sends a notification message to the sender using the new subject of the original message.

Important

The two rules must have identical conditions. Rules are processed in order; so, the first rule adds the word "undeliverable", and the second rule blocks the message and notifies the recipient.

Here's what the first rule would look like if you want to add "undeliverable" to the subject:

![Screenshot of rule that prepends undeliverable to messages with attachments.](../../exchangeonline/media/example3-img1.jpg)

And the second rule does the blocking and notification (the same rule from Example 2):

![Screenshot of rule that notifies recipients when an inbound message is blocked.](../../exchangeonline/media/example2.jpg)

## Example 4: Apply a rule with a time limit

If you have a malware outbreak, you might want to apply a rule with a time limit so that you temporarily block attachments. For example, the following rule has both a start and stop day and time:

![Screenshot of rule showing a time limit.](../../exchangeonline/media/example4.jpg)

## Example 5: Block messages based on attachment file extension

If you want to prevent users from sending or receiving messages that have attachments with specific file extensions, you can create a transport rule in Microsoft 365. This can help you protect your organization from malicious or unwanted files, such as executable programs, scripts, or macros. In this example, you will learn how to create a transport rule that blocks messages based on the file name extension of the attachment.

### Steps to create a transport rule

To create a transport rule that blocks messages with certain attachment types, follow these steps:

1. Sign in to the [Exchange admin center](https://admin.exchange.microsoft.com/).
2. Select **Mail flow** and then select **Rules**.
3. Select **+ Add a rule** and then select **Create a new rule**.
4. In the **Name** box, specify a name for the new rule.
5. Select the **Apply this rule if** drop-down list, point to **Any attachment**, and then select **File extension includes these words**.
6. In the **Specify words or phrases** window, type the file name extension of any attachment that you want to block, and then select the **Add** button to add the file name extension to the list. When the list is completed, select **Save**.
7. Select the **Do the following** drop-down list, point to **Block the message**, and then select **Reject the message and include an explanation** or select **Delete the message without notifying anyone**.
8. If it's required, specify a rejection reason to inform users who will receive the non-delivery report (NDR) of the reason that mail delivery failed, and then select **Save**.
9. Select the **Next** button.
10. On the next page, specify any additional options, such as rule mode and rule activation or deactivation time, and then select **Next**.
11. After reviewing the rule, select **Finish**.

By default, the transport rule is created as disabled. Make sure you toggle the **Enable or disable rule** switch to enable the rule.

[![Screenshot of block email.](../../exchangeonline/media/block-email.png)](../../exchangeonline/media/block-email.png#lightbox)

### Use PowerShell to create a rule that blocks messages with executable attachments

Use the following syntax to create a rule to block messages that contain executable attachments:

```powershell
New-TransportRule -Name "<UniqueName>" -AttachmentHasExecutableContent $true [-RejectMessageEnhancedStatusCode <5.7.1 | 5.7.900 to 5.7.999>] [-RejectMessageReasonText "<Text>"] [-DeleteMessage $true]
```

**Notes**:

- If you use the *RejectMessageEnhancedStatusCode* parameter without the *RejectMessageReasonText* parameter, the default text is: Delivery not authorized, message refused.
- If you use the *RejectMessageReasonText* parameter without the *RejectMessageEnhancedStatusCode* parameter, the default code is 5.7.1.

This example creates a new rule named Block Executable Attachments that silently deletes messages that contain executable attachments.

```powershell
New-TransportRule -Name "Block Executable Attachments" -AttachmentHasExecutableContent $true -DeleteMessage $true
```

For detailed syntax and parameter information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).