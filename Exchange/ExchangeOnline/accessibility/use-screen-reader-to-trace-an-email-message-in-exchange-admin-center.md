---
layout: Conceptual
title: Use a screen reader to trace an email message in the Classic Exchange admin center in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/accessibility/use-screen-reader-to-trace-an-email-message-in-exchange-admin-center
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
ms.assetid: c95dd3ac-27e3-47ac-9130-5314a72ab4bd
ms.reviewer: 
description: Admins can learn how to use a screen reader to run a message trace in the Classic Exchange admin center (Classic EAC) in Exchange Online.
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
document_id: 037c85ec-e84a-3cba-bcf6-e4d4e930f820
document_version_independent_id: 76558e9a-30e2-0991-5134-e41a683c4b68
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/accessibility/use-screen-reader-to-trace-an-email-message-in-exchange-admin-center.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: accessibility/use-screen-reader-to-trace-an-email-message-in-exchange-admin-center
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/accessibility/use-screen-reader-to-trace-an-email-message-in-exchange-admin-center.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 9a83094b-7b5d-84ea-2136-12d11495fbff
---

# Use a screen reader to trace an email message in the Classic Exchange admin center in Exchange Online | Microsoft Learn

You can trace email messages by using your screen reader in the Classic Exchange admin center (Classic EAC) in Exchange Online. This is helpful if users are wondering whether their messages are delayed or possibly lost in delivery. With message tracing, you can follow messages as they pass through Exchange Online and determine whether a targeted email message was received, rejected, deferred, or delivered.

## Get started

Navigate with Internet Explorer and keyboard shortcuts, and make sure that you have the appropriate Microsoft 365 or Office 365 subscription plan and admin role to perform this task. Then, open the EAC and get started.

### Use your browser and keyboard to navigate in the EAC

Exchange Online, which includes the EAC, is a web-based application, so the keyboard shortcuts and navigation may be different from those in Exchange 2016. [Accessibility in the Exchange admin center](accessibility-in-exchange-admin-center).

For best results when working in the EAC in Exchange Online, use Internet Explorer as your browser. [Learn more about Internet Explorer keyboard shortcuts](https://support.microsoft.com/help/17456/).

Many tasks in the EAC require the use of pop-up windows. In your browser, be sure to [enable pop-up windows](https://support.microsoft.com/help/17479) for Microsoft 365 or Office 365.

### Confirm your Office 365 or Microsoft 365 subscription plan

Exchange Online is included in several different subscription plans, but capabilities may differ by plan. If your EAC doesn't include a function described in this article, your plan might not include it.

For more information about the Exchange Online capabilities in your subscription plan, go to [What Office 365 business product or license do I have?](https://support.microsoft.com/office/f8ab5e25-bf3f-4a47-b264-174b1ee925fd) and [Exchange Online Service Description](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description).

### Open the EAC, and confirm your admin role

To trace a message, [Use a screen reader to open the Exchange admin center](use-screen-reader-to-open-exchange-admin-center) and check that you've been assigned to the Organization Management, Compliance Management, and Help Desk admin role groups. Learn how to [Use a screen reader to identify your admin role in the Exchange admin center](use-screen-reader-to-identify-admin-role-in-exchange-admin-center).

## Create a new message trace

You might find that you need a message trace when a user contacts you about messages that are not delivered or are taking longer than usual to be delivered. You can trace a message using various criteria, including email address, date range, delivery status, and message ID.

1. In the EAC, press Ctrl+F6 until the primary navigation pane has the focus and you hear "Dashboard, Primary navigation link."
2. Tab to **mail flow**, and press Enter.
3. To move to the menu bar, press Ctrl+F6.
4. Tab to **message trace**. You hear "Message trace, Secondary navigation link." Press Enter.
5. To access the main window list view, press Ctrl+F6. You hear "Message was sent or received combo box, Past 48 hours."
6. The **Date range** combo box has the focus, and the default setting is **Past 48 hours**. To cycle through the other choices, including **Past 24 hours,** **Past 7 Days**, and **Custom**, press the Up Arrow or Down Arrow key.

    Tip

    If you select **Custom**, you can tab to and enter the time zone, start date and time, and end date and time. These fields are not available unless you select **Custom** in the **Date range** combo box. Note that there might not be any data for messages that are less than four hours old. You cannot run a message trace on a message more than 90 days old.
7. Tab to the **Delivery status** combo box. Choices are **All** (the default setting), **Delivered**, **Failed**, Pending, **Expanded**, **Quarantined**, **Filtered as spam**, and **Unknown**. Press the Down Arrow or Up Arrow key until the delivery status you want is selected.
8. Tab to the **Message ID** text box. This is an optional field, but it can help narrow the search results. The Message ID or Client ID is generated by the sending system and can be found in the header of the message with the **Message-ID**: token. The Message ID might include angle brackets (&lt; &gt;).
9. To specify senders (one or more) in the message trace, tab to the **add sender** button and press Enter. In the **Select Members** dialog box, the **Search** button has the focus.

    1. To search for a user within your organization, press Enter, type all or part of the name of the user, and then press Enter.
    2. Press the Tab key about seven times until you hear the name of the user in the search results list.
    3. To add the user to the list of senders for the message trace, press the Down Arrow key until you hear the user's name and then press Enter. The list of users retains the focus, so you can continue to add more users by selecting their mailboxes and pressing Enter.

    Tip

    To check the users you've added, tab to the **Add** button. To hear the list of users, press the Tab key again. The first name is read. To hear the second name in the list, press the Tab key one more time. Continue pressing the Tab key until you hear the names of all the users you've added. To delete a user from the list, activate the **Remove** link by pressing Enter when you hear the username.

    1. To specify an external user or an email address with a wildcard (for example, \*@contoso.com), press the Tab key until you hear "Check names edit, Type in text." (In Narrator, you hear "Editing.") Type the email address of the external user or the address with a wildcard. To select the **Check names** button, press Shift+Tab and then press Enter. This verifies the email address and adds it to the list of users.

    Tip

    When you specify a wildcard, you cannot also add full email addresses to the message trace. &gt; Be aware that if you type an external email address and press Enter, this adds the user to the list and then closes the dialog box. If you're not finished, use the **Check names** button to add it instead.

    1. When you finish adding users, tab to the **OK** button and press Enter. The **message trace** page has the focus again, and the **Sender** text box lists the senders you specified for the message trace.
10. To add a recipient to the message trace instead of or in addition to the senders, tab to the **add recipient** button and press Enter. In the **Select Members** dialog box, the **Search** button has the focus. To add one or more recipients to the message trace, repeat step 9.
11. On the **message trace** page, tab to the **search** button and press Enter. The **Message Trace Results** page opens and shows the date, sender, recipient, subject, and status of the message(s) that are a result of the message trace.

Tip

When you run a trace for messages that are less than seven days old, the messages should appear within 5-30 minutes. When you run a message trace for messages that are more than seven days old, results may take up to a few hours. So if the **Message Trace Results** page appears empty at first, check again later. An easy way to do this is to keep this page open, and, on the toolbar, periodically tab to the **Refresh** button and then press Enter.

1. To close the **Message Trace Results** page, tab to the Close button and press Enter.

## Review the status of pending or completed message traces

It might take a few minutes to a few hours for message trace results to return. You can check the status of pending or completed message traces.

1. In the EAC, press Ctrl+F6 until the primary navigation pane has the focus and you hear "Dashboard, Primary navigation link."
2. Tab to **mail flow**, and press Enter.
3. To move to the menu bar, press Ctrl+F6.
4. Tab to **message trace**. You hear "Message trace, Secondary navigation link." Press Enter.
5. To access the main window list view, press Ctrl+F6. You hear "Message was sent or received combo box..
6. The **Date range** combo box has the focus. To move to the View **pending or completed traces** link, press Shift+Tab. Press Enter. The **pending or completed traces** page opens and shows the report title, date submitted, report status, and messages.
7. To refresh the page, make sure that the **Refresh** button has the focus (this is the default setting) and then press Enter.
8. To close the **pending or completed traces** page, tab to the **Close** button and press Enter.

    Note

    For more information, refer to [Trace an email message](../monitoring/trace-an-email-message/trace-an-email-message).