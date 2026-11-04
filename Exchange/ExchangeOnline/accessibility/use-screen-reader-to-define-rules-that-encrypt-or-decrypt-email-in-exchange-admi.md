---
layout: Conceptual
title: Use a screen reader to define rules that encrypt or decrypt email messages in the Classic Exchange admin center in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/accessibility/use-screen-reader-to-define-rules-that-encrypt-or-decrypt-email-in-exchange-admi
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
ms.assetid: 3d8f2b49-c27e-40c9-808b-4bc48f3cdb07
ms.reviewer: 
description: Admins can learn how to use a screen reader to create mail flow rules (also known as transport rules) in the Classic Exchange admin center (Classic EAC) that use mMessage encryption to encrypt and decrypt messages in Exchange Online.
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
document_id: 7d78555c-e3b0-a750-d603-04b8084ff416
document_version_independent_id: 5ec3478e-bb8c-a592-df3e-47d9e589dc30
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/accessibility/use-screen-reader-to-define-rules-that-encrypt-or-decrypt-email-in-exchange-admi.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: accessibility/use-screen-reader-to-define-rules-that-encrypt-or-decrypt-email-in-exchange-admi
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/accessibility/use-screen-reader-to-define-rules-that-encrypt-or-decrypt-email-in-exchange-admi.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 829b215e-5d1e-738f-9866-ed00ee7dc67e
---

# Use a screen reader to define rules that encrypt or decrypt email messages in the Classic Exchange admin center in Exchange Online | Microsoft Learn

In the Classic Exchange admin center (Classic EAC) in Exchange Online, you can create mail flow rules (also known as transport rules) to enable or disable Microsoft Purview Message Encryption. This lets you encrypt outgoing email messages and remove encryption from encrypted messages coming from inside your organization or from replies to encrypted messages sent from your organization.

**Note**: To learn more about message encryption, go to [Encryption](/en-us/purview/encryption). Your organization must have [Set up new Message Encryption capabilities](/en-us/purview/set-up-new-message-encryption-capabilities) to complete the tasks in this topic.

## Get started

Navigate with Internet Explorer and keyboard shortcuts, and make sure that you have the appropriate Microsoft 365 or Office 365 subscription plan and admin role to perform this task. Then, open the EAC and get started.

### Use your browser and keyboard to navigate in the EAC

Exchange Online, which includes the EAC, is a web-based application, so the keyboard shortcuts and navigation may be different from those in Exchange 2016. [Accessibility in the Exchange admin center](accessibility-in-exchange-admin-center).

For best results when working in the EAC in Exchange Online, use Internet Explorer as your browser. [Learn more about Internet Explorer keyboard shortcuts](https://support.microsoft.com/help/17456/).

Many tasks in the EAC require the use of pop-up windows. In your browser, be sure to [enable pop-up windows](https://support.microsoft.com/help/17479) for Microsoft 365 or Office 365.

### Confirm your Office 365 or Microsoft 365 subscription plan

Exchange Online is included in several different subscription plans, but capabilities may differ by plan. If your EAC doesn't include a function described in this article, your plan might not include it.

For more information about the Exchange Online capabilities in your subscription plan, go to [What Microsoft 365 Apps for business product or license do I have?](https://support.microsoft.com/office/f8ab5e25-bf3f-4a47-b264-174b1ee925fd) and [Exchange Online Service Description.](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description).

### Open the EAC, and confirm your admin role

To complete the tasks covered in this topic, [Use a screen reader to open the Exchange admin center](use-screen-reader-to-open-exchange-admin-center) and check that you've been assigned to the Organization Management and Records Management admin role groups. [Use a screen reader to identify your admin role in the Exchange admin center](use-screen-reader-to-identify-admin-role-in-exchange-admin-center).

## Create a mail flow rule to encrypt email messages

1. In the EAC, to move the focus to the first link in the navigation pane (**Dashboard**) press Ctrl+F6 *twice*. You hear "Dashboard, Primary navigation link..
2. To move the focus to the **mail flow** link in the navigation pane, press the Tab key until you hear "Mail flow, Primary navigation link." Press Enter.
3. To move the focus to the mail flow settings in the content area of the page, the first of which is the **rules** link, press Ctrl+F6. You hear "Rules, Secondary navigation link..
4. To create a new rule, move the focus to the **New** button by pressing the Tab key until you hear "New button." Press Enter. You hear "Menu." To select the **Create a new rule** option from the list of options that opens for the button, press the Down Arrow key. You hear "Create a new rule." Press Enter.
5. As the focus moves to the **Name** text box in the **new rule** pop-up window, you hear "New rule, Name, Edit." Type the name of the new rule (such as Encrypt email for email address). To move to the next option in the window, press the Tab key.
6. As the focus moves to the **Apply this rule if** drop-down box, you hear "Apply this rule if, Combo box." Press the Down Arrow or Up Arrow key until you hear the condition you want to select. Press Enter. For example, if you want to encrypt messages for a particular email address, perform the following five steps.

    1. In the **Apply this rule if** drop-down box, press the Down Arrow key until you hear "The recipient is." Press Enter.
    2. As the focus moves to the **Search** button in the **Select Members** pop-up window that opens, you hear "Select Members, Search..
    3. To move the focus to each of the following three elements of the user interface, press the Tab key:

        1. The **Display Name** column. You hear "Display Name, Column header..
        2. The list of names of each person in your organization in the **Name** column. You hear the name of the first person followed by "Button..
        3. The first person in the list. You hear the name of the first person followed by "Row."
    4. The first person in the list. You hear the name of the first person followed by "Row."
    5. To accept your changes, move the focus to the **OK** button by pressing the Tab key until you hear "Okay button." Press Enter.
7. As the focus moves back to the **new rule** pop-up window, you hear "New rule..
8. To move the focus to the **More options** link in the **new rule** pop-up window, press the Tab key until you hear "More options link." Press Enter.

    Tip

    When you select the **More options** link, more user interface (UI) elements are added to the page and more options are added to the combo boxes. To have access to the **Modify the message security** option that you need to select in the next step, you must select the **More options** link.
9. To move the focus back to the **Do the following** drop-down box in the **new rule** pop-up window, press Shift+Tab until you hear "Do the following, Combo box." Perform the following two steps.

    1. In the **Do the following** drop-down box, to select the **Modify the message security** option, press the Down Arrow key until you hear "Modify the message security." Press Enter.
    2. As the focus moves to a list of message security options, you hear the first option in the list, "Apply rights protection." To select the **Apply Office 365 Message Encryption** option, press the Down Arrow key until you hear "Apply Office 365 Message Encryption." Press Enter.
10. To save the new rule, move the focus to the **Save** button by pressing the Tab key until you hear "Save button." Press Enter.
11. As the focus moves back to the **New** button on the **rules** content area of the page, you hear "Rules, New button." The new rule is turned on by default.

Tip

To turn off a new rule, press the Tab key to tab through the elements of the **rules** content area of the page, use the Up Arrow and Down Arrow keys to select a rule, and then press Spacebar. To hear the settings for a selected rule, press the Tab key until the focus moves to the details pane for the selected rule, and you hear the details for the rule.

## Create a mail flow rule to decrypt email messages

1. In the EAC, to move the focus to the first link in the navigation pane (**Dashboard**) press Ctrl+F6 *twice*. You hear "Dashboard, Primary navigation link..
2. To move the focus to the **mail flow** link in the navigation pane, press the Tab key until you hear "Mail flow, Primary navigation link." Press Enter.
3. To move the focus to the mail flow settings in the content area of the page, the first of which is the **rules** link, press Ctrl+F6. You hear "Rules, Secondary navigation link..
4. To create a new rule, move the focus to the **New** button by pressing the Tab key until you hear "New button." Press Enter. You hear "Menu." To select the **Create a new rule** option from the list of options that opens for the button, press the Down Arrow key. You hear "Create a new rule." Press Enter.
5. As the focus moves to the **Name** text box in the **new rule** pop-up window, you hear "New rule, Name, Edit." Type the name of the new rule (such as Remove encryption from incoming mail). To move to the next option in the window, press the Tab key.
6. As the focus moves to the **Apply this rule if** drop-down box, you hear "Apply this rule if, Combo box." Press the Down Arrow or Up Arrow key until you hear the condition you want to select. Press Enter. For example, if you want to decrypt all incoming messages for your organization, perform the following four steps.

    1. In the **Apply this rule if** drop-down box, press the Down Arrow key until you hear "The recipient is located." Press Enter.
    2. As the focus moves to a list of locations in the **select recipient location** pop-up window that opens, you hear "Select recipient location..
    3. To move between and select a location in the list, press the Down Arrow and Up Arrow keys. You hear the name of each location. For example, to select the **Inside the organization location**, press the Down Arrow key until you hear "Inside the organization..
    4. To accept your changes, move the focus to the **OK** button by pressing the Tab key until you hear "Okay button." Press Enter.
7. As the focus moves back to the **new rule** pop-up window, you hear "New rule..
8. To move the focus to the **More options** link in the **new rule** pop-up window, press the Tab key until you hear "More options link." Press Enter.

    Tip

    When you select the **More options** link, more user interface (UI) elements are added to the page and more options are added to the combo boxes. To have access to the **Modify the message security** option that you need to select in the next step, you must select the **More options** link.
9. To move the focus back to the **Do the following** drop-down box in the **new rule** pop-up window, press Shift+Tab until you hear "Do the following, Combo box." Perform the following two steps.

    1. In the **Do the following** drop-down box, to select the **Modify the message security** option, press the Down Arrow key until you hear "Modify the message security." Press Enter.
    2. As the focus moves to a list of message security options, you hear the first option in the list, "Apply rights protection." To select the **Remove Office 365 Message Encryption** option, press the Down Arrow key until you hear "Remove Office 365 Message Encryption." Press Enter.
10. To save the new rule, move the focus to the **Save** button by pressing the Tab key until you hear "Save button." Press Enter.
11. As the focus moves back to the **New** button on the **rules** content area of the page, you hear "Rules, New button." The new rule is turned on by default.

Tip

To turn off a new rule, press the Tab key to tab through the elements of the **rules** content area of the page, use the Up Arrow and Down Arrow keys to select a rule, and then press Spacebar. To hear the settings for a selected rule, press the Tab key until the focus moves to the details pane for the selected rule, and you hear the details for the rule.