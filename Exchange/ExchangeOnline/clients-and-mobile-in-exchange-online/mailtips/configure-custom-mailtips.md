---
layout: Conceptual
title: Configure custom MailTips for recipients in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/mailtips/configure-custom-mailtips
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
description: 'MailTips are informative messages displayed to users in the InfoBar in Outlook on the web and Microsoft Outlook 2010 or later when a user does any of the following while composing an e-mail message:'
ms.topic: how-to
author: officedocspr
ms.author: odocspr
ms.assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2024-06-21T00:00:00.0000000Z
locale: en-us
document_id: e4cf8892-771b-e40d-2036-79672516de05
document_version_independent_id: fe2f2228-34b5-e10f-bca9-ce76deefd2d8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/mailtips/configure-custom-mailtips.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/mailtips/configure-custom-mailtips
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/mailtips/configure-custom-mailtips.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: fef2b0d5-5f3b-309d-6e5d-3c134201e4ee
---

# Configure custom MailTips for recipients in Exchange Online | Microsoft Learn

MailTips are informative messages displayed to users in the InfoBar in Outlook on the web (formerly known as Outlook Web App) and Microsoft Outlook 2010 or later when a user does any of the following steps while composing an email message:

- Add a recipient
- Add an attachment
- Reply or Reply all
- Open a message from the Drafts folder that's already addressed to recipients

In addition to the built-in MailTips that are available, you can create custom MailTips for all types of recipients. For more information about the built-in MailTips, see [MailTips](mailtips).

## What do you need to know before you begin?

- Estimated time to complete: 10 minutes
- You need to be assigned permissions before you can perform this procedure or procedures. For information on the permissions you need, see the "MailTips" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- You can configure the primary MailTip in the Exchange admin center (EAC) or in Exchange Online PowerShell. However, you can only configure additional MailTip translations in Exchange Online PowerShell.
- When you add a MailTip to a recipient, two things happen:

    - HTML tags are automatically added to the text. For example, if you enter the text `This mailbox is not monitored`, the MailTip automatically becomes `<html><body>This mailbox is not monitored</body></html>`. Additional HTML tags in the MailTip aren't supported.
    - The text is automatically added to the *MailTipTranslations* property of the recipient as the default value. If you modify the MailTip text, the default value is automatically updated in the *MailTipTranslations* property.
- The length of a MailTip can't exceed 175 displayed characters.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Configure MailTips for recipients

### Use the EAC to configure MailTips for recipients

1. In the [EAC](https://admin.exchange.microsoft.com), go to **Recipients** &gt; **Mailboxes**. Or, use [**Manage mailboxes**](https://admin.exchange.microsoft.com/#/mailboxes).
2. Select any of the following recipient tabs based on the recipient type:

    - **Mailboxes**
    - **Resources**
    - **Contacts**
3. On the chosen tab, select the recipient you want to modify.
4. Select an individual mailbox by clicking anywhere in the row other than the button option that appears in the blank area next to the **Display name** column.
5. In the **User mailbox** details flyout that opens, go to **Others** &gt; **Manage mail tip**.

    Important

    If you select the **Contacts** recipient tab, you must select **General** &gt; **Manage mail tip** in the details flyout that opens, to configure the mailtips.
6. Enter the text for the MailTip. When you're finished, select **Save**.

### Use Exchange Online PowerShell to configure MailTips for recipients

To configure a MailTip for a recipient, use the following syntax:

```PowerShell
Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"
```

*&lt;RecipientType&gt;* can be any type of recipient. For example, `Mailbox`, `MailUser`, `MailContact`, `DistributionGroup`, or `DynamicDistributionGroup`.

For example, suppose you have a mailbox named "Help Desk" for users to submit support requests, and the promised response time is **2 hours**. To configure a custom MailTip that explains this, run the following command:

```PowerShell
Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."
```

## Use Exchange Online PowerShell to configure additional MailTips in different languages

To configure additional MailTip translations without affecting the existing MailTip text or other existing MailTip translations, use the following syntax:

```PowerShell
Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}
```

*&lt;culture&gt;* is a valid ISO 639 two-letter culture code associated with the language.

For example, suppose the mailbox named "Notifications" currently has the MailTip "This mailbox is not monitored." To add the Spanish translation, run the following command:

```PowerShell
Set-Mailbox -MailTipTranslations @{Add="ES:Esta caja no se supervisa."}
```

## How do you know this worked?

To verify that you have successfully configured a MailTip for a recipient, do the following steps:

1. In Outlook on the web or Outlook 2010 or later, compose an email message addressed to the recipient, but don't send it.
2. Verify whether the MailTip appears in the InfoBar.
3. If you configured additional MailTip translations, compose the message in Outlook on the web where the language setting matches the language of the MailTip translation to verify the results.