---
layout: Conceptual
title: POP3 and IMAP4 in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/pop3-and-imap4/pop3-and-imap4
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: 'Summary: An overview of POP3 and IMAP4 in Exchange Online, and the differences between them.'
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: fce4cf21-02b4-4b42-82c8-ddb3c7eed4dc
ms.reviewer: akprakash
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2023-10-31T00:00:00.0000000Z
locale: en-us
document_id: 64383249-903c-6cc5-83e1-93e0eb8ba128
document_version_independent_id: d93c4ce8-4bf4-15d0-b3ba-3d3eb11ebb37
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/pop3-and-imap4/pop3-and-imap4.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/pop3-and-imap4/pop3-and-imap4
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/pop3-and-imap4/pop3-and-imap4.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: a3285ed3-0f8b-01bf-c5ca-e9f181c89f4d
---

# POP3 and IMAP4 in Exchange Online | Microsoft Learn

By default, POP3 and IMAP4 are enabled for all users in Exchange Online.

- To enable or disable POP3 and IMAP4 for individual users, see [Enable or Disable POP3 or IMAP4 access for a user](enable-or-disable-pop3-or-imap4-access).
- To customize the POP3 or IMAP4 settings for a user, see [Set POP3 or IMAP4 settings for a user](pop3-or-imap4-settings).

Note

If you've enabled *security defaults* in your organization, POP3 and IMAP4 are automatically disabled in Exchange Online. For more information, see [Security defaults in Microsoft Entra ID](/en-us/entra/fundamentals/security-defaults).

To protect your Exchange Online tenant from brute force or password spray attacks, your organization will need to [Disable Basic authentication in Exchange Online](../disable-basic-authentication-in-exchange-online) and only use [Modern authentication for Outlook in Exchange Online](../enable-or-disable-modern-authentication-in-exchange-online). Disabling Basic authentication will block legacy protocols, such as POP and IMAP.

Users can use any email programs that support POP3 and IMAP4 to connect to Exchange Online (for example, Outlook, Windows Mail, and Mozilla Thunderbird). The features supported by each email client programs vary. For information about features offered by specific POP3 and IMAP4 client programs, see the documentation that's included with each application.

POP3 and IMAP4 provide access to the basic email features of Exchange Online and allow for offline email access, but don't offer rich email, calendaring, and contact management, or other features that are available when users connect with Outlook, Exchange ActiveSync, Outlook on the web (formerly known as Outlook Web App), or Outlook Voice Access.

Note

Each time a person accesses a POP-based or IMAP-based email program to open his or her Microsoft 365 or Office 365 email, that user will experience a delay of several seconds. The delay results from using a proxy server, which introduces an additional hop for authentication. The proxy server first looks up the assigned pod server (client access server) and then authenticates against that.

## Settings users use to set up POP3 or IMAP4 access to their Exchange Online mailboxes

After you enable POP3 and IMAP4 client access, you have to give users the information in the following table so that they can connect their email programs to their Exchange Online mailboxes.

POP3 and IMAP4 email programs don't use POP3 and IMAP4 to send messages to the email server. Email programs that use POP3 and IMAP4 rely on SMTP to send messages.

| Protocol | Server name | Port | Encryption method |
| --- | --- | --- | --- |
| POP3 | Outlook.office365.com | 995 | SSL/TLS |
| IMAP4 | Outlook.office365.com | 993 | SSL/TLS |
| SMTP | Smtp.office365.com | 587 | STARTTLS |

## Understanding the differences between POP3 and IMAP4

By default, POP3 clients remove downloaded messages from the email server. This behavior makes it difficult to access email on multiple computers, since downloaded messages are stored on the local computer. But, you can typically configure a POP3 client to keep copies of downloaded messages on the server.

POP3 client programs download messages to a single folder on the client computer (typically, the Inbox). POP3 can't synchronize multiple folders on the email server with multiple folders on the client computer. POP3 also doesn't support public folder access.

IMAP4 clients are much more flexible and generally offer more features than POP3 clients. By default, IMAP4 clients don't remove downloaded messages from the email server. This behavior makes it easy to access email message from multiple computers.

IMAP4 clients support creating and accessing multiple email folders on the email server. For example, most IMAP4 clients can be configured to keep a copy of sent items on the server so these messages are accessible from any computer.

IMAP4 supports additional features that are supported by most IMAP4 clients (for example, viewing message senders and subjects before downloading the entire message).

## Send and receive options for POP3 and IMAP4 email programs

POP3 and IMAP4 clients let users choose when they want to connect to the email server to send and receive email. This section discusses some of the most common connectivity options and provides some factors your users should consider when they choose connection options available in their POP3 and IMAP4 email clients.

### Common configuration settings

Three of the most common connection settings that can be set on the POP3 or IMAP4 client application are:

- To send and receive messages every time the email application is started. When this option is used, mail is sent and received only on starting the email application.
- To send and receive messages manually. When this option is used, messages are sent and received only when the user clicks a send-and-receive option in the client user interface.
- To send and receive messages every set number of minutes. When this option is used, the client application connects to the server every set number of minutes to send messages and download any new messages.

For information about how to configure these settings for the email application that you use, see the Help documentation that's provided with the email application.

### Considerations when selecting send and receive options

The default setting on some email programs is to not keep a copy of messages on the server after they're retrieved. If the user wants to access messages from multiple email programs or devices, they should keep a copy of messages on the server.

For always-connected clients, the user might configure the email application to send and receive messages every set number of minutes. Connecting to the email server at frequent intervals lets the user keep the email application up-to-date with the most current information on the server.

However, if the client isn't always connected to the internet, the user might configure the email application to send and receive messages manually.

Note

If the IMAP4 client supports the IMAP4 IDLE command, email transfers to and from the Exchange Online mailbox might occur in nearly real time.