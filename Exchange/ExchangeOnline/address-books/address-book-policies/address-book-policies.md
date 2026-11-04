---
layout: Conceptual
title: Address book policies in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-book-policies/address-book-policies
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
description: Learn how to use address book policies (ABPs) to create separate virtual organizations with a segmented global address list in Exchange Online.
ms.topic: overview
author: Srividyavaranasi
ms.author: srvar
ms.assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2026-10-26T00:00:00.0000000Z
locale: en-us
document_id: 3d52e882-9b75-3091-79c5-c6733aa924b1
document_version_independent_id: 42c575aa-bb89-3aa2-21f1-adf4771ec10b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-book-policies/address-book-policies.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-book-policies/address-book-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-book-policies/address-book-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: fe2e92ca-dc86-d111-5040-12bc9f87e453
---

# Address book policies in Exchange Online | Microsoft Learn

Address book policies (ABPs) let admins segment users into specific groups to provide customized views of the organization's global address list (GAL). The goal of an ABP is to provide a simpler mechanism for GAL segmentation (also known as *GAL segregation*) in organizations that require multiple GALs.

An ABP contains these elements:

- One GAL. Note that this defines the recipients who can be found in people search. Users assigned this ABP will be able to find *only* people included in this GAL in people search experiences across Microsoft 365 products. For more information about GALs, see [Default address lists in Exchange Online](../address-lists/address-lists#default-address-lists).
- One offline address book (OAB). For more information about OABs, see [Offline address books in Exchange Online](../offline-address-books/offline-address-books).
- One room list. Note that this room list is a custom address list that specifies rooms (contains the filter `RecipientDisplayType -eq 'ConferenceRoomMailbox'`). It's not a room finder that you create with the *RoomList* switch on the **New-DistributionGroup** or **Set-DistributionGroup** cmdlet. For more information, see [Managing resource mailboxes](../../recipients-in-exchange-online/manage-resource-mailboxes).
- One or more address lists. For more information about address lists, see [Custom Address Lists in Exchange Online](../address-lists/address-lists#custom-address-lists).

For ABP management procedures, see:

- [Create an address book policy in Exchange Online](create-an-address-book-policy)
- [Change the settings of an address book policy in Exchange Online](change-the-settings-of-an-address-book-policy)
- [Assign an address book policy to users in Exchange Online](assign-an-address-book-policy-to-mail-users)
- [Turn on address book policy routing in Exchange Online](turn-on-address-book-policy-routing).

Note

- ABPs create only a virtual separation of users from a directory perspective, not a legal separation.
- Implementing an ABP is a multi-step process that requires planning. You must create or identify the required global address list, offline address book, room address list, and other address lists before you create and assign the ABP.

## How ABPs Work

The following diagram shows how ABPs work. The user is assigned Address Book Policy A that contains a subset of address lists that are available in the organization. When the ABP is created and assigned to the user, the ABP becomes the scope of the address lists that the user is able to view.

![Overview of Address Book Policies.](../../exchangeonline/media/itpro_mailbox_abpoverall.gif)

To turn on ABP email routing in your Exchange Online organization, see [Turn on address book policy routing in Exchange Online](turn-on-address-book-policy-routing).

To assign ABPs to users, see [Assign an address book policy to users in Exchange Online](assign-an-address-book-policy-to-mail-users).

ABPs take effect when a user connects to their Exchange Online Mailbox. If you change an ABP, the updated ABP takes effect when a user restarts or reconnects their email client app.

## ABP example

In the following diagram, Fabrikam and Tailspin Toys share the same Exchange Online organization and the same CEO. The CEO is the only employee common to both companies.

![Two Companies One CEO.](../../exchangeonline/media/itpro_.gif)

The suggested configuration includes three ABPs:

- One ABP is assigned to Fabrikam employees. The GAL and address lists in the ABP include Fabrikam employees and the CEO.
- One ABP is assigned to Tailspin Toys employees. The GAL and address lists in the ABP include Tailspin Toys employees and the CEO.
- One ABP is assigned to only the CEO. The (default) GAL and address lists in the ABP include all employees (Fabrikam, Tailspin Toys, and the CEO).

Based on this configuration, the ABPs help to enforce these requirements:

- The users in Tailspin Toys can only see Tailspin Toys employees and the CEO in people search experiences or when they browse the GAL.
- The users in Fabrikam can only see Fabrikam employees and the CEO in people search experiences or when they browse the GAL.
- The CEO can see all Fabrikam and Tailspin Toys employees in people search experiences or when she browses the GAL.
- Users who view the CEO's group membership can see only groups that belong to their company. They can't see groups that belong to the other company.