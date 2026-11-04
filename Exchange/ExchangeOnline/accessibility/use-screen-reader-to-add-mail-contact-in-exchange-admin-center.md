---
layout: Conceptual
title: Use a screen reader to add a new mail contact in the Classic Exchange admin center in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/accessibility/use-screen-reader-to-add-mail-contact-in-exchange-admin-center
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
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 723ab221-3abe-40ee-8143-eee45e9d0519
ms.reviewer: 
description: Admins can learn how to use a screen reader to create a new mail contact in the Classic Exchange admin center (Classic EAC) in Exchange Online.
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
f1.keywords:
- CSH
ms.custom: A11y_UseSR
ms.service: exchange-online
ms.date: 2018-06-26T00:00:00.0000000Z
locale: en-us
document_id: 2604b43e-3348-acc6-320e-c5c44398df74
document_version_independent_id: f2457d6b-b301-9c34-6d27-a4c340c09002
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/accessibility/use-screen-reader-to-add-mail-contact-in-exchange-admin-center.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: accessibility/use-screen-reader-to-add-mail-contact-in-exchange-admin-center
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/accessibility/use-screen-reader-to-add-mail-contact-in-exchange-admin-center.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 5e5cf473-bad4-ec00-bad8-740ed31c5352
---

# Use a screen reader to add a new mail contact in the Classic Exchange admin center in Exchange Online | Microsoft Learn

Using a screen reader with Exchange Online, you can use the Classic Exchange admin center (Classic EAC) to set up a *mail contact*: a mail-enabled directory service object containing information about a person or entity that exists outside of your Exchange Online organization. Each mail contact has an external email address. For more information about mail contacts, refer to the [Recipients in Exchange Online](../recipients-in-exchange-online/recipients-in-exchange-online) article.

## Get started

Navigate with Internet Explorer and keyboard shortcuts, and make sure that you have the appropriate Microsoft 365 or Office 365 subscription plan and admin role to work in the EAC. Then, open the EAC and get started.

### Use your browser and keyboard to navigate in the EAC

Exchange Online, which includes the EAC, is a web-based application, so the keyboard shortcuts and navigation may be different from those in Exchange 2016. [Accessibility in the Exchange admin center](accessibility-in-exchange-admin-center).

For best results when working in the EAC in Exchange Online, use Internet Explorer as your browser. [Learn more about Internet Explorer keyboard shortcuts](https://support.microsoft.com/help/17456/).

Many tasks in the EAC require the use of pop-up windows. In your browser, be sure to [enable pop-up windows](https://support.microsoft.com/help/17479) for Microsoft 365 or Office 365.

### Confirm your Office 365 or Microsoft 365 subscription plan

Exchange Online is included in several different subscription plans. But capabilities may differ by plan. If your EAC doesn't include a function described in this article, your plan might not include it.

For more information about the Exchange Online capabilities in your subscription plan, go to [What Office 365 business product or license do I have?](https://support.microsoft.com/office/f8ab5e25-bf3f-4a47-b264-174b1ee925fd) and [Exchange Online Service Description.](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description).

### Open the EAC, and confirm your admin role

To add a new mail contact, [Use a screen reader to open the Exchange admin center in Exchange Online](use-screen-reader-to-open-exchange-admin-center) and check that you've been assigned to the Organization Management and Recipient Management admin role group. Learn how to [Use a screen reader to identify your admin role in the Exchange admin center](use-screen-reader-to-identify-admin-role-in-exchange-admin-center).

## Use the EAC to create a mail contact

1. In the EAC, in the primary navigation pane, tab to **Recipients**. You hear "Recipients, Primary navigation." Press Enter.
2. To move the focus to the menu bar, press Ctrl+F6. You hear "Mailboxes, Secondary navigation."
3. Press the Left Arrow key until you hear "Contacts, Secondary navigation," and then press Enter. A table listing mail contacts appears.
4. To move the focus to the contacts menu bar, press Ctrl+F6 until you hear "New button menu."
5. Press Spacebar, and then press the Down Arrow key until you hear "Mail contact." Then, press Enter. The **new mail contact** window opens.

    **Note**: In Narrator, if the menu options for the **New** button are not read, you hear "Empty line." **Mail contact** is the first option. **Mail user** is the second option. When you select **Mail contact**, if Narrator doesn't announce the name of the **new mail contact** window or the **First name** box, to refresh the window and reestablish the focus, press F5.
6. Tab to the following boxes, and complete the contact information:

    **Note**: Required boxes are designated with an asterisk. In screen readers, you hear "star" or "asterisk" before the label. For example, in the required **Display Name** box, you hear "Star display name" or "Asterisk display name.

    - **First name**. Type the contact's first name.
    - **Initials**. Type the contact's initial.
    - **Last name**: Type the contact's last name.
    - **\*Display name**. To change the default, type the name as it will appear in the **contacts** list in the EAC and in your organization's address book. By default, Exchange uses the names you entered in the **First name**, **Initials**, and **Last name** boxes. This name can't exceed 64 characters.
    - **\*Alias**. Type a unique alias (64 characters or less) for the contact.
    - **\*External email address**. Type the contact's email address that is outside of your organization. Email sent to the contact is forwarded to this email address.
7. When you're finished, tab to the **Save** button. The **new mail contact** window closes, and the contact is added to the table in the **contacts** window.