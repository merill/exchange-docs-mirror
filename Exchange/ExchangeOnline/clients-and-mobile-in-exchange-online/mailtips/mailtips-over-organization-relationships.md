---
layout: Conceptual
title: MailTips over organization relationships in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/mailtips/mailtips-over-organization-relationships
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
description: Microsoft Exchange Server allows you to configure organization relationships with Microsoft Exchange Online or other Exchange organizations. Establishing an organization relationship allows you to enhance the user experience when dealing with the other organization. For example, you can share free or busy data, configure secure message flow, and enable message tracking across both organizations.
ms.topic: article
author: alexcotsalas
ms.author: alexcotsalas
ms.assetid: 1784256f-abe1-4503-b8c4-26d544b73452
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
document_id: c69d5345-2783-e058-ca85-f3742fbe84a8
document_version_independent_id: d02cf29b-7ade-a56e-800a-2986c59c22c4
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/mailtips/mailtips-over-organization-relationships.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/mailtips/mailtips-over-organization-relationships
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/mailtips/mailtips-over-organization-relationships.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: a78a3555-e6b2-c44a-c72f-f9ce3d600784
---

# MailTips over organization relationships in Exchange Online | Microsoft Learn

Exchange Online allows you to configure organization relationships with other Exchange organizations. Establishing an organization relationship allows you to enhance the user experience when dealing with the other organization. For example, you can share free or busy data, configure secure message flow, and enable message tracking across both organizations.

## Controlling the MailTips access level

You may want to restrict certain types of MailTips. You can either allow all MailTips to be returned or allow only a limited set that would prevent NDRs. You can configure this setting with the *MailTipsAccessLevel* parameter on the **Set-OrganizationRelationship** cmdlet. The following table shows which MailTips are returned over the organization relationship.

| MailTip | Is the MailTip available when the access level is set to All? | Is the MailTip available when the access level is set to Limited? |
| --- | --- | --- |
| Large Audience | Yes | No |
| Automatic Replies | Yes <br> If the remote domain of the recipient is specified as internal, the internal automatic reply is displayed. Otherwise, the external automatic reply is displayed. | Yes <br> The external automatic reply is displayed. |
| Moderated Recipient | Yes | No |
| Oversize Message | Yes | Yes |
| Restricted Recipient | Yes | Yes |
| Mailbox Full | Yes | No |
| Custom MailTips | Yes | No |
| External Recipients | Yes <br> If the remote domain of the recipient is specified as internal, this MailTip is suppressed. Otherwise, the external MailTip is returned. | Yes <br> If the remote domain of the recipient is specified as internal, this MailTip is suppressed. Otherwise, the external MailTip is returned. |

For detailed steps about how to configure MailTips access levels, see [Manage MailTips for organization relationships](manage-mailtips-for-organization-relationships).

## Controlling the MailTips access scope

When you enable MailTips over an organization relationship and set the access level to `All`, the recipient-specific MailTips, Mailbox Full, Automatic Replies, and custom MailTips, are returned for all users. However, you may only want to allow these MailTips for a specific set of users. For example, if you set up an organization relationship with a partner, you may want to allow these MailTips only for the users that work with that partner.

To achieve this, you need to first create a group and add all users for whom you want to share recipient-specific MailTips to that group. You can then specify that group on the organization relationship.

After you implement this restriction, your Client Access servers will first verify whether the recipient for whom they received a MailTips query is part of this group. If the recipient is a member of this group, the Client Access servers will proxy back all MailTips including the recipient-specific MailTips. Otherwise they won't include the recipient-specific MailTips in their response.

For detailed steps about how to configure MailTips access levels, see [Manage MailTips for organization relationships](manage-mailtips-for-organization-relationships).