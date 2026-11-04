---
layout: Conceptual
title: Address lists in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-lists/address-lists
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
description: Admins can learn about the different types of address lists that are available in Exchange Online.
ms.topic: overview
author: Srividyavaranasi
ms.author: srvar
ms.assetid: 8ee2672a-3a45-4897-8cc0-fa23c374dbf9
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
document_id: 1a4e7552-5725-e5ad-0e75-6ca39d8e8d66
document_version_independent_id: 418ba58b-b27d-29c5-eed4-d20b8779dc6f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-lists/address-lists.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-lists/address-lists
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-lists/address-lists.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 1ee202b0-50ff-efcd-9a0a-187cecfa729c
---

# Address lists in Exchange Online | Microsoft Learn

An address list is a collection of mail-enabled recipient objects in Exchange Online. Address lists are based on recipient filters. You can filter by recipient type (for example, mailboxes and mail contacts), recipient properties (for example, Company or State or Province), or both. Address lists use recipient filters to determine membership. When you create or modify a recipient, Exchange Online evaluates the recipient against the applicable filters. However, a newly created custom address list might not automatically include all existing recipients that match its filter. If expected recipients are missing, you might need to update a property used by the filter to trigger reevaluation. These are the different types of address lists that are available:

- **Global address lists (GALs)**: The built-in GAL that's automatically created by Exchange Online includes every mail-enabled object in the organization. You can create additional GALs to separate users by organization or location, but a user can only see and use one GAL.
- **Address lists**: Address lists are subsets of recipients that are grouped together in one list, which makes them easier to find by users. Exchange Online comes with several built-in address lists, and you can create more based on your organization's needs.
- **Offline address books (OABs)**: OABs contain address lists and GALs. OABs are used by Outlook clients in cached Exchange mode to provide local access to address lists and GALs for recipient look-ups. For more information, see [Offline address books in Exchange Online](../offline-address-books/offline-address-books).

Users in your organization use address lists and the GAL to find recipients for email messages. Here's an example of what address lists look like in Outlook 2016:

![Global Address List (GAL).](../../exchangeonline/media/54c5aa4b-fbd3-4b37-8642-9a52b9558641.png)

For information about managing address lists, see [Manage address lists in Exchange Online](manage-address-lists).

**Notes:**

- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets or features that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- Precanned recipient filters or custom recipient filters identify the recipients that are included in address lists and GALs. For more information, see [Recipient filters for address lists in Exchange Online PowerShell](use-recipient-filters-to-create-an-address-list).
- You can hide recipients from all address lists and GALs. For more information, see [Hide recipients from address lists](manage-address-lists#hide-recipients-from-address-lists).

## Global address lists

By default, a new Exchange Online organization has a GAL named Default Global Address List that's the primary repository of all recipients in the organization. Typically, most organizations have only one GAL, because users can only see and use one GAL in Outlook and Outlook on the web (formerly known as Outlook Web App). You might need multiple GALs and address book policies if you want different groups to have segmented views of recipients in address lists and people-search experiences. This configuration provides virtual directory separation only; it isn't a security or legal separation boundary. If you plan on creating additional GALs, consider the following issues:

- You can only use the Exchange Online PowerShell to create, modify, remove, and update GALs.
- If a user belongs to multiple GALs, they'll still see only one GAL based on the following conditions:

    - The user needs permissions to view the GAL. You assign user permissions to GALs by using address book policies (ABPs). For more information, see [Address book policies in Exchange Online](../address-book-policies/address-book-policies).
    - If a user is still eligible to see multiple GALs, only the largest GAL is used (the GAL that contains the most recipients).
    - Each GAL needs a corresponding offline address book (OAB) that includes the GAL. To create OABs, see [Create an offline address book in Exchange Online](../offline-address-books/create-offline-address-book).
- The built-in GAL is named Default Global Address List, and any additional GALs that you create require unique names. Depending on the email client, users might not see the actual name of the GAL that they're using:

    - In Outlook on the web, users see the actual name of the GAL that they're using (for example, Default Global Address List).
    - In Outlook, the GAL always appears as Global Address List, which likely doesn't match the actual name.

## Default address lists

By default, Exchange Online comes with five built-in address lists and one GAL. These address lists are described in the following table. Note that by default, system-related mailboxes like arbitration mailboxes and public folder mailboxes are hidden from address lists.

| Name | Type | Description | Recipient filter used |
| --- | --- | --- | --- |
| All Contacts | Address list | Includes all mail contacts in the organization. To learn more about mail contacts, see [Recipients in Exchange Online](../../recipients-in-exchange-online/recipients-in-exchange-online). | `"Alias -ne $null -and (ObjectCategory -like 'person' -and ObjectClass -eq 'contact')"` |
| All Distribution Lists | Address list | Includes all distribution groups and mail-enabled security groups in the organization. To learn more about mail-enabled groups, see [Recipients in Exchange Online](../../recipients-in-exchange-online/recipients-in-exchange-online). | `"Alias -ne $null -and ObjectCategory -like 'group'"` |
| All Rooms | Address list | Includes all room mailboxes. Equipment mailboxes aren't included. To learn more about room and equipment (resource) mailboxes, see [Recipients in Exchange Online](../../recipients-in-exchange-online/recipients-in-exchange-online). | `"Alias -ne $null -and (RecipientDisplayType -eq 'ConferenceRoomMailbox' -or RecipientDisplayType -eq 'SyncedConferenceRoomMailbox')"` |
| All Users | Address list | Includes all user mailboxes, linked mailboxes, remote mailboxes (Microsoft 365 or Office 365 mailboxes), shared mailboxes, room mailboxes, equipment mailboxes, and mail users in the organization. To learn more about these recipient types, see [Recipients in Exchange Online](../../recipients-in-exchange-online/recipients-in-exchange-online). | `"((Alias -ne $null) -and (((((((ObjectCategory -like 'person') -and (ObjectClass -eq 'user') -and (-not(Database -ne $null)) -and (-not(ServerLegacyDN -ne $null)))) -or (((ObjectCategory -like 'person') -and (ObjectClass -eq 'user') -and (((Database -ne $null) -or (ServerLegacyDN -ne $null))))))) -and (-not(RecipientTypeDetailsValue -eq 'GroupMailbox')))))"` |
| Default Global Address List | GAL | Includes all mail-enabled recipient objects in the organization (users, contacts, groups, dynamic distribution groups, and public folders). | `"((Alias -ne $null) -and (((ObjectClass -eq 'user') -or (ObjectClass -eq 'contact') -or (ObjectClass -eq 'msExchSystemMailbox') -or (ObjectClass -eq 'msExchDynamicDistributionList') -or (ObjectClass -eq 'group') -or (ObjectClass -eq 'publicFolder'))))"` |
| Public Folders | Address list | Includes all mail-enabled public folders in your organization. Access permissions determine who can view and use public folders. For more information about public folders, see [Public folders in Microsoft 365 or Office 365 and Exchange Online](../../collaboration-exo/public-folders/public-folders). | `"Alias -ne $null -and ObjectCategory -like 'publicFolder'"` |

## Custom Address Lists

An Exchange Online organization might contain thousands of recipients, so the built-in address lists could become quite large. To prevent this, you can create custom address lists to help users find what they're looking for.

For example, consider a company that has two large divisions in one Exchange Online organization:

- Fourth Coffee, which imports and sells coffee beans.
- Contoso, Ltd, which underwrites insurance policies.

For most day-to-day activities, employees at Fourth Coffee don't communicate with employees at Contoso, Ltd. Therefore, to make it easier for employees to find recipients who exist only in their division, you can create two new custom address lists: one for Fourth Coffee and one for Contoso, Ltd. However, if an employee is unsure about where recipient exists, they can search in the GAL, which contains all recipients from both divisions.

In Exchange Online, you can only use PowerShell to create custom address lists.

## Best Practices for Creating Address Lists

Although address lists are useful tools for users, poorly planned address lists can cause frustration. To make sure that your address lists are practical for users, consider the following best practices:

- Address lists should make it easier for users to find recipients.
- Avoid creating so many address lists that users can't tell which list to use.
- Use a naming convention and location hierarchy for your address lists so users can immediately tell what the list is for (which recipients are included in the list). If you have difficulty naming your address lists, create fewer lists and remind users that they can find anyone in your organization by using the GAL.

For information about managing address lists, see [Manage address lists in Exchange Online](manage-address-lists).

## View Address Lists in Outlook and Outlook on the web

Address lists in Exchange include both users and other objects such as meeting rooms. Historically, both Outlook and Outlook on the web (formerly known as Outlook Web App) allowed you to browse the entire address list, regardless of its size. A user in an organization with thousands or even hundreds of thousands of entries could scroll through the entire list in a single dialog to find a user or object. However, this approach is inefficient in terms of human effort and computing resources. A simple search can quickly narrow down the results, making it easier and faster to find an entry.

Microsoft made a change to encourage users to use search instead of infinite browsing and also to improve performance. This change impacts browsing in any online address list with more than 500 objects. This change applies to the GAL, built-in address lists, and custom address lists. The change does not affect browsing Offline Address Books.

In Outlook, opening an online address book is limited to showing the first 500 users if the result set exceeds 500 objects. To find a specific user or set of users with similar names, you can use the existing search functionality in Outlook. The behavior when searching based on **All columns** is unchanged. Search continues to return results if the criteria produces a matching result set of less than 5000 objects (by checking for partial matches in DisplayName, FirstName, LastName, Alias, and CommonName). If the result set exceeds 5000 objects, no results are displayed and a message encourages you to narrow your search criteria. Searches based on **Name Only** now behave consistently with searches based on **All columns**. The only difference with **Name Only** is the criteria is naturally based only on the name value. Searches based on **Name only** no longer allow unlimited browsing of the entire address list as they did previously.

Tip

As previously mentioned, users can still browse an Offline Address Book in its entirety.

In Outlook on the web, users are already directed to use search and suggestions provided by the search engine. However, if a user selects the **To:** button in a draft email, they are able to view an online address list. If the online address list contains more than 450 users, no results are shown. A message directs the user to find the desired recipient using search instead. Also, the People Hub in Outlook on the web now requires a search criteria to display any users. Users automatically get a corresponding message when they navigate to view an address list.