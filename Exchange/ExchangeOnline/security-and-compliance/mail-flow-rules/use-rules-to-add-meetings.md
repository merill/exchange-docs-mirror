---
layout: Conceptual
title: Use mail flow rules to automatically add meetings to calendars in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-add-meetings
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Admins can learn how to use mail flow rules to add meetings to calendars in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: c93c31a4-fe5e-479b-83b6-ee114d4f236c
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: d74e35f7-51df-073f-6f5c-7413db1f341b
document_version_independent_id: 92e127cb-4b4d-2415-a535-a2d151439a11
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-add-meetings.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/use-rules-to-add-meetings
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-add-meetings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 28b9cc44-053c-8ff3-2eb0-ef6565d2d65a
---

# Use mail flow rules to automatically add meetings to calendars in Exchange Online | Microsoft Learn

Note

This article doesn't apply to the Built-in security add-on for on-premises mailboxes.

With the Direct to Calendar feature in Exchange Online, administrators can configure mail flow rules (also known as transport rules) that allow designated users to add meetings to calendars. The benefits of Direct to Calendar are:

- The event is automatically added to the recipient's calendar without any action from them. If the user received the meeting invitation, it's on their calendar.
- The sender doesn't need to deal with Out of Office or other unwanted response messages that result from sending meeting invitations to a large number of recipients.
- No meeting-related messages are seen by attendees.

Direct to Calendar requires two mail flow rules with specific conditions and actions. These rules are described in the following table:

| Rule description | Condition | Action | Comments |
| --- | --- | --- | --- |
| This mail flow rule turns regular meeting invitations into Direct to Calendar meeting invitations. | **The sender** &gt; **is this person** (the *From* parameter). <br> This condition identifies the users who are authorized to send Direct to Calendar meeting invitations. Although you can use other conditions, restricting the invitations by sender helps prevent unauthorized use of Direct to Calendar meeting invitations. | **Modify the message properties** &gt; **set a message header** (the *SetHeaderName* and *SetHeaderValue* parameters). <br> This action sets the **X-MS-Exchange-Organization-CalendarBooking-Response** header to the value `Accept`. Other valid values are `Tentative` and `Decline`. | We recommend that you use dedicated mailboxes (shared mailboxes are OK) for sending Direct to Calendar meeting invitations, because *any* meeting invitations from these senders will be automatically added to recipient calendars. <br> The dedicated mailboxes require no special permissions to send Direct to Calendar meeting invitations. |
| This mail flow rule prevents Direct to Calendar meeting invitations from appearing in the Inbox of recipients. | **The sender** &gt; **is this person** (the *From* parameter). | **Modify the message properties** &gt; **set a message header** (the *SetHeaderName* and *SetHeaderValue* parameters). <br> This action sets the **X-MS-Exchange-Organization-CalendarBooking-TriageAction** header to the value `MoveToDeletedItems`. The other valid value is `None`. | Technically, this rule is optional (without it, meetings are still automatically added to recipient calendars). <br> This rule doesn't prevent meeting cancellation messages for Direct to Calendar meetings from appearing in the Inbox of recipients. |

For more information about mail flow rules, see [Mail flow rules (transport rules) in Exchange Online](mail-flow-rules).

## What do you need to know before you begin?

- Estimated time to complete: 10 minutes
- You need to be assigned permissions before you can perform this procedure(s). To see what permissions you need, see the "Mail flow" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- The designated accounts for sending Direct to Calendar meeting invitations need to exist.
- For more information about opening and using the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center).
- For more information about how to connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use the Exchange admin center to create Direct to Calendar mail flow rules

1. In the EAC, go to **Mail flow** &gt; **rules**.
2. Select **+Add a rule**, and then select **Create a new rule**.
3. In the **Set rule conditions** page that opens, configure these additional settings on the **New rule** page:

    - **Name**: Direct to Calendar response (or anything descriptive).
    - **Apply this rule if** &gt; **The sender** &gt; **is this person**: Select one or more users to send Direct to Calendar meeting invitations.
    - **Do the following** &gt; **Modify the message properties** &gt; **set a message header**: Enter the following values:
    - **Set the message header**`X-MS-Exchange-Organization-CalendarBooking-Response`
    - **to the value**`Accept`

    [![Screenshot that shows the settings for the Direct to Calendar capture mail flow rule.](../../exchangeonline/media/52f4cb2c-5a86-46e7-a31b-231ae89931ab.png)](../../exchangeonline/media/52f4cb2c-5a86-46e7-a31b-231ae89931ab.png#lightbox)
4. Select **Next**. The **Set rule settings** page appears.
5. Select **Next**, leaving the default values as is. The **Review and finish** page appears.
6. Select **Finish**.
7. Navigate back to the EAC home page, and choose **Mail flow** &gt; **Rules**.
8. Select **+Add a rule**, and then select **Create a new rule**.
9. In the **Set rule conditions** page that opens, configure these extra settings on the **New rule** page:

    - **Name**: Direct to Calendar triage action (or anything descriptive).
    - **Apply this rule if** &gt; **The sender** &gt; **is this person**: Select the same users as in step 3.
    - **Do the following** &gt; **Modify the message properties** &gt; **set a message header**: Enter the following values:
    - **Set the message header**`X-MS-Exchange-Organization-CalendarBooking-TriageAction`
    - **to the value**`MoveToDeletedItems`
10. Select **Next**. The **Set rule settings** page appears.
11. Select **Next**, leaving the default values as is. The **Review and finish** page appears.
12. Select **Finish**.

    [![Screenshot that shows the settings for the Direct to Calendar triage action mail flow rule.](../../exchangeonline/media/52384435-eb38-449b-928b-94e0394e8f6a.png)](../../exchangeonline/media/52384435-eb38-449b-928b-94e0394e8f6a.png#lightbox)

## Use Exchange Online PowerShell to create Direct to Calendar mail flow rules

1. To create the mail flow rule that turns regular meeting invitations into Direct to Calendar meeting invitations, use the following syntax:

    ```PowerShell
    New-TransportRule -Name "Direct to Calendar response" -From "<designated sender 1>","<designated sender 2>"... -SetHeaderName "X-MS-Exchange-Organization-CalendarBooking-Response" -SetHeaderValue Accept
    ```

    This example configures the rule using the dedicated mailbox named **Direct to Calendar invites**.

    ```PowerShell
    New-TransportRule -Name "Direct to Calendar response" -From "Direct to Calendar invites" -SetHeaderName "X-MS-Exchange-Organization-CalendarBooking-Response" -SetHeaderValue Accept
    ```
2. To create the mail flow rule that prevents Direct to Calendar meeting invitations from appearing in the Inbox of recipients, use the following syntax:

    ```PowerShell
    New-TransportRule -Name "Direct to Calendar triage action" -From "<designated sender 1>","<designated sender 2>"... -SetHeaderName "X-MS-Exchange-Organization-CalendarBooking-TriageAction" -SetHeaderValue MoveToDeletedItems
    ```

    The following example configures the rule using the dedicated mailbox named **Direct to Calendar invites**.

    ```PowerShell
    New-TransportRule -Name "Direct to Calendar triage action" -From "Direct to Calendar invites" -SetHeaderName "X-MS-Exchange-Organization-CalendarBooking-TriageAction" -SetHeaderValue MoveToDeletedItems
    ```

For detailed syntax and parameter information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).

## How do you know this worked?

To verify that you've successfully configured Direct to Calendar meeting invitations, use the designated sender mailbox to send a test meeting invitation to a few recipients. Verify that the meeting automatically appears in the calendars of the recipients, and that there are no meeting-related messages in the Inbox (the second rule should automatically move these messages to the Deleted Items folder).

## More information

- The designated sender mailbox will receive meeting acceptance responses to Direct to Calendar meetings. Use the following strategies to help minimize the impact of these messages on the designated sender:

    - In Outlook, enable the **Update tracking information, and then delete responses that don't contain comments** and **After updating tracking information, move receipt to &lt;Deleted Items&gt;** settings in **Mail** &gt; **Tracking** for the designated sender mailbox. For more information, see [Change how meeting requests, polls, and read or delivery receipts are processed](https://support.microsoft.com/office/3e18ef46-57c0-4e49-ad89-b44ae75596ed).
    - Clearing the **Request Responses** setting in Direct to Calendar meeting invitations doesn't prevent responses from being sent back to the designated sender mailbox.
- If the designated mailbox sends a meeting cancellation for a Direct to Calendar meeting, the canceled meeting title is always changed to **CANCELED: &lt;previous meeting title&gt;**, and the canceled meeting remains in the calendars of attendees until they manually remove it.