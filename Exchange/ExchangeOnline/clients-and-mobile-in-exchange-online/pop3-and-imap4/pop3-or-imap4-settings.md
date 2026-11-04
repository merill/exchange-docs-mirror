---
layout: Conceptual
title: Set POP3 or IMAP4 settings for a user in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/pop3-and-imap4/pop3-or-imap4-settings
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
ms.custom:
- has-azure-ad-ps-ref
description: You use the Set-CASMailbox cmdlet to configure the PO3 and IMAP4 options for each user. The configuration options are described in the following table.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: bf4ca453-e79c-4b87-a9a5-3ae1b21181e2
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-26T00:00:00.0000000Z
locale: en-us
document_id: 8b99421b-d435-6839-a32c-f3b1a0b32861
document_version_independent_id: b88aeb4b-b606-421b-3f99-d2a74aef3d3a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/pop3-and-imap4/pop3-or-imap4-settings.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/pop3-and-imap4/pop3-or-imap4-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/pop3-and-imap4/pop3-or-imap4-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: ed179219-f543-e05d-454a-b79832d9e268
---

# Set POP3 or IMAP4 settings for a user in Exchange Online | Microsoft Learn

You use the **Set-CASMailbox** cmdlet to configure the PO3 and IMAP4 options for each user. The configuration options are described in the following table.

| Parameter | Description | Values |
| --- | --- | --- |
| *PopForceICalForCalendarRetrievalOption* *ImapForceICalForCalendarRetrievalOption* | Sets the preferred format for meeting requests.  By default, meeting requests appear as Outlook on the web (formerly known as Outlook Web App) links. You can change them to iCal format. | `$true`: Meeting requests are all Outlook on the web links `$false`: Meeting requests are all iCal format |
| *PopSuppressReadReceipt* *ImapSuppressReadReceipt* | Sets whether to send read receipts when a message is downloaded and again when it is opened or just when the message is opened  By default, if a read receipt is requested, two read receipts are sent: one when a user downloads a message and another when the user opens the message. You can change it so that only one read receipt is sent: when the user opens the message. | `$false`: POP3 or IMAP4 users are sent a read receipt each time a recipient downloads a message. Users are also sent a read receipt when the user opens the message. This is the default setting. `$true`: POP3 or IMAP4 users that use the **send read receipt for messages I send** option in their email client programs receive a read receipt only when the recipient opens the message. |
| *PopMessagesRetrievalMimeFormat* *ImapMessagesRetrievalMimeFormat* | Sets the preferred format for received messages.  The default is to use the best format based on the message. | Use a numeral or a text value. `0` or `TextOnly`: Text only `1` or `HtmlOnly`: HTML `2` or `HtmlAndTextAlternative`: HTML and alternative text `3` or `TextEnriched`: Enriched text `4` or `TextEnrichedAndTextAlternative`: Enriched text and alternative text `5` or `BestBodyFormat`: Best body format. This is the default value. `6` or `Tnef`: Transport-Neutral Encapsulation Format (TNEF). Also known as rich text format, Outlook rich text format, or MAPI rich text format. |
| *PopEnableExactRFC822Size* *ImapEnableExactRFC822Size* | Sets whether to calculate the exact size of messages.  Changing this value is not recommended unless the default value causes problems for your email client. By default, the estimated message size, rather than the exact message size, is sent to the email client. | `$true`: Use actual message size. `$false`: Use estimated message size. This is the default. |

For additional information related to POP3 and IMAP4, see [POP3 and IMAP4](pop3-and-imap4).

## What do you need to know before you begin?

- Estimated time to finish each procedure: five minutes.
- You can only use Exchange Online PowerShell to perform this procedure. To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "POP3 and IMAP4 settings" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to set the meeting request format for a POP3 or IMAP4 user

The following example sets all meeting requests in incoming mail to USER01 to iCal format for a POP3 user.

```PowerShell
Set-CASMailbox USER01 -PopUseProtocolDefaults $false -PopForceICalForCalendarRetrievalOption $true
```

The following example sets all meeting requests in incoming mail to USER01 to iCal format for an IMAP4 user.

```PowerShell
Set-CASMailbox USER01-ImapUseProtocolDefaults $false -ImapForceICalForCalendarRetrievalOption $true
```

### How do you know this worked?

To verify that you successfully set the meeting request format for a POP3 or an IMAP4 user, run the following command in Exchange Online PowerShell and verify that the values displayed are the values that you configured:

```PowerShell
Get-CASMailbox USER01 | format-list *ForceIcal*,*UseProtocolDefaults
```

## Use Exchange Online PowerShell to set the suppress read receipt option for a POP3 or IMAP4 user

The following example sets it up so that the POP3 sender receives a read receipt only when the message is opened.

```PowerShell
Set-CASMailbox USER01 -PopUseProtocolDefaults $false -PopSuppressReadReceipt $true
```

The following example sets it up so that the IMAP4 sender receives a read receipt only when the message is opened.

```PowerShell
Set-CASMailbox USER01 -ImapUseProtocolDefaults $false -ImapSuppressReadReceipt $true
```

### How do you know this worked?

To verify that you successfully set the read receipt option for a POP3 or an IMAP4 user, run the following command in Exchange Online PowerShell and verify that the values displayed are the values that you configured:

```PowerShell
Get-CASMailbox USER01 | format-list *SuppressReadReceipt,*UseProtocolDefaults
```

## Use Exchange Online PowerShell to set the message retrieval format for a POP3 or IMAP4 user

The following example sets the message retrieval format to text only for POP3 access for `USER01`.

```PowerShell
Set-CASMailbox USER01 -PopUseProtocolDefaults $false -PopMessagesRetrievalMimeFormat TextOnly
```

The following example sets the message retrieval format to text only for IMAP4 access for `USER01`.

```PowerShell
Set-CASMailbox USER01 -ImapUseProtocolDefaults $false -ImapMessagesRetrievalMimeFormat TextOnly
```

### How do you know this worked?

To verify that you successfully set the message retrieval format for a POP3 or an IMAP4 user, run the following command in Exchange Online PowerShell and verify that the values displayed are the values that you configured:

```PowerShell
Get-CASMailbox USER01 | format-list *MessagesRetrievalMimeFormat,*UseProtocolDefaults
```

## Use Exchange Online PowerShell to set the message size calculation for a POP3 or IMAP4 user

This example calculates the exact size of POP messages for USER01.

Important

Set the *PopEnableExactRFC822Size* parameter to `$true` only if the POP client doesn't work for this user.

```PowerShell
Set-CASMailbox USER01 -PopUseProtocolDefaults $false -PopEnableExactRFC822Size $true
```

This example calculates the exact size of IMAP messages for USER01.

Important

Set the *ImapEnableExactRFC822Size* parameter to `$true` only if the IMAP client doesn't work for this user.

```PowerShell
Set-CASMailbox USER01 -ImapUseProtocolDefaults $false -ImapEnableExactRFC822Size $true
```

### How do you know this worked?

To verify that you successfully set the message size calculation for a POP3 or IMAP4 user, run the following command in Exchange Online PowerShell and verify that the values displayed are the values that you configured::

```PowerShell
Get-CASMailbox USER01 | format-list *EnableExact*,*UseProtocolDefaults
```

## For more information

[Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell)

[POP3 and IMAP4](pop3-and-imap4)

[Enable or Disable POP3 or IMAP4 access for a user](enable-or-disable-pop3-or-imap4-access)

[Set-CASMailbox](/en-us/powershell/module/exchangepowershell/set-casmailbox)