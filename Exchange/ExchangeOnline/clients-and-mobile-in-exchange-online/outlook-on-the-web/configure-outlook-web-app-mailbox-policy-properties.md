---
layout: Conceptual
title: View or configure Outlook on the web mailbox policy properties in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/configure-outlook-web-app-mailbox-policy-properties
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
ms.custom:
- has-azure-ad-ps-ref
description: Admins can learn how to view and modify Outlook on the web mailbox policies (formerly known as Outlook Web App mailbox policies) in Exchange Online.
ms.topic: how-to
author: Swatyario
ms.author: adbhale
ms.assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
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
document_id: b1a3732b-86d4-53eb-22a6-8e6feec5ceeb
document_version_independent_id: 1a67364d-2277-1253-23ff-28b0acfe861b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/configure-outlook-web-app-mailbox-policy-properties.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-on-the-web/configure-outlook-web-app-mailbox-policy-properties
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/configure-outlook-web-app-mailbox-policy-properties.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 1f627200-4aaf-50e2-b3fd-42f69c21d0cb
---

# View or configure Outlook on the web mailbox policy properties in Exchange Online | Microsoft Learn

After you create a mailbox policy for Outlook on the web and the new Outlook for Windows, you can configure a variety of options to control the features available to users in Outlook on the web (formerly known as Outlook Web App) and the new Outlook for Windows. For example, you can enable or disable Inbox rules or create a list of allowed file types for attachments.

For more information about mailbox policies for Outlook on the web and the new Outlook for Windows, see [Outlook on the web mailbox policies](outlook-web-app-mailbox-policies).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 3 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. For information on the permissions you need, see the "Outlook on the web mailbox policies" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- For information on how to open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center). For information on how to connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to view or modify policies for Outlook on the web and the new Outlook for Windows

1. In the [EAC](https://admin.exchange.microsoft.com), go to **Roles** &gt; **Outlook web app policies**. Or, use [**Outlook web app policies**](https://admin.exchange.microsoft.com/#/owapolicies).
2. On the **Outlook web app policies** page, select the policy that you want to view or configure by clicking anywhere in the row other than the button option that appears next to the **Name** column.
3. In the **Details** flyout that opens, the following sections and links are available:

    - **Name**: Select **Manage name** to change the name of the policy in the **Edit name** flyout that opens.

        When you're finished in the **Edit name** flyout, select **Save changes**. Or, select **Close X** to cancel.
    - **Features**: Select **Manage features**. In the **Edit features** flyout that opens, the available settings are visible in the following expandable sections:

        - **Communication management**
        - **Information management**
        - **Security**
        - **User experience**
        - **Time management**

        When you're finished in the **Edit features** flyout, Select **Save changes**. Or, select **Close X** to cancel.
    - **Access**: Select **Manage access**. In the **Edit access** flyout that opens, the available settings are visible in the following sections:

        - **File access**
        - **Offline access**

        When you're finished in the **Edit access** flyout, select **Save changes**. Or, click **Close X** to cancel.

## Use Exchange Online PowerShell to view or modify policies for Outlook on the web and the new Outlook for Windows

### Use Exchange Online PowerShell to view Outlook on the web mailbox policies

To view an Outlook on the web mailbox policy, use the following syntax:

```PowerShell
Get-OwaMailboxPolicy [-Identity "<Policy Name>"]
```

This example returns a summary list of all policies in the organization.

```PowerShell
Get-OwaMailboxPolicy | Format-Table Name
```

This example retrieves detailed information for the policy named "Executives".

```PowerShell
Get-OwaMailboxPolicy -Identity Executives
```

For detailed syntax and parameter information, see [Get-OwaMailboxPolicy](/en-us/powershell/module/exchangepowershell/get-owamailboxpolicy).

### Use Exchange Online PowerShell to modify Outlook on the web mailbox policies

To modify an Outlook on the web mailbox policy, use the following syntax:

```PowerShell
Set-OwaMailboxPolicy -Identity "<Policy Name>" [Settings]
```

This example enables calendar access in the default mailbox policy.

```PowerShell
Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true
```

For detailed syntax and parameter information, see [Set-OwaMailboxPolicy](/en-us/powershell/module/exchangepowershell/set-owamailboxpolicy).

## How do you know that you've successfully modified an Outlook on the web mailbox policy?

To verify that you've successfully modified an Outlook on the web mailbox policy, perform either of the following steps:

- On the **Outlook web app policies** page in the [EAC](https://admin.exchange.microsoft.com/#/owapolicies), select the policy and review the settings in the **Details** flyout that opens.
- In Exchange Online PowerShell, replace &lt;Policy Name&gt; with the name of the policy, and run the following command to verify the settings:

    ```PowerShell
    Get-OwaMailboxPolicy -Identity "<Policy Name>"
    ```