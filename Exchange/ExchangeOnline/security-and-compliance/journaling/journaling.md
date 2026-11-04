---
layout: Conceptual
title: Journaling in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/journaling/journaling
Manager: laurawi
ms.subservice: exo-security-compliance
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn how to use journaling in Exchange Online to meet compliance needs or integrate with third-party solutions. Discover best practices and important considerations for secure email archiving.
ms.topic: article
author: k-reagle
ms.author: kreagle
ms.assetid: 1e7df155-02a3-4daf-94f9-8ea46f041a3a
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ai-usage: ai-assisted
ms.date: 2026-05-29T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1012
locale: en-us
document_id: b8d4ec80-7a55-398a-22e9-3f5df24a867b
document_version_independent_id: 4543c414-41d1-b8fe-8a58-4dc61ccf61ff
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/journaling/journaling.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/journaling/journaling
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/journaling/journaling.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 5d650127-80be-5e78-5e37-2f572700f6cc
---

# Journaling in Exchange Online | Microsoft Learn

Important

Please refer to the [Microsoft 365 security center](https://security.microsoft.com/homepage) and the [Microsoft Purview compliance portal](https://compliance.microsoft.com/homepage) for Exchange security and compliance features. They are no longer available in the new [Exchange admin center](https://admin.exchange.microsoft.com).

When possible, we recommend that you use [Microsoft 365 retention](/en-us/purview/retention) to archive and manage data in-place to meet your compliance requirements. However, some organizations might need to use a third-party solution to receive a copy of emails for storage or other scenarios. Configure journaling to store that data outside Exchange.

## Considerations for journaling

Journaling is an older feature from Exchange that moves data outside Microsoft 365, so you must take extra precautions to secure it and also resolve any duplication that might result from this solution. It is your responsibility to monitor and follow up on any non-delivery receipts to the journaling mailbox that can occur because of external and dependent services.

You don't have these more administrative overheads when you use Microsoft 365 retention and other [Microsoft Purview compliance solutions](/en-us/purview/) that keep the data within your tenant. As a more modern compliance solution, they aren't restricted to just email but can also manage today's array of communication and productivity apps, such as Microsoft Teams.

## Journal rules

The following are key aspects of journal rules:

- **Journal rule scope**: Defines which messages are journaled by the Journaling agent.
- **Journal recipient**: Specifies the SMTP address of the recipient you want to journal.
- **Journaling mailbox**: Specifies one or more mailboxes used for collecting journal reports.

In Exchange Online, there's a limit to the number of journal rules that you can create. For details, see [Journal, Transport, and Inbox rule limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#journal-transport-and-inbox-rule-limits).

### Journal rule scope

You can use a journal rule to journal only internal messages, only external messages, or both. The following list describes these scopes:

- **Internal messages only**: Journal rules with the scope set to journal internal messages sent between the recipients inside your Exchange organization.
- **External messages only**^1^: Journal rules with the scope set to journal external messages sent to recipients or received from senders outside your Exchange organization.
- **All messages**: Journal rules with the scope set to journal all messages that pass through your organization regardless of origin or destination. These messages include the ones that may have already been processed by journal rules in the Internal and External scopes.

^1^If the sender and recipients are both in [accepted domains](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains) of the same organization, the messages are not honored as external, even if the `x-ms-exchange-crosstenant-authas` header in the messages has the value `anonymous`. Accordingly, these messages are not journaled as external.

### Journal recipient

You can implement targeted journaling rules by specifying the SMTP address of the recipient you want to journal. The recipient can be a mailbox, distribution group, dynamic distribution group, mail user, or contact. These recipients may be subject to regulatory requirements, or they may be involved in legal proceedings where email messages or other communications are collected as evidence. By targeting specific recipients or groups of recipients, you can easily configure a journaling environment that matches your organization's processes and meets regulatory and legal requirements. Targeting only the specific recipients that need to be journaled also minimizes storage and other costs associated with retention of large amounts of data.

All messages sent to or from the journaling recipients you specify in a journaling rule are journaled. If you specify a distribution group as the journaling recipient, all messages sent to or from members of the distribution group are journaled. If you don't specify a journaling recipient, all messages sent to or from recipients that match the journal rule scope are journaled.

Note

The SMTP address specified for the journaling recipient cannot contain a wildcard character. For example, the SMTP address cannot be listed as `*@contoso.com`.

### Journaling mailbox

The journaling mailbox is used to collect journal reports. How you configure the journaling mailbox depends on your organization's policies, regulatory requirements, and legal requirements. You can specify one journaling mailbox to collect messages for all the journal rules configured in the organization, or you can use different journaling mailboxes for different journal rules or sets of journal rules.

You can't designate an Exchange Online mailbox as a journaling mailbox. You can deliver journal reports to an on-premises archiving system or a third-party archiving service. If you're running an Exchange hybrid deployment with your mailboxes split between on-premises servers and Exchange Online, you can designate an on-premises mailbox as the journaling mailbox for your Exchange Online and on-premises mailboxes.

Journaling mailboxes contain sensitive information. You must secure journaling mailboxes because they collect messages that are sent to and from recipients in your organization. These messages may be part of legal proceedings or may be subject to regulatory requirements. Various laws require that messages remain tamper-free before they're submitted to an investigatory authority. We recommend that you create policies that govern who can access the journaling mailboxes in your organization, limiting access to only those individuals who have a direct need to access them. Speak with your legal representatives to make sure that your journaling solution complies with all the laws and regulations that apply to your organization.

Important

If you configure a journaling rule to send journal reports to a journaling mailbox that doesn’t exist or is temporarily unavailable, the journal reports remain in the transport queue on Microsoft datacenter servers. Delivery is retried periodically for up to 24 hours to address temporary delivery failures. If the journal reports can't be delivered after the retry period, a non-delivery report (NDR) for the journal report is generated and sent to the alternate journaling mailbox.

#### Alternate journaling mailbox

When the journaling mailbox is unavailable, you may not want the undeliverable journal reports to collect in mail queues on Mailbox servers. Instead, you can configure an alternate journaling mailbox to store those journal reports. The alternate journaling mailbox receives the journal reports as attachments in the non-delivery reports (also known as NDRs or bounce messages) generated when the journaling mailbox or the server on which it's located refuses delivery of the journal report or becomes unavailable. As with the journaling mailbox, you can't designate an Exchange Online mailbox as an alternate journaling mailbox.

When the journaling mailbox becomes available again, you can use the **Send Again** feature in Outlook to submit journal reports for delivery to the journaling mailbox.

When you configure an alternate journaling mailbox, all the journal reports that are rejected or can't be delivered across your entire Exchange organization are delivered to the alternate journaling mailbox. Therefore, it's important to make sure that the alternate journaling mailbox and the Mailbox server where it's located can support many journal reports.

Caution

If you configure an alternate journaling mailbox, you must monitor the mailbox to make sure that it doesn't become unavailable at the same time as the journal mailboxes. If the alternate journaling mailbox also becomes unavailable or rejects journal reports at the same time, the rejected journal reports are lost and can't be retrieved. Due to [existing limits on receiving email for Exchange Online mailboxes](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#receiving-limits), configuring the alternate journaling mailbox to be an Exchange Online mailbox is not supported.

Because the alternate journaling mailbox collects all the rejected journal reports for the entire Exchange Online organization, you must make sure that this doesn't violate any laws or regulations that apply to your organization. If laws or regulations prohibit your organization from allowing journal reports sent to different journaling mailboxes from being stored in the same alternate journaling mailbox, you may be unable to configure an alternate journaling mailbox. Discuss this with your legal representatives to determine whether you can use an alternate journaling mailbox.

When you configure an alternate journaling mailbox, you should use the same criteria that you used when you configured the journaling mailbox.

Important

The alternate journaling mailbox should be treated as a special dedicated mailbox. Any messages addressed directly to the alternate journaling mailbox aren't journaled.

## Journal reports

A journal report is the message that the Journaling agent generates when a message matches a journal rule and is to be submitted to the journaling mailbox. The original message that matches the journal rule is included unaltered as an attachment to the journal report. The body of a journal report contains information from the original message such as the sender email address, message subject, message-ID, and recipient email addresses. This is also referred to as envelope journaling, and is the only journaling method supported by Microsoft 365 and Office 365.

### Journal reports and IRM-protected messages

When implementing journaling, you must consider journaling reports and IRM-protected messages. IRM-protected messages affect the search and discovery capabilities of third-party archiving systems that don't have RMS support built-in. In Microsoft 365 and Office 365, you can configure journal report decryption to save a clear-text copy of the message in a journal report. The messages and attachments are decrypted if the encryption originates from the organization. Journaling doesn't decrypt items that are encrypted by external organizations.

To enable journal report decryption for the organization, complete these steps.

1. On your local computer, using a work or school account that has compliance admin permissions in your organization, [connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
2. Run the `Set-IRMConfiguration` cmdlet to enable journal report decryption.

    ```powershell
     Set-IRMConfiguration -JournalReportDecryptionEnabled $true
    ```

    Set the `JournalReportDecryptionEnabled` parameter to `true` to enable decryption. Set the parameter to `false` to disable decryption.

    Important

    Journal report decryption doesn't currently support the explicit use of OME branding templates. If you use an Exchange mail flow rule (also known as a transport rule) to apply an OME branding template, the journal report won't contain a decrypted copy of the message. Currently, journal report decryption only works with the default OME branding template that's applied without a mail flow rule by Exchange Online. In other words, the branding template applied by OME implicitly on messages.

## Troubleshooting

When a message matches the scope of multiple journal rules, all matching rules are triggered.

- If the matching rules are configured with different journal mailboxes, a journal report is sent to each journal mailbox.
- If the matching rules are all configured with the same journal mailbox, only one journal report is sent to the journal mailbox.

Journaling always identifies messages as internal if the email address in the SMTP **MAIL FROM** command is in a domain that's configured as an accepted domain in Exchange Online. These messages include spoofed messages from external sources (messages where the **X-MS-Exchange-Organization-AuthAs** header value is also Anonymous). Therefore, journal rules that are scoped to external messages won't be triggered by spoofed messages with SMTP **MAIL FROM** email addresses in accepted domains.

The 'mail from' field is left empty for Out of Office (OOF) automatic reply messages. Since an empty **MAIL FROM** field cannot be resolved to an accepted internal domain, is leading to these messages being journaled by journal rules scoped to external.

### Duplicate journal report scenarios in a hybrid Exchange environment

In a hybrid Exchange environment, the following scenarios are known to result in duplicate journal reports and these are considered by design:

1. **Cloud to cloud**: Any situations where email is forked will lead to duplicate journaling, such as:

    - Transport chipping (too many recipients on the message).
    - Internal and external recipients exist on the same message – two forks are created for spam/phishing purposes (one in which internal recipients exist, and one in which external recipients exist).
    - Any future needs where the cloud needs to fork the message.
2. **Cloud to on-premises**: Once when cloud journals and once when on-premises journals.
3. **On-premises to cloud**: Once when on-premises journals and once when the cloud journals. This can be prevented by setting the PreventDuplicateJournalingEnabled parameter to true on Exchange Online tenant. To enable this setting, run the following command-

    ```powershell
    Set-TransportConfig -PreventDuplicateJournalingEnabled $true
    ```

### Skip journal report generation

We bypass journaling for emails that have already been journaled without any changes to the recipient list, or if the original email is already a journaling report.

### Journaling for quarantined messages

When a message is sent to [quarantine](/en-us/defender-office-365/quarantine-about) by a mail flow rule, the message doesn't get journaled until it's released from quarantine.

If you're having trouble with the **JournalingReportDNRTo** mailbox, see the Microsoft support article [Mail flow rules and Inbox rules in Exchange Online don't work as expected](https://support.microsoft.com/help/2829319).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).