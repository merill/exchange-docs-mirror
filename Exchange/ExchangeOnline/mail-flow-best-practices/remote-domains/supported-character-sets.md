---
layout: Conceptual
title: Supported character sets for remote domains in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/remote-domains/supported-character-sets
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
description: MIME and non-MIME character sets that admins can configure in remote domains (message formatting settings for external domains) in Exchange Online
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 66023a62-1fd3-4019-be2b-4e7147db148a
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 8e9391f0-40d7-6884-60c3-039d32b3d92e
document_version_independent_id: 27a7b5e7-8875-f239-85a7-56304487d970
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/remote-domains/supported-character-sets.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/remote-domains/supported-character-sets
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/remote-domains/supported-character-sets.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 84d19d41-5721-e551-1c58-d664a93ae69b
---

# Supported character sets for remote domains in Exchange Online | Microsoft Learn

Remote domains define settings based on the destination domain of each email message. All organizations have a default remote domain named "Default" that's applied to the domain "\*". The default remote domain applies the same settings to all email messages regardless of the destination domain. However, you can configure specific settings for a specific destination domain.

For more information about remote domains, see [Remote domains in Exchange Online](remote-domains).

For remote domain procedures, see [Manage remote domains in Exchange Online](manage-remote-domains).

The following table describes the character sets that you can configure in remote domains.

## New Exchange admin center (EAC)

1. Navigate to **Mail flow** &gt; **Remote domains**. The **Remote domains** screen appears.
2. Click **+ Add a remote domain**.

    The **Name the domain** screen appears.
3. Provide a name for the domain and the remote domain in their respective text boxes.
4. Click **Next**. The **Email reply types** screen appears.
5. Configure the 'automatic email reply types' settings by choosing one of the following options:

    - **None**
    - **Allow only external out of office replies**
    - **Allow internal out of office replies**
6. Click **Next**. The **Message reporting** screen appears.
7. Configure the message-reporting settings by choosing the following options:

    - **Allow delivery options**
    - **Allow non-delivery options**
    - **Allow meeting forward notifications**

    Note

    You can choose one of more options.
8. Click **Next**. The **Text and character set** screen appears.
9. Configure the format and delivery method of email messages. Do this task by choosing any of the options in the following panes:

    - **Use rich-text format**
    - **Supported Character Set**
10. Click **Next**. The **Review** screen appears.
11. Review the settings configured and click **Save**. The new review domain is created successfully.

## Classic EAC

- Navigate to **Mail flow** &gt; **Remote domains**. Click **New**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.png) to create a new remote domain or select the existing remote domain and click **Edit**![Edit icon](../../exchangeonline/media/itpro_eac_editicon.png). In the settings window that opens, use the **MIME character set** and **Non-MIME character set** drop-down lists to select the character set.
- In Exchange Online PowerShell, use the value in the Name column in the following table for the *CharacterSet* parameter or *NonMimeCharacterSet* parameter on the [Set-RemoteDomain](/en-us/powershell/module/exchangepowershell/set-remotedomain) cmdlet.

    | Name | Description |
    | --- | --- |
    | big5 | Chinese Traditional (Big5) |
    | DIN\_66003 | German (IA5) |
    | euc-jp | Japanese (EUC) |
    | euc-kr | Korean (EUC) |
    | GB18030 | Chinese Simplified (GB18030) |
    | gb2312 | Chinese Simplified (GB2312) |
    | hz-gb-2312 | Chinese Simplified (HZ) |
    | iso-2022-jp | Japanese (JIS) |
    | iso-2022-kr | Korean (ISO) |
    | iso-8859-1 | Western European (ISO) |
    | iso-8859-2 | Central European (ISO) |
    | iso-8859-3 | Latin 3 (ISO) |
    | iso-8859-4 | Baltic (ISO) |
    | iso-8859-5 | Cyrillic (ISO) |
    | iso-8859-6 | Arabic (ISO) |
    | iso-8859-7 | Greek (ISO) |
    | iso-8859-8 | Hebrew (ISO) |
    | iso-8859-9 | Turkish (ISO) |
    | iso-8859-13 | Estonian (ISO) |
    | iso-8859-15 | Latin 9 (ISO) |
    | koi8-r | Cyrillic (KOI8-R) |
    | koi8-u | Cyrillic (KOI8-U) |
    | ks\_c\_5601-1987 | Korean (Windows) |
    | NS\_4551-1 | Norwegian (IA5) |
    | SEN\_850200\_B | Swedish (IA5) |
    | shift\_jis | Japanese (Shift-JIS) |
    | utf-8 | Unicode (UTF-8) |
    | windows-1250 | Central European (Windows) |
    | windows-1251 | Cyrillic (Windows) |
    | windows-1252 | Western European (Windows) |
    | windows-1253 | Greek (Windows) |
    | windows-1254 | Turkish (Windows) |
    | windows-1255 | Hebrew (Windows) |
    | windows-1256 | Arabic (Windows) |
    | windows-1257 | Baltic (Windows) |
    | windows-1258 | Vietnamese (Windows) |
    | windows-874 | Thai (Windows) |