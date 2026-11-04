---
layout: Conceptual
title: Collaboration in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/collaboration-exo
Manager: serdars
ms.subservice: exo-groups
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Microsoft 365 or Office 365 and Exchange Online provide several features that can help your end users easily collaborate in email.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 7d433daa-c68f-4441-b2f5-1280991185c2
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2026-09-08T00:00:00.0000000Z
locale: en-us
document_id: 4bd8e7d2-4bf8-46e2-480f-9eca0c71cb65
document_version_independent_id: 60583132-eadf-5119-fc52-495cec0ba1f5
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/collaboration-exo.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/collaboration-exo
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/collaboration-exo.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: fda6cfb4-bab5-5880-aa50-60389e372350
---

# Collaboration in Exchange Online | Microsoft Learn

Microsoft 365 or Office 365 and Exchange Online provide several features that can help your end users easily collaborate in email.

Each of these features, described in the following sections, has a different user experience and feature set and should be used based on what your users need to accomplish and what your organization can provide.

This topic compares these collaboration features to help you decide which features to offer your users.

## Public folders

Public folders are designed for shared access and provide an easy and effective way to collect, organize, and share information with other people in your workgroup or organization.

Public folders organize content in a deep hierarchy that's easy to browse. Users discover interesting and relevant content by browsing through branches of the hierarchy that are relevant to them. Users always see the full hierarchy in their Outlook folder view. Public folders are a great technology for distribution group archiving. A public folder can be mail-enabled and added as a member of the distribution group. Email sent to the distribution group is automatically added to the public folder for later reference. Public folders also provide simple document sharing and don't require SharePoint to be installed in your organization. Finally, end users can use public folders with the following supported Outlook clients: Outlook for Windows, Outlook for Mac, and Outlook on the web (formerly known as Outlook Web App), but with some limitations.

To learn more, see [Public folders in Microsoft 365 or Office 365 and Exchange Online](public-folders/public-folders).

## Shared mailboxes

A shared mailbox is a mailbox that multiple designated users can access to read and send email messages and to share a common calendar. Shared mailboxes can provide a generic email address (such as info@contoso.com or sales@contoso.com) that customers can use to inquire about your company. If the shared mailbox has the Send As permission assigned when a delegated user responds to the email message, it can appear as though the mailbox (for example, sales@contoso.com) is responding, not the actual user.

To learn more, see [Shared mailboxes in Exchange Online](shared-mailboxes).

## Groups

Groups (also called distribution groups) are a collection of two or more recipients that appears in the shared address book. When an email message is sent to a group, it's received by all members of the group. Distribution groups can be organized by a particular discussion subject (such as "Dog Lovers") or by users who share a common work structure that requires them to communicate frequently.

To learn more, see [Recipients in Exchange Online](../recipients-in-exchange-online/recipients-in-exchange-online).

## Which one to use?

The following table gives you a quick glance at each of the collaboration features to help you decide which one to use.

| - | Public folders | Shared mailboxes | Groups |
| --- | --- | --- | --- |
| **Type of group** | With the proper permissions, everyone in your organization can access and search public folders. Public folders are ideal for maintaining history or distribution group conversations. | Delegates working on behalf of a virtual identity, and they can respond to email as that shared mailbox identity. Example: support@tailspintoys.com | Users who need to send email to a group of recipients with a common interest or characteristic. |
| **Ideal group size** | Large | Small^1^ | Large |
| **Access** | Accessible by anyone in your organization. | Users can be granted Full Access and/or Send As permissions. If granted Full Access permissions, users must also add the shared mailbox to their Outlook profile to access the shared mailbox. | For distribution groups, members must be manually added. For dynamic distribution groups, members are added based on filtering criteria. |
| **Shared calendar?** | Yes | Yes | No |
| **Email arrives in user's personal Inbox?** | No. Email arrives in the public folder. | No. Email arrives in the Inbox of the shared mailbox. | Yes. Email arrives in the Inbox of a distribution group member. |
| **Supported clients** | Outlook 2010 or later  Outlook on the web | Outlook 2010 or later  Outlook on the web | Outlook 2010 or later  Outlook on the web |

Note

^1^ Depending on workload, the ideal group size may be very small (not more than 25). If more than a few users need to access a Shared mailbox at the same time, consider one of the other options.