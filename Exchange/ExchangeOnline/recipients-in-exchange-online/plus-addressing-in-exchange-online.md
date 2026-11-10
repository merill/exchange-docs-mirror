---
layout: Conceptual
title: Plus Addressing in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/plus-addressing-in-exchange-online
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
author: officedocspr
ms.author: odocspr
audience: ITPro
f1.keywords: 
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: 
ms.collection: 
ms.custom: 
description: You use plus addressing to support dynamic, disposable recipient (not sender) email addresses in your Exchange Online organization.
ms.date: 2024-05-17T00:00:00.0000000Z
locale: en-us
document_id: 65dc2481-2a27-06f3-976c-90614a863d81
document_version_independent_id: a3c4f846-0578-54ed-f2a8-c511be3605af
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/plus-addressing-in-exchange-online.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/plus-addressing-in-exchange-online
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/plus-addressing-in-exchange-online.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 88056c63-bc96-262b-5b5b-93b855f79f71
---

# Plus Addressing in Exchange Online | Microsoft Learn

Plus addressing (also known as *subaddressing*) is enabled by default in Exchange Online. Subaddressing is an industry-defined way to support dynamic, disposable recipient (not sender) email addresses for mailboxes.

An SMTP email address uses the basic syntax: `<local-part>@<domain>`. For example, `sean@contoso.com`.

Plus addressing uses the syntax: `<local-part>+<tag>@<domain>`. For example, `sean+newsletter@contoso.com`.

The original email address must be valid. The `+tag` value that you add is arbitrary, although regular character restrictions for SMTP email addresses apply (for example, no spaces). For more information about using plus addresses, see the Using plus addresses section.

Plus addressing allows users to use unique, receive-only email addresses that are extensions of their actual email address. It is useful for creating disposable addresses. The tag acts as a label and is useful for managing email and site registrations. Plus addressing can be used in any email client that sends emails and you can receive emails addressed to you using plus addresses as you would normal emails.

When Exchange receives an email for an address that contains a `+`, it will try to resolve the full email address (for example, `sean+newsletter@contoso.com`) to a known mailbox. If the first resolution attempt fails, Exchange does a second attempt to resolve the email address without the plus sign and tag (for example, `sean@contoso.com`).

If inbound internet email for your on-premises organization is routed through Exchange Online, your on-premises mailboxes can also use plus addresses if those mailbox addresses are known in Exchange Online. If the on-premises mailbox addresses are unknown to Exchange Online, plus addressing won't work and message delivery will be affected.

## Disable plus addressing in Exchange

Use the following procedures to disable plus addressing for your organization.

### Use the Exchange admin center to disable plus addressing

1. In the Exchange admin center at https://admin.exchange.microsoft.com, go to **Settings** &gt; **Mail flow**.
2. Select **Turn off plus addressing for your organization** checkbox, and then select **Save**.

### Use Exchange Online PowerShell to disable plus addressing

1. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
2. The command uses the following syntax:

    ```PowerShell
    Set-OrganizationConfig -DisablePlusAddressInRecipients <$true | $false>
    ```

    To disable plus addressing in your organization, run the following command:

    ```PowerShell
    Set-OrganizationConfig -DisablePlusAddressInRecipients $true
    ```

## Using plus addresses

Your users can create new plus addresses by adding a new tag to use them as unique addresses for services that they sign up for. However, they cannot send emails from plus addresses. To automatically identify and filter messages that are sent to plus addresses, use Inbox rules to act on those messages. Using the condition *Recipient address includes*, you can specify an action for messages sent to a particular plus address. For example, you can move messages sent to a plus address to a specific folder.

Plus addresses are not aliases that are configured on the mailbox, therefore they don't resolve to a user's name in Outlook. This limitation results in plus addresses not being easily identifiable in the `To` or `CC` fields of messages.