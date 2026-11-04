---
layout: Conceptual
title: Turn on address book policy routing in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-book-policies/turn-on-address-book-policy-routing
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
description: Admins can learn how to turn on address book policy routing in Exchange Online to enable virtual organizations within an organization.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 5627b8ac-0551-4558-b3b6-25c402698426
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2025-07-22T00:00:00.0000000Z
locale: en-us
document_id: 6ea8ab60-59e5-200d-b048-9ff0d06c26f6
document_version_independent_id: 2dd67ab1-d489-3579-8922-db28f842ea32
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-book-policies/turn-on-address-book-policy-routing.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-book-policies/turn-on-address-book-policy-routing
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-book-policies/turn-on-address-book-policy-routing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: b3accc9b-f7f3-c678-f0f6-e71fb668031a
---

# Turn on address book policy routing in Exchange Online | Microsoft Learn

Address book policies (ABPs) allow you to segment users into specific groups to give them customized global address lists (GALs) in Outlook and Outlook on the web (formerly known as Outlook Web App). For more information about ABPs, see [Address book policies in Exchange Online](address-book-policies).

ABP routing creates the virtual organizations within a single Exchange Online organization. The global address list (GAL) you reside in determines your virtual organization. When ABP routing is turned on, users assigned to different GALs appear as external recipients and can't view each other's contact cards.

In Exchange Online, you can only turn on ABP routing in Exchange Online PowerShell.

Looking for the Exchange Server version of this article? See [Use the Exchange Management Shell to install and configure the Address Book Policy Routing Agent](../../email-addresses-and-address-books/address-book-policies/abp-procedures#use-the-exchange-management-shell-to-install-and-configure-the-address-book-policy-routing-agent).

## What do you need to know before you begin?

- You need to be a member of the Organization Management role group in Exchange Online before you can perform the procedure in this article.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to turn on ABP routing

To enable ABP routing in the Exchange Online organization, run the following command:

```PowerShell
Set-TransportConfig -AddressBookPolicyRoutingEnabled $true
```

For detailed syntax and parameter information, see [Set-TransportConfig](/en-us/powershell/module/exchangepowershell/set-transportconfig).

### How do you know this procedure worked?

To verify you successfully turned on ABP routing, use any of the following steps:

- In Exchange Online PowerShell, run the following command to verify that ABP routing is enabled for the organization:

    ```PowerShell
    Get-TransportConfig | Format-List AddressBookPolicyRoutingEnabled
    ```
- Get a user in one ABP to send a message to a user in a different ABP. Verify the sender's email address doesn't resolve to their display name.