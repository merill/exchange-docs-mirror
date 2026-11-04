---
layout: Conceptual
title: Managing email apps for user mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/managing-email-apps-for-user-mailboxes
Manager: serdars
ms.subservice: exo-manageability
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
description: This article explains how to enable or disable Exchange ActiveSync, MAPI, and Outlook on the web for a mailbox using the EAC or Exchange Online PowerShell.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-17T00:00:00.0000000Z
locale: en-us
document_id: 132cea42-61d6-c845-e11d-d73fa36d08d1
document_version_independent_id: dfe7cb45-b26f-ee36-b694-57e54309d13c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/managing-email-apps-for-user-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-user-mailboxes/managing-email-apps-for-user-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/managing-email-apps-for-user-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 1c74ca91-3824-c6c5-9371-9f5c463fcc5c
---

# Managing email apps for user mailboxes | Microsoft Learn

## Enable or disable email apps for user mailboxes in Exchange Online

You can use the Exchange admin center (EAC) or Exchange Online PowerShell to enable or disable the following email apps for user mailboxes:

- **Microsoft Exchange ActiveSync**: Exchange ActiveSync is a client protocol that lets users synchronize a mobile device with their Exchange mailbox. Exchange ActiveSync is enabled by default when a user mailbox is created. To learn more, see [Exchange ActiveSync in Exchange Online](../../clients-and-mobile-in-exchange-online/exchange-activesync/exchange-activesync).
- **MAPI**: When MAPI is enabled, a user's mailbox can be accessed by Outlook or other MAPI email clients.
- **Outlook on the web**: When Outlook on the web is enabled, a user can use Outlook on the web to access their mailbox.
- **IMAP** and **POP3**: These are older email protocols that Exchange supports. When enabled, users can use email clients that support these protocols to access their mailbox in Exchange.

Note

Support for Outlook on the web and MAPI, POP3, and IMAP4 email clients is enabled by default when a user mailbox is created.

Outlook on the web is required for the Share to Outlook feature to work in Microsoft Teams and for the new Outlook.

### What do you need to know before you begin?

- Estimated time to complete: 2 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mobile devices" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the Exchange admin center to enable or disable email apps

1. In the EAC, navigate to **Recipients** &gt; **Mailboxes**.
2. In the list of user mailboxes, select the mailbox that you want to enable or disable email apps for. A display pane is shown for the selected user mailbox.
3. On the **General** tab, under **Email apps & mobile devices**, select the **Manage email apps settings** link.
4. In the **Manage settings for email apps** display pane, set **Outlook desktop (MAPI)**, **Mobile (Exchange ActiveSync)**, **IMAP**, **POP3** and **Outlook on the web** to **Enabled** or **Disabled**
5. Select **Save** to save your change. A message **Email app settings updated successfully** is displayed. Select **Close** to exit.

## Use Exchange Online PowerShell to enable or disable email apps

This example disables Exchange ActiveSync for the mailbox of Yan Li.

```PowerShell
Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false
```

This example disables MAPI for the mailbox of Ken Sanchez.

```PowerShell
Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $true
```

For detailed syntax and parameter information, see [Set-CASMailbox](/en-us/powershell/module/exchangepowershell/set-casmailbox).