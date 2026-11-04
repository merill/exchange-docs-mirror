---
layout: Conceptual
title: Create a mailbox policy in Exchange Online for Outlook on the web and the new Outlook for Windows | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/create-outlook-web-app-mailbox-policy
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
description: You can create an Outlook on the web mailbox policy to apply a common set of policy settings. Outlook on the web mailbox policies is useful for applying and standardizing settings, for example, attachment settings, for specific groups of users.
ms.topic: how-to
author: Swatyario
ms.author: adbhale
ms.assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms.reviewer: chrisda
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2023-11-17T00:00:00.0000000Z
locale: en-us
document_id: 458f1476-ddd9-d2cc-885c-256c50d7207c
document_version_independent_id: c816274c-2300-993b-1e01-ed85989c1ab7
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/create-outlook-web-app-mailbox-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-on-the-web/create-outlook-web-app-mailbox-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/create-outlook-web-app-mailbox-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: e2d705ca-d778-c2a5-edc9-34b0acc38ef3
---

# Create a mailbox policy in Exchange Online for Outlook on the web and the new Outlook for Windows | Microsoft Learn

You can create mailbox policies to apply settings to users in Outlook on the web (formerly known as Outlook Web App) and the new Outlook for Windows. Outlook on the web mailbox policies are useful for applying and standardizing settings, for example, attachment settings, for specific groups of users.

For more information about Outlook on the web mailbox policies, see [Outlook on the web mailbox policies](outlook-web-app-mailbox-policies).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. For information on the permissions you need, see the "Outlook on the web mailbox policies" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- For information on how to open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center). For information on how to connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to create a mailbox policy for Outlook on the web and the new Outlook for Windows

1. In the [EAC](https://admin.exchange.microsoft.com), go to **Roles** &gt; **Outlook web app policies**. Or, use the [**Outlook web app policies**](https://admin.exchange.microsoft.com/#/owapolicies) page and select **New OWA policy**.
2. In the **New Outlook web app policy** window that opens, configure the following settings:

    - **Basics** - **Name**: Enter a unique name for your policy.
    - **Features** - Use the checkboxes to enable or disable the features. By default, the most common features are displayed.
    - **File access** - Select how users can access and view email attachments from public and private computers.
    - **Review** - Review the Outlook Web App policy you have entered.

    Note

    You can configure settings for individual users by using the **Set-CASMailbox** cmdlet in Exchange Online PowerShell.
3. Select **Create** to save the policy.

    Under **Features**, the following list contains the features you can configure when you create a mailbox policy using the EAC for Outlook on the web and the new Outlook for Windows:

    - **Communication management**:

        - *Instant messaging*: If set to **Enabled**, users have access to instant messaging functionality such as the ability to send and receive instant messages, view presence information for other users, and change their own presence information.
        - *Text messaging*: If set to **Enabled**, users can send and receive text messages and create text message notification rules using Outlook on the web and the new Outlook for Windows.
        - *Exchange ActiveSync*: If set to **Enabled**, users can manage their linked mobile devices using Options in Outlook on the web.
        - *Contacts*: if set to **Enabled**, users can use Contacts in Outlook on the web and the new Outlook for Windows.
        - *LinkedIn contact sync*: If set to **Enabled**, users can add their LinkedIn connections to their mailbox as contacts. When a user's connection updates their information in LinkedIn, the contact is automatically updated.
        - *Mobile device contact sync*: If set to **Enabled**, users have access to personal contacts on their devices outside of Outlook on the web.
        - *All address lists*: If set to **Enabled**, users can view all address lists. If it's set to **Disabled**, the user can only view the default global address list.
    - **Information management**:

        - *Journaling*: If set to **Enabled**, the Journal folder is visible in Outlook on the web and the new Outlook for Windows.
        - *Notes*: If set to **Enabled**, the Notes folder is visible in Outlook on the web and the new Outlook for Windows.
        - *Inbox Rules*: If set to **Enabled**, a user can create and edit custom rules in Outlook on the web and the new Outlook for Windows.
        - *Recover deleted items*: If set to **Enabled**, users can view items that have been deleted from the Deleted Items folder and choose whether to recover them to the Deleted Items folder or to delete them permanently using Outlook on the web and the new Outlook for Windows.
    - **Security**:

        - *Change password*: If set to **Enabled**, people can change their passwords by going to Options in Outlook on the web and the new Outlook for Windows.
    - **User experience**:

        - *Themes*: If set to **Enabled**, users can change the color scheme in Outlook on the web and the new Outlook for Windows.
        - *Premium client*: If set to **Enabled**, users can use the standard version of Outlook on the web. If you clear the checkbox, users are switched to the light version of Outlook on the web and get a simplified experience.
        - *Email signature*: If set to **Enabled**, users can create a custom signature and choose whether to automatically include it in messages they send.
        - *Weather*: If set to **Enabled**, users can see weather information on their calendar.
        - *Places*: If set to **Enabled**, users can see location suggestions for meetings.
        - *Local events*: If set to **Enabled**, users can see the events happening in their area.
        - *Interesting calendars*: If set to **Enabled**, users can browse and add interesting calendars.
    - **Time management**:

        - *Calendar*: If set to **Enabled**, users can use the Calendar in Outlook on the web and the new Outlook for Windows.
        - *Tasks*: If set to **Enabled**, users can use Tasks in Outlook on the web and the new Outlook for Windows.
        - *Reminders and notifications*: If set to **Enabled**, users receive new email notifications and task and calendar reminders.

    Under **Manage access**, select how users can view and access attachments from public or private computers:

    - **File access**:
        - **Public or shared computer**: If set to **Enabled**, users can open file attachments by selecting them and then selecting **Open**.
        - **Private computers**: If set to **Enabled**, users can open file attachments by selecting them and then selecting **Open**.

## Use Exchange Online PowerShell to create a mailbox policy for Outlook on the web and the new Outlook for Windows

In Exchange Online PowerShell, creating a mailbox policy for Outlook on the web and the new Outlook for Windows is a two-step process:

1. Create the policy by using the following syntax:

    ```PowerShell
    New-OwaMailboxPolicy -Name "<Unique Name>"
    ```

    This example creates a mailbox policy named "Executives" for Outlook on the web and the new Outlook for Windows.

    ```PowerShell
    New-OwaMailboxPolicy -Name Policy1
    ```

    For detailed syntax and parameter information, see [New-OwaMailboxPolicy](/en-us/powershell/module/exchangepowershell/new-owamailboxpolicy).
2. Modify the default settings of the policy.

    For more information, see [Use Exchange Online PowerShell to modify mailbox policies for Outlook on the web and the new Outlook for Windows](configure-outlook-web-app-mailbox-policy-properties#use-exchange-online-powershell-to-modify-outlook-on-the-web-mailbox-policies).

## How do you know this worked?

To verify that you've successfully created a mailbox policy for Outlook on the web and the new Outlook for Windows, perform the following step:

- In the EAC, go to **Roles** &gt; **Outlook Web App Policies**, and look for your new mailbox policy.

To verify that you've successfully created a mailbox policy for Outlook on the web and the new Outlook for Windows, do either of the following steps:

- In the EAC, click **Roles** &gt; **Outlook Web App Policies**, select the policy and review the settings in the details flyout that opens.
- In Exchange Online PowerShell, run the following command to verify the policy is listed:

    ```PowerShell
    Get-OwaMailboxPolicy | Format-Table Name
    ```
- In Exchange Online PowerShell, replace &lt;Policy Name&gt; with the name of the policy, and run the following command to verify the settings:

    ```PowerShell
    Get-OwaMailboxPolicy -Identity "<Policy Name>"
    ```