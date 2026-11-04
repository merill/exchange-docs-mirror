---
layout: Conceptual
title: Sender Rewriting Scheme (SRS) in Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/sender-rewriting-scheme
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Describes Sender Rewriting Scheme (SRS) in Office 365.
author: Benny-54
ms.author: serdars
audience: ITPro
ms.topic: article
ms.localizationpriority: medium
ms.service: exchange-online
ms.assetid: 
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords: 
ms.date: 2025-09-24T00:00:00.0000000Z
locale: en-us
document_id: 81a08e5b-9e6f-35d9-477d-e2c4c6921e16
document_version_independent_id: ffd42698-bf1f-01de-c8a7-3430f8a57909
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/sender-rewriting-scheme.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/sender-rewriting-scheme
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/sender-rewriting-scheme.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7cbaac1e-1137-4825-819f-cd751d73c036
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/eda7d4a5-11e2-4d6f-b379-0d496f2a17a5
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 20b3bb8d-7b30-a720-07d0-e6ce37f2bb87
---

# Sender Rewriting Scheme (SRS) in Microsoft 365 | Microsoft Learn

The Sender Rewriting Scheme (SRS) feature rewrites the MAIL FROM address (also known as the `5321.MailFrom` address, P1 sender, or envelope sender) for all applicable messages sent from Microsoft 365 to external recipients. SRS was added to Microsoft 365 to resolve a problem where autoforwarding is incompatible with the [Sender Policy Framework (SPF)](/en-us/defender-office-365/email-authentication-spf-configure).

Note

SRS doesn't affect the From address (also known as the `5322.From` address or P2 sender) shown in email clients.

SRS rewriting is used to prevent spoofing of unverified domains. You should send messages only from domains that are configured as [accepted domains](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains).

As of August 2023, SRS is used to rewrite addresses from [mailbox forwarding](../recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding) (also known as SMTP forwarding) instead of the forwarding mailbox. This behavior consolidates all forwarding methods to use SRS in Exchange Online. While SRS is designed to avoid disruptions to forwarded messages, some special cases could see issues. For example, SRS doesn't rewrite messages from on-premises servers to the internet. For more information, see the Relaying from a customer's on-premises server section in this article.

The relay pool in Microsoft 365 affects SRS rewriting behavior. Messages that qualify for the relay pool skip SRS rewriting and are sent from IP addresses that aren't part of the Microsoft 365 SPF record. This behavior mainly affects messages entering Exchange Online that fail SPF checks. SRS doesn't fix these failures. For more information, see [Outbound delivery pools](/en-us/defender-office-365/outbound-spam-high-risk-delivery-pool-about#relay-pool?#relay-pool).

SRS improves the delivery of applicable messages that pass SPF checks when they arrive from the original sender but fail SPF checks at the final external destination after they're forwarded.

SRS rewrites the MAIL FROM address in the following scenarios:

- Messages in Microsoft 365 that are autoforwarded (or redirected) to an external recipient by using any of the following methods:
    - [Mailbox forwarding](../recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding) (also known as SMTP forwarding).
    - Inbox rule redirection.
    - Mail flow rule (also known as transport rule) redirection.
    - Groups with external members.
    - Mail contact forwarding.
    - Mail user forwarding.
- Messages that are autoforwarded (or redirected) from a customer's on-premises environment and relayed through Exchange Online.

Note

SRS rewriting doesn't resolve the issue of forwarded messages not passing DMARC checks. Although SPF checks might pass due to the rewritten MAIL FROM address, DMARC also requires domain alignment between the SPF or DKIM domain and the domain of the From address. In such cases, the only reliable way for DMARC to pass is to ensure the following requirements:

- The message is DKIM-signed using the domain in the From address.
- The DKIM signature remains intact during transit until it reaches the final destination.

Otherwise, if the original sender domain has a 'p=reject' DMARC policy, email servers that enforce DMARC policies might reject the forwarded messages. Authenticated Received Chain (ARC) was developed to address the forwarding limitations of DKIM and is implemented in Microsoft 365.

Part of the SRS implementation is to reroute non-delivery reports (also known as NDRs or bounce messages) to the original sender if a message can't be delivered.

The following sections present different autoforwarding scenarios and how SRS handles them.

## Autoforwarding emails for a mailbox hosted on Microsoft 365

SRS rewrites the MAIL FROM address of messages sent to an Exchange Online mailbox that are then autoforwarded using mailbox forwarding or Inbox rule redirection. SRS rewrites the MAIL FROM address before the message leaves Exchange Online using the following pattern:

`<Forwarding Mailbox Local Part>+SRS=<Hash>=<Timestamp>=<Original Sender Domain>=<Original Sender Username>@<Forwarding Mailbox Domain>`

Or

`bounces+SRS=<Hash>=<Timestamp>@<Default Accepted Domain>` if SRS rewriting would cause the local part of the rewritten email address (before the @) to exceed 64 characters. To receive NDRs for undeliverable messages rewritten by SRS, an admin must create a mailbox named "bounces" in Exchange Online. The domain for this mailbox must be set to the default accepted domain for the organization.

In the following example, a message is sent from `bob@fabrikam.com` to the Exchange Online recipient `john.work@contoso.com`. John set up autoforwarding to his home email address `john.home@adatum.com`. The following table shows the effect of SRS on the message.

| - | Original message | Autoforwarded message |
| --- | --- | --- |
| **Recipient** | `john.work@contoso.com` | `john.home@adatum.com` |
| **MAIL FROM address** | `bob@fabrikam.com` | `john.work+SRS=44ldt=IX=fabrikam.com=bob@contoso.com` |
| **From address** | `bob@fabrikam.com` | `bob@fabrikam.com` |

## Relaying from a customer's on-premises server

When a message from an unverified domain (not an accepted domain) is relayed from a customer's on-premises server or an application through Exchange Online, SRS rewrites the MAIL FROM address before the message leaves Exchange Online using the following pattern:

`bounces+SRS=<Hash>=<Timestamp>@<Default Accepted Domain>`

Tip

To receive NDRs for undeliverable messages rewritten by SRS, an admin must create a mailbox named "bounces" in Exchange Online or on-premises Exchange. The domain for this mailbox must be set to the default accepted domain for the organization.

In the following example, a message is sent from `bob@fabrikam.com` to the on-premises Exchange recipient `john.onprem@contoso.com`. John set up autoforwarding to his home email address `john.home@adatum.com`. The following table shows the effect of SRS on the message.

| - | Original message | Relayed message received by Exchange Online | Relayed message sent from Exchange Online |
| --- | --- | --- | --- |
| **Recipient** | `john.onprem@contoso.com` | `john.home@adatum.com` | `john.home@adatum.com` |
| **MAIL FROM address** | `bob@fabrikam.com` | `bob@fabrikam.com` | `bounces+SRS=44ldt=IX@contoso.com` |
| **From address** | `bob@fabrikam.com` | `bob@fabrikam.com` | `bob@fabrikam.com` |

In this scenario, SRS rewrites the MAIL FROM address. Customers are encouraged to set the default accepted domain to one of their own domains.

## Forwarded messages sent to a customer's on-premises server

By design, SRS considers on-premises servers to be within the trust boundary of an organization, so SRS doesn't rewrite forwarded messages sent to the on-premises environment. In complex routing configurations that use on-premises servers to route messages to the internet, forwarded messages not rewritten by SRS are subject to SPF failure. To solve this issue, admins can enable SRS rewriting for messages flowing through an on-premises outbound connector using the *SenderRewritingEnabled* parameter on the **New-OutboundConnector** and **Set-OutboundConnector** cmdlets in Exchange Online PowerShell.

Tip

For outbound partner connectors that handle messages to external recipients, the value of the *SenderRewritingEnabled* parameter is always `True`, and you get an error if you attempt to change it to `False`.

## Mail Flow rule redirected messages

SRS rewrites the MAIL FROM address before the message leaves Exchange Online using the following pattern:

`bouncesEtr+SRS=<Hash>=<Timestamp>=<OrigSenderDomain>=<OrigSenderUser>@<Default Accepted Domain>`

To receive NDRs for undeliverable messages rewritten by SRS, an admin must create a mailbox named "bouncesETR" in Exchange Online. For example, [Directory-Based Edge Blocking](../mail-flow-best-practices/use-directory-based-edge-blocking) might interfere with NDRs if no such recipient exists in your organization.