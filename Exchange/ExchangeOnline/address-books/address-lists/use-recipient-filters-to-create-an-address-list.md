---
layout: Conceptual
title: Recipient filters for address lists in Exchange Online PowerShell in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-lists/use-recipient-filters-to-create-an-address-list
Manager: serdars
ms.subservice: exo-address-books
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: This topic describes the recipient filter options that admins can use in custom address lists and global address lists (GALs) in Exchange Online.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
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
document_id: ba24baca-d249-6b19-3530-9549c77e51d2
document_version_independent_id: 4bdaed59-8c12-77fb-ab2d-2b9b27932484
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-lists/use-recipient-filters-to-create-an-address-list.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-lists/use-recipient-filters-to-create-an-address-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-lists/use-recipient-filters-to-create-an-address-list.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: a1d87856-2569-5717-0f87-0bb77435d309
---

# Recipient filters for address lists in Exchange Online PowerShell in Exchange Online | Microsoft Learn

Recipient filters identify the recipients that are included in address lists and GALs. There are two basic options: **precanned recipient filters** and **custom recipient filters**. These are basically the same recipient filtering options that are used by dynamic distribution groups and email address policies.

- **Precanned recipient filters**

    - Uses the required *IncludedRecipient* parameter with the `AllRecipients` value *or* one or more of the following values: `MailboxUsers`, `MailContacts`, `MailGroups`, `MailUsers`, or `Resources`. You can specify multiple values separated by commas.
    - You can also use any of the optional *Conditional* filter parameters: *ConditionalCompany*, *ConditionalCustomAttribute[1to15]*, *ConditionalDepartment*, and *ConditionalStateOrProvince*.

    You specify multiple values for a *Conditional* parameter by using the syntax `"<Value1>","<Value2>"...`. Multiple values of the same property implies the **or** operator. For example, "Department equals Sales or Marketing or Finance".
- **Custom recipient filters**: Uses the required *RecipientFilter* parameter with an OPATH filter.

    - The basic OPATH filter syntax is `"<Property1> -<Operator> '<Value1>' <Property2> -<Operator> '<Value2>'..."`.
    - Double quotation marks `" "` are required around the whole OPATH filter. Although the filter is a string (not a system block), you can also use braces `{ }`, but only if the filter doesn't contain variables that require expansion.
    - Hyphens (`-`) are required before all operators. Here are some of the most frequently used operators:
    - `and`, `or`, and `not`.
    - `eq` and `ne` (equals and does not equal; not case-sensitive).
    - `lt` and `gt` (less than and greater than).
    - `like` and `notlike` (string contains and does not contain; requires at least one wildcard in the string. For example, `"Department -like 'Sales*'"`.
    - Use parentheses to group `<Property> -<Operator> '<Value>'` statements together in complex filters. For example, `"(Department -like 'Sales*' -or Department -like 'Marketing*') -and (Company -eq 'Contoso' -or Company -eq 'Fabrikam')"`. Exchange stores the filter in the **RecipientFilter** property with each individual statement enclosed in parentheses, but you don't need to enter them that way.
    - For more information, see [Additional OPATH syntax information](/en-us/powershell/exchange/recipient-filters#additional-opath-syntax-information).

For more information about address lists, see [Address lists in Exchange Online](address-lists).

For address list procedures that use recipient filters, see [Address list procedures in Exchange Online](address-list-procedures).