---
layout: Conceptual
title: Enable or disable modern authentication for Outlook in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/enable-or-disable-modern-authentication-in-exchange-online
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: high
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 58018196-f918-49cd-8238-56f57f38d662
ms.reviewer: akprakash
description: Admins can learn how to require Modern Auth or require Basic Auth for connections to Exchange Online by Outlook 2013 or later.
ms.collection:
- Adm_O365
- exchange-online
- M365-email-calendar
search.appverid:
- BCS160
- MOE150
- MED150
- MET150
audience: Admin
f1.keywords:
- CSH
ms.custom:
- Adm_O365
- Adm_O365_FullSet
- MiniMaven
ms.service: exchange-online
ms.date: 2023-10-31T00:00:00.0000000Z
locale: en-us
document_id: e3595c01-2eb7-a6e0-0424-12d7628fa25b
document_version_independent_id: 2368964f-83cb-e16f-c04c-832361e18c63
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/enable-or-disable-modern-authentication-in-exchange-online.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/enable-or-disable-modern-authentication-in-exchange-online
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/enable-or-disable-modern-authentication-in-exchange-online.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 6e685ea3-34fe-09db-a354-1f4a845d600c
---

# Enable or disable modern authentication for Outlook in Exchange Online | Microsoft Learn

Modern authentication in Exchange Online enables authentication features like multifactor authentication (MFA), smart cards, certificate-based authentication (CBA), and non-Microsoft SAML identity providers. Modern authentication is based on the [Active Directory Authentication Library](/en-us/azure/active-directory/azuread-dev/active-directory-authentication-libraries) (ADAL) and OAuth 2.0.

When you enable modern authentication in Exchange Online, Windows-based Outlook clients that support modern authentication (Outlook 2013 or later) use modern authentication to connect to Exchange Online mailboxes. For more information, see [How modern authentication works for Office client apps](/en-us/office365/enterprise/modern-auth-for-office-2013-and-2016).

When you disable modern authentication in Exchange Online, Windows-based Outlook clients that support modern authentication use basic authentication to connect to Exchange Online mailboxes. They don't use modern authentication.

**Notes**:

- Since August 2017, Modern authentication is enabled by default in Exchange Online, Microsoft Teams, and SharePoint.
- Enabling or disabling modern authentication in Exchange Online as described in this article **only** affects modern authentication connections by Windows-based Outlook clients that support modern authentication (Outlook 2013 or later).
- Enabling or disabling modern authentication in Exchange Online as described in this article **does not** affect other email clients that support modern authentication (for example, Outlook Mobile, Outlook for Mac 2016, and Exchange ActiveSync in iOS 11 or later). These other email clients **always** use modern authentication to sign in to Exchange Online mailboxes.
- Enabling or disabling modern authentication has no effect on IMAP or POP3 clients. However, you enabled *security defaults* in your organization, POP3 and IMAP4 are already disabled in Exchange Online. For more information, see [Security defaults in Microsoft Entra ID](/en-us/entra/fundamentals/security-defaults).
- When you enable modern authentication in Exchange Online, Windows-based Outlook clients that support modern authentication are prompted to sign in again. Further, the Basic Auth sign in dialog box and the Modern Auth dialog box look very different. See the **Outlook and Basic Auth** section of the [Basic Auth and Exchange Online](https://techcommunity.microsoft.com/t5/exchange-team-blog/basic-auth-and-exchange-online-february-2020-update/ba-p/1191282) blog post for details.
- A user with multiple accounts configured in their Outlook profile might receive an error when they try to connect to their mailbox. For more information, see [Outlook shows "Disconnected" after you enable modern authentication in Microsoft 365](/en-us/troubleshoot/outlook/authentication/outlook-shows-disconnected-after-enabling-modern-authentication)

## Enable or disable modern authentication in Exchange Online for client connections in Outlook 2013 or later

### Using Exchange Online PowerShell

1. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
2. Do one of these steps:

    - Run the following command to enable modern authentication connections to Exchange Online by Outlook 2013 or later clients:

        ```PowerShell
        Set-OrganizationConfig -OAuth2ClientProfileEnabled $true
        ```

        The previous command doesn't block or prevent Outlook 2013 or later clients from using basic authentication connections.
    - Run the following command to prevent modern authentication connections (force the use of basic authentication connections) to Exchange Online by Outlook 2013 or later clients:

        ```PowerShell
        Set-OrganizationConfig -OAuth2ClientProfileEnabled $false
        ```
3. To verify the change was successful, run the following command:

    ```PowerShell
    Get-OrganizationConfig | Format-Table Name,OAuth* -Auto
    ```

### Using the Microsoft 365 admin center

In the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?linkid=2024339), go to **Settings** &gt; **Org Settings** &gt; **Modern Authentication**. In the **Modern authentication** flyout that appears, click to enable or disable **Turn on modern authentication for Outlook 2013 for Windows and later (recommended)**.