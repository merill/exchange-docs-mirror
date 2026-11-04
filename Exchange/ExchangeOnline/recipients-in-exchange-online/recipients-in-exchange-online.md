---
layout: Conceptual
title: Recipients in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/recipients-in-exchange-online
Manager: serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Admin can learn about the different recipient types in Exchange Online.
ms.topic: how-to
author: Swatyario
ms.author: adbhale
ms.assetid: 50d16941-5cd7-435d-8715-e2b69f8410ab
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
- essentials-manage
audience: ITPro
ms.service: exchange-online
ms.custom: seo-marvel-apr2020
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: c3247f38-1977-e869-cb49-968c2a887f7d
document_version_independent_id: e7ea33c2-c985-edb9-4669-4dbb6da2feeb
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/recipients-in-exchange-online.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/recipients-in-exchange-online
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/recipients-in-exchange-online.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 1f4a4541-ddca-4a10-eaec-d0dde96739cb
---

# Recipients in Exchange Online | Microsoft Learn

A recipient is any mail-enabled object in Exchange Online that can receive email messages. Exchange Online includes several recipient types. Each recipient type is identified in the Exchange admin center (EAC) and has a unique value in the *RecipientTypeDetails* property in Exchange Online PowerShell.

Note

In Exchange Online, the new EAC enhances the admin experience with a different look and feel. The **Mailboxes** and **Shared** mailboxes tabs under **Recipients** in the Classic EAC are now merged into a single **Mailboxes** tab under **Recipients** in the new EAC. On the **Mailboxes** tab, you can view shared mailboxes and user mailboxes under one list view. For more information, see [Exchange admin center in Exchange Online](../exchange-admin-center).

The following table describes the different types of recipients in Exchange Online and provides links to articles that explain how to manage and configure them.

| Recipient type | Description |
| --- | --- |
| **Users** |  |
| User mailbox | A mailbox that's assigned to an individual user in your Exchange Online organization. A mailbox contains the user's email messages, calendar items, contacts, tasks, and other important business data. <br>[Create user mailboxes in Exchange Online](create-user-mailboxes). |
| Shared mailbox | A mailbox that's designed for access by multiple users. <br> Shared mailboxes do not require licenses in Exchange Online. <br><br>[Shared mailboxes in Exchange Online](../collaboration-exo/shared-mailboxes) |
| Mail contact | A mail contact contains information about a person who's outside of your Exchange Online organization. A mail contact has an external email address, but the mail contact is visible in your organization's shared address book (also known as the global address list or GAL) and other address lists. <br>[Manage mail contacts](manage-mail-contacts) |
| Mail user | A mail user (also known as a *mail-enabled user*) is similar to a mail contact in that it represents a user with an external email address and is visible in your organization's shared address book and other address lists. However, a mail user also has a user account in your organization, and you can assign permissions to the mail user. <br> Mail users do not require licenses in Exchange Online. <br><br>[Manage mail users](manage-mail-users) |
| **Resources** |  |
| Room mailbox | A type of resource mailbox that's assigned to a meeting location, such as a conference room, auditorium, or training room. Room mailboxes can be included as resources in meeting requests. <br>[Manage resource mailboxes](manage-resource-mailboxes) |
| Equipment mailbox | A type of resource mailbox that's assigned to a resource that's not location-specific, such as a portable computer, projector, microphone, or a company car. Equipment mailboxes can be included as resources in meeting requests. <br>[Manage resource mailboxes](manage-resource-mailboxes) |
| **Groups** |  |
| Distribution group | Distribution groups (also known as *distribution lists*) provide a single point of contact for delivering email to the members of the group. <br>[Create and manage distribution groups](manage-distribution-groups/manage-distribution-groups). |
| Mail-enabled security group | Like a distribution group, a mail-enabled security group provides a single point of contact for delivering email to the members of the group. However, a mail-enabled security group is also a *security principal*, which means you can assign permissions to the group that affect all group members who are also security principals (user mailboxes, mail users, other mail-enabled security groups, etc.). <br>[Manage mail-enabled security groups](manage-mail-enabled-security-groups). |
| Dynamic distribution group | A dynamic distribution group uses recipient filters and conditions to periodically calculate the membership of the group. <br>[Manage dynamic distribution groups](manage-dynamic-distribution-groups/create-manage-dynamic-distribution-groups) |
| **Collaboration** |  |
| Microsoft 365 group | Microsoft 365 groups (formerly known as Office 365 groups), are used for collaboration between teams, both inside and outside your company, by providing group email and a shared workspace for conversations, files, and calendars. <br> For email, the benefit of a Microsoft 365 group over traditional groups is: the email history of the group is preserved. If a new user joins an old Microsoft 365 group, the entire email history of the group is available to them. <br><br>[Create and manage groups](create-and-manage-groups) |
| Mail-enabled public folder | A public folder is designed for shared access to collect, organize, and share information. <br>[Public folders in Microsoft 365, Office 365, and Exchange Online](../collaboration-exo/public-folders/public-folders) |