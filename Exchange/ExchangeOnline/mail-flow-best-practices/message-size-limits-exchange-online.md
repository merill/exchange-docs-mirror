---
layout: Conceptual
title: Message size limits in exchange online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/message-size-limits-exchange-online
Manager: shrianan
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Message size limits and how to configure them
ms.date: 2026-11-04T00:00:00.0000000Z
ms.service: exchange-online
ms.topic: concept-article
ms.author: arindamt
author: ArindamT
audience: ITPro
locale: en-us
document_id: 5c51851c-6cd4-0082-c5be-1fcacb526be4
document_version_independent_id: ee34ea20-85d3-045d-b70b-036d1d956b31
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/message-size-limits-exchange-online.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/message-size-limits-exchange-online
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/message-size-limits-exchange-online.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: f263c9be-bbd4-4efc-c0fa-c8da05168c42
---

# Message size limits in exchange online | Microsoft Learn

Exchange Online limits the size of messages that users can send and receive. By default, the maximum message size is 35 MB for sending and 36 MB for receiving. But sometimes users need to send or receive email messages that are larger than the default limits in Exchange Online. For example, a user might need to send a large presentation, log file, or other attachment that can't easily be reduced in size. To enable users to send a large file as an actual attachment, administrators can configure mailbox-specific limits up to 150 MB. For more information about the supported limits, see [Exchange Online limits - Service Descriptions](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#message-limits-1).

Important

The message size limit isn't the same as the attachment size limit. The total message size includes the message body, headers, attachments, and any extra size introduced by encoding or content conversion.

This article explains how message size limits work in Exchange Online, how to configure them, and why a large message might still be rejected even after you increase the configured limits.

## Customizable maximum message size

Administrators can customize the maximum message size for an individual mailbox, a group of mailboxes, or all mailboxes in the organization. Exchange Online supports custom mailbox message size limits from 1 MB through 150 MB.

For example, administrators can:

- Allow selected users to send and receive messages up to 100 MB.
- Restrict student mailboxes to 5 MB while allowing faculty mailboxes up to 50 MB.
- Configure a consistent 10 MB limit for cloud and on-premises mailboxes in a hybrid Exchange environment.
- Apply different limits to specific users based on organizational requirements.

Administrators can configure message size limits through the Exchange admin center (EAC) or Exchange Online PowerShell.

To change the message size limit for one or more existing mailboxes, select the mailbox or mailboxes under: Recipients &gt; Mailboxes &gt; Message size restrictions

![Screenshot that shows the message size limit.](../exchangeonline/mail-flow-best-practices/media/message-size-limits-exchange-online/messagesize.png)

For bulk changes, Exchange Online PowerShell is generally more convenient.

Update a single mailbox

```powershell
Set-Mailbox -Identity *alias@domain.com* -MaxSendSize 75MB -MaxReceiveSize 75MB
```

Update multiple mailboxes

```powershell
(“alias”, “alias2”, “alias3”) \| % {Set-Mailbox –Identity \$\_ -MaxSendSize 75MB -MaxReceiveSize 75MB}
```

Update all mailboxes

```powershell
Get-Mailbox \| Set-Mailbox -MaxSendSize 75MB -MaxReceiveSize 75MB
```

Update the default settings (For mailboxes to be created in the future.)

```powershell
Get-MailboxPlan \| Set-MailboxPlan -MaxSendSize 75MB -MaxReceiveSize 75MB
```

> 
> [NOTE] Updating thousands of mailboxes at a time can take a while to complete - a rough rule of thumb is around 5 to 10 minutes per 1,000. And while replicating the updates across the service typically takes an extra 15 minutes, allow up to 30 minutes after the update process is finished before testing out the new settings.

## Understand the effective maximum message size limit

The configured limit applies to the entire email message, not just the attached file. The total message size includes:

- Message headers
- Message body
- Attachments
- MIME encoding
- Content conversion or transcoding overhead

Attachments also need to be encoded when you transport them as part of an email message. This encoding can increase the size of the message. Base64 encoding can increase the size of binary data by approximately 33 percent.

As a result, a mailbox configured with a 150 MB message size limit doesn't necessarily mean that every 150 MB attachment can be sent successfully.

Messages that remain within Microsoft datacenters can be up to 150 MB, subject to the applicable mailbox, client, and service limits. However, messages routed outside Microsoft datacenters are subject to an additional 33 percent translation encoding increase. Microsoft therefore documents a maximum message size of 112 MB for messages routed outside Microsoft datacenters.

As a result, a large message might be delivered successfully to another Microsoft 365 user but fail when sent to an external recipient. Messages between an on-premises Exchange environment and Exchange Online also leave Microsoft datacenters and therefore need to account for this additional encoding overhead.

## Outlook and Outlook on the web can behave differently

The email client you use to send the message can affect the effective limit.

Outlook supports messages up to the applicable Exchange Online maximum, subject to mailbox and transport limits. For example, in Outlook, assuming no transcoding is involved, you can attach a 150 MB file and send it. If the recipient is also hosted in the cloud and is configured to receive 150 MB messages, they receive it.

Outlook on the web accounts for possible encoding expansion and can restrict the message size to approximately 25% less than the configured mailbox limit. It does this proactively to account for the possibility that transcoding might increase the message size.

Therefore, the same large attachment might work in Outlook but be rejected when sent through Outlook on the web.

## What should you check if a large message still fails?

If you increase MaxSendSize and MaxReceiveSize but the message still can't be delivered, don't look only at the attachment size.

- Check sender's limit: Verify that the sender's MaxSendSize allows the message.
- Check Recipient's limit: Make sure the recipient's MaxReceiveSize is high enough. If email gets rejected because of recipient's message size limit, you get the following NDR: Remote server returned '550 5.2.3 RESOLVER.RST.RecipSizeLimit;message too large for this recipient'
- Which email client is used: Check whether the message is being sent from Outlook, Outlook on the web, or another client.
- Message destination: Determine whether the message stays within Microsoft 365 or leaves Microsoft datacenters.
- Encoding overhead: Consider the additional message size introduced by MIME/Base64 encoding.
- External system limits: The recipient's email provider might enforce a smaller message size limit.
- Other systems in the mail path: In hybrid or more complex mail environments, also consider on-premises Exchange servers, connectors, third-party gateways, security services, and recipient messaging systems.

In practice, the lowest applicable limit anywhere in the mail path can determine whether the message is delivered.

## A better option for very large files

Increasing the email message size limit isn't always the best solution. If users regularly need to share large files, consider storing the files in OneDrive or SharePoint and sharing a link instead of attaching the files directly to the message. This approach reduces the size of the email message and avoids the additional message size introduced when attachments are encoded for email transport.