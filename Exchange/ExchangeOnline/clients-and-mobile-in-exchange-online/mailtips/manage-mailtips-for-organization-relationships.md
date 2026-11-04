---
layout: Conceptual
title: Manage MailTips for organization relationships in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/mailtips/manage-mailtips-for-organization-relationships
Manager: dansimp
ms.subservice: outlook-services
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: You can use Exchange Online PowerShell to configure custom settings for MailTips between various organizations.
ms.topic: how-to
author: alexcotsalas
ms.author: alexcotsalas
ms.assetid: 6e6b48ef-c41c-47ad-8063-66901765c2a5
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 19084361-4a5a-7a61-d75d-35963abce21d
document_version_independent_id: 07c12ea9-cc7b-719a-8538-c6c0fadec1b7
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/mailtips/manage-mailtips-for-organization-relationships.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/mailtips/manage-mailtips-for-organization-relationships
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/mailtips/manage-mailtips-for-organization-relationships.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: 1e094f00-5fb0-b47f-03ad-e05ab65eae26
---

# Manage MailTips for organization relationships in Exchange Online | Microsoft Learn

You can use Exchange Online PowerShell to configure custom settings for MailTips between various organizations.

By establishing an organizational relationship, you can enhance the user experience for both organizations by sharing free/busy data, configuring secure message flow, and enabling message tracking. For more information about organizational relationships, see [MailTips over organization relationships](mailtips-over-organization-relationships).

You can use various settings to control how MailTips are used between two organizations that have established an organizational relationship. The procedures in this section illustrate these various controls. In all examples, the on-premises organization is contoso.com, the remote organization is online.contoso.com, and the organizational relationship is named Contoso Online.

You use the **Set-OrganizationRelationship** cmdlet to configure these settings.

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "MailTips" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- You can only use Exchange Online PowerShell to perform this procedure.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to enable or disable MailTips between two organizations

This example configures the organizational relationship so that MailTips are returned to senders in the remote organization when composing messages to recipients in your organization.

```PowerShell
Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $true
```

This example configures the organizational relationship to prevent MailTips from being returned to senders in the remote organization when composing messages to recipients in your organization.

```PowerShell
Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $false
```

For detailed syntax and parameter information, see [Set-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/set-organizationrelationship).

## Use Exchange Online PowerShell to configure which MailTips are returned to the remote organization

For each organizational relationship, you can determine which set of MailTips are returned to senders in the other organization. This example configures the organizational relationship so that all MailTips are returned.

```PowerShell
Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel All
```

This example configures the organizational relationship so that only the Automatic Replies, Oversize Message, Restricted Recipient, and Mailbox Full MailTips are returned.

```PowerShell
Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel Limited
```

This example configures the organizational relationship so that no MailTips are returned.

Note

Don't use this method to disable MailTips for this relationship. To disable MailTips, set the *MailTipsAccessEnabled* parameter to `$false`.

```PowerShell
Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel None
```

For detailed syntax and parameter information, see [Set-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/set-organizationrelationship).

## Use Exchange Online PowerShell to configure a specific group of users for whom recipient-specific MailTips are returned

You can restrict the return of recipient-specific MailTips to a specific group of users. By default, when you enable MailTips for an organizational relationship, the following recipient-specific MailTips are returned for all users:

- Automatic Replies
- Mailbox Full
- Custom MailTip

You can specify a MailTips access group on the organizational relationship. After you specify a group, the recipient-specific MailTips are returned only for mailboxes, mail contacts, and mail users that are members of that group. This example configures the organizational relationship to return recipient-specific MailTips only for members of the ShareMailTips@contoso.com group.

```PowerShell
Set-OrganizationRelationship "Contoso Online" -MailTipsAccessScope ShareMailTips@contoso.com
```

For detailed syntax and parameter information, see [Set-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/set-organizationrelationship).