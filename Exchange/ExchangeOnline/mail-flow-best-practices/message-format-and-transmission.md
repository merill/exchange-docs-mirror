---
layout: Conceptual
title: Message format and transmission in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/message-format-and-transmission
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
audience: ITPro
ms.localizationpriority: medium
ms.author: serdars
ms.topic: article
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: 828cf844-0f26-44f4-9a76-20bdbd58b992
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
ms.reviewer: 
ms.date: 2018-06-25T00:00:00.0000000Z
description: Learn to control email message format and transmission in Exchange Online. Adjust settings for individual users or domains to optimize message readability.
locale: en-us
document_id: 305b4e17-d851-901f-0313-92e8c9bb208b
document_version_independent_id: fc575c4f-6f17-452c-465b-9d41715ef29a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/message-format-and-transmission.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/message-format-and-transmission
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/message-format-and-transmission.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: bfcfa037-bd2d-0482-1861-4e315557fa05
---

# Message format and transmission in Exchange Online | Microsoft Learn

There are settings in Outlook, Outlook on the web, and Exchange Online that control the format of email messages and how they are sent to people on other domains. The default settings work in most cases. If specific recipients have trouble reading messages sent from your organization, you can adjust the settings for individual users, or for all users on a specific domain. For example, you can prevent recipients from receiving a winmail.dat attachment.

There are two types of settings you can use:

- **Message format**: When a user creates a message, they can choose the message format in which to author the message. In Outlook, they have a choice between plain text, HTML, and rich-text format. In Outlook on the web (formerly known as Outlook Web App) they have a choice between plain text and HTML.
- **Message transmission**: This means how the message is actually sent to the other email system. Exchange can send messages to other domains by using Multipurpose Internet Mail Extensions (MIME) or Transport Neutral Encapsulation Format (TNEF). All three message formats can be sent using TNEF. Only HTML and plain text can be sent using MIME. Message transmission format can be set by an admin per domain or per recipient, and users can also specify message transmission format.

## Message formats

The following list describes the three message formats available in Exchange Online, and shows which ones are available in Outlook and Outlook on the web:

| Format | Description | Available in Outlook | Available in Outlook on the web |
| --- | --- | --- | --- |
| **Plain text** | A plain text message uses only US-ASCII text as described in RFC 2822. The message can't contain different fonts or other text formatting. | Yes | Yes |
| **HTML** | An HTML message supports text formatting, background images, tables, bullet points, and other graphical elements. | Yes | Yes |
| **Rich text format (RTF)** | RTF supports text formatting and other graphical elements.  Only Outlook, Outlook on the web, and a few other MAPI email clients understand RTF messages. Please note that RTF messages that are encrypted with S/MIME will face limitations and may be prone to face conversion issues (like journaling delivery). | Yes | Can read messages formatted in RTF, but can't format or send this format |

## Message transmission formats for mail sent to external recipients

The following table describes the message transmission formats that Exchange Online uses to send email messages to external recipients.

| Transmission format | Description |
| --- | --- |
| **Transport Neutral Encapsulation Format (TNEF)** | TNEF is a Microsoft-specific format for transmitting formatted email messages. A TNEF message contains a plain text version of the message and an attachment that packages the original formatted version of the message. Typically, this attachment is named Winmail.dat. The Winmail.dat attachment includes formatting, attachments, and Outlook-specific features such as meeting requests.  An email client that fully understands TNEF, such as Outlook, processes the Winmail.dat attachment and displays the original message content without ever displaying the Winmail.dat attachment. An email client that doesn't understand TNEF may present a TNEF message in any of the following ways:  The plain text version of the message is displayed, and the message contains an attachment named Winmail.dat, Win.dat, or some other generic name such as Att\_nnnnn\_.dat or Att\_nnnnn\_.eml where the *nnnnn* placeholder represents a random number.  The plain text version of the message is displayed. The TNEF attachment is ignored or removed. The result is a plain text message.  There are third-party utilities that can help convert Winmail.dat attachments. |
| **Multipurpose Internet Mail Extensions (MIME)** | MIME is an internet standard that supports text in character sets other than ASCII, non-text attachments, message bodies with multiple parts, and header information in non-ASCII character sets. |

## Message format and transmission settings

Admins and users can control message formatting and transmission. Admin settings override user settings.

Admins can control the following settings:

- **Remote domain settings**: Remote domain settings control the format of messages sent to people on the remote domain. You can control the format for a specific external domain, or for all external domains. For more information about remote domains, see [Remote domains in Exchange Online](remote-domains/remote-domains). The remote domain settings override the per-user settings set by admins or users.
- **Mail user and mail contact settings**: You can change settings for individual recipients by changing settings for specific mail users or mail contacts. Mail users and mail contacts are similar because both have external email addresses and contain information about people outside the Exchange Online organization. The main difference is mail users have user IDs that can be used to sign in to the Exchange Online organization. When an admin changes a per-recipient setting, it overrides settings that a user sets for that recipient. For more information about the admin settings, see [Manage mail users](../recipients-in-exchange-online/manage-mail-users) and [Manage mail contacts](../recipients-in-exchange-online/manage-mail-contacts).

Users can control the following settings:

- **Outlook settings**: In Outlook, you can set the message formatting and encoding options described in the following list:

    - **Message format**: You can set the default message format for all messages. You can override the default message format as you compose a specific message.
    - **Internet message format**: You can control whether TNEF messages are sent to remote recipients or whether they are first converted to a more compatible format. You can also specify various message encoding options for messages sent to remote recipients. These settings don't apply to messages sent to recipients in the Exchange Online organization.
    - **Internet recipient message format**: You can control whether TNEF messages are sent to specific recipients or whether they are first converted to a more compatible format. You can set the options for specific contacts in your Contacts folder, and you can override these options for a specific recipient in the To, Cc, or Bcc fields as you compose a message. These options aren't available for recipients in the Exchange Online organization.
    - **Internet recipient message encoding options**: You can control the MIME or plain text encoding options for specific contacts in your Contacts folder, and you can override these options for a specific recipient in the To, Cc, or Bcc fields as you compose a message. These options aren't available for recipients in the Exchange Online organization.
    - **International options**: You can control the character sets used in messages.

    For more information about Outlook settings, see [Change the message format in Outlook](https://support.microsoft.com/office/338a389d-11da-47fe-b693-cf41f792fefa).
- **Outlook on the web settings**: You can set the default message format for all messages. You can override the default message format as you compose a specific message.