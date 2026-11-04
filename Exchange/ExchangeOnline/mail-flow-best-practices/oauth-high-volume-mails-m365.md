---
layout: Conceptual
title: Use OAuth authentication for high volume emails for Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/oauth-high-volume-mails-m365
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
ms.author: serdars
ms.topic: how-to
author: serdars
ms.service: exchange-online
ms.assetid: e1da5f2f-c732-4010-85c9-878b2cef3fb3
ms.collection:
- exchange-online
- M365-email-calendar
description: Learn how to use OAuth authentication to connect with SMTP protocols and to access email data for Office 365 users.
f1.keywords:
- NOCSH
ms.reviewer: mgolda
audience: ITPro
ms.date: 2026-03-26T00:00:00.0000000Z
locale: en-us
document_id: 02ff9797-59fb-efdd-d5ee-0fae2df0f66d
document_version_independent_id: d461ea62-b786-a4ad-29dc-9b37820b3184
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/oauth-high-volume-mails-m365.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/oauth-high-volume-mails-m365
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/oauth-high-volume-mails-m365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 17b9d9d2-6aa4-c3bf-dfef-6285482a54bf
---

# Use OAuth authentication for high volume emails for Microsoft 365 | Microsoft Learn

Learn how to use OAuth authentication to connect with SMTP protocols and to access email data for Office 365 users.

OAuth2 support for SMTP protocols as described below is available for both Microsoft 365 (which includes Office on the web) and Outlook.com users.

If you're not familiar with the OAuth 2.0 protocol, see [OAuth 2.0 protocol on Microsoft identity platform overview](/en-us/azure/active-directory/develop/active-directory-v2-protocols). For more information about the Microsoft Authentication Libraries (MSAL), which implement the OAuth 2.0 protocol to authenticate users and access secure APIs, see [MSAL overview](/en-us/azure/active-directory/develop/msal-overview).

## Register your application

To use OAuth, an application must be registered with Microsoft Entra.

Follow the instructions listed in [Register an application with the Microsoft identity platform](/en-us/azure/active-directory/develop/quickstart-register-app) to create a new application.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) at least as a Cloud Application Administrator.
2. Browse to **Identity** &gt; **Applications** &gt; **App registrations** and select **New registration**.

    [![Screenshot of new registration.](../exchangeonline/media/hve-m365/app-registration-1.png)](../exchangeonline/media/hve-m365/app-registration-1.png#lightbox)
3. Enter a display name for your application. Users of your application might see the display name when they use the app, for example during sign-in. You can change the display name at any time and multiple app registrations can share the same name. The app registration's automatically generated Application (client) ID, not its display name, uniquely identifies your app within the identity platform.

    [![Screenshot of register an application.](../exchangeonline/media/hve-m365/register-application-1.png)](../exchangeonline/media/hve-m365/register-application-1.png#lightbox)
4. After registration, several IDs are created, some of these are required later to obtain an OAuth 2.0 token.

    [![Screenshot of several IDs.](../exchangeonline/media/hve-m365/hve-oauth.png)](../exchangeonline/media/hve-m365/hve-oauth.png#lightbox)

## Add API permissions

1. Under the left menu, select **API permissions** and select **Add a permission**.

    [![Screenshot of hveoauth api permissions.](../exchangeonline/media/hve-m365/hve-oauth-api-permissions.png)](../exchangeonline/media/hve-m365/hve-oauth-api-permissions.png#lightbox)
2. Navigate to **APIs my organization uses** and search for **Office 365 Exchange Online**.

    [![Screenshot of APIs my organization uses.](../exchangeonline/media/hve-m365/req-api-permissions.png)](../exchangeonline/media/hve-m365/req-api-permissions.png#lightbox)
3. Under **Request API permissions**, choose **Application permissions**, select **Mail.Send**, and select **Add permissions**.

    Note

    The **Mail.Send** application permission does not grant the ability to send email from all Exchange mail users. Following the described configuration, **only HVE Account type mail users will be able to send email**, unless the application is explicitly authorized for other mail users through **Exchange application access controls**. Depending on your configuration, this is enforced using either: [Application Access Policies (legacy)](/en-us/exchange/permissions-exo/application-access-policies), or [Role Based Access Control for Applications in Exchange Online](/en-us/exchange/permissions-exo/application-rbac).
4. After adding the API permission, admin needs to select **Grant admin consent for**.

    [![Screenshot of grant admin consent.](../exchangeonline/media/hve-m365/grant-admin-consent.png)](../exchangeonline/media/hve-m365/grant-admin-consent.png#lightbox)

We're supporting both: delegate permission and application permission to allow legacy OAuth third-party applications, as they use application permissions with app secrets.

**Delegate Permissions:**

1. In the **API permissions** tab, add **Mail.Send** API permission from **Office 365 Exchange Online\Delegated Permissions**.
2. In the **API permissions** tab, select **Grant admin consent**.
3. In the **Authentication** tab, enable **Allow public client flows**.
4. Use the **HVE mail user's credentials** to request a token for the audience `https://outlook.office.com/.default`.

**Application Permissions:**

1. In the **API permissions** tab, add **Mail.Send** API permission from **Office 365 Exchange Online\Application Permissions**.
2. In the **API permissions** tab, select **Grant admin consent**.
3. In the **Certificate & secrets** tab, add a new client secret.
4. Use the **client secret** to request a token for the audience `https://outlook.office.com/.default`.

## Restrict OAuth access to allowed applications

High Volume Email supports restricting OAuth authentication to a specific set of Microsoft Entra ID applications. This helps prevent unauthorized or unintended applications from using an HVE account and reduces the risk of misuse or unexpected billing. By default, any application with valid OAuth credentials and the required Exchange Online permissions can authenticate to HVE. With allowed applications, you can explicitly define which applications are permitted to send email using a specific HVE account.

### How allowed applications work

When allowed applications are configured for an HVE account:

- During OAuth authentication, HVE validates the application identity in the access token.
- Only applications that are explicitly allowed for the HVE account can authenticate successfully.
- Authentication requests from other applications are rejected. The validation is based on the service principal ID (object ID) of the Microsoft Entra ID application used to obtain the OAuth token.

Note

Allowed applications apply to OAuth authentication only. They do not affect SMTP Basic authentication using passwords.

### Configure allowed applications

Allowed applications are configured per HVE account using Exchange Online PowerShell. You can add or remove Microsoft Entra ID applications by specifying their service principal GUIDs.

Note

To specify the allowed app IDs, you must use the service principal object ID from the Overview page of the Enterprise Application node (Azure Portal) for the application registration. Do not use the object ID from the Overview page of the App Registrations node. Using the incorrect Object ID will cause an authentication failure. Learn more about [Authenticate an IMAP, POP or SMTP connection using OAuth](/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth?source=recommendations#use-client-credentials-grant-flow-to-authenticate-smtp-imap-and-pop-connections).

**Add allowed applications**

```powershell
Add-HVEAppAccess -Identity HVEaccount@contoso.com -AppIds <service-principal-id-1>,<service-principal-id-2>
```

**Remove allowed applications**

```powershell
Remove-HVEAppAccess -Identity HVEaccount@contoso.com -AppIds <service-principal-id-1>,<service-principal-id-2>
```

**View allowed applications**

```powershell
Get-HVEAccountSettings -Identity HVEaccount@contoso.com | Format-List *AllowedApps*
```

### Limits and behavior

- Each HVE account can have a maximum of 10 allowed applications configured.
- If no allowed applications are configured for an HVE account, no additional application-level restriction is enforced.

## HVE SMTP protocol exchange

To authenticate an SMTP server connection, the client must respond with an `AUTH` command in `SASL XOAUTH2` format. `SASL XOAUTH2` encodes the username and access token together in the following format:

```text
base64("user=" + userName + "^Aauth=Bearer " + accessToken + "^A^A")
```

`^A` represents a Control + A (`%x01`).

For example, the `SASL XOAUTH2` format to access `application@contoso.onmicrosoft.com` with access token `EwBAAl3BAAUFFpUAo7J3Ve0bjLBWZWCclRC3EoAA` is:

```text
base64("user=application@contoso.onmicrosoft.com^Aauth=Bearer EwBAAl3BAAUFFpUAo7J3Ve0bjLBWZWCclRC3EoAA^A^A")
```

Sample client-server message exchange that results in an authentication success:

```text
[connection begins]

C: auth xoauth2

S: 334

C: dXNlcj1hcHBsaWNhdGlvbkBjb250b3NvLm9ubWljcm9zb2Z0LmNvbQFBdXRoPUJlYXJlciBFd0JBQWwzQkFBVUZGcFVBbzdKM1ZlMGJqTEJXWldDY2xSQzNFb0FBAQE=

S: 235 2.7.0 Authentication successful

[connection continues...]
```

Sample client-server message exchange that results in an authentication failure:

```text
[connection begins]

C: auth xoauth2

S: 334

C: dXNlcj1hcHBsaWNhdGlvbkBjb250b3NvLm9ubWljcm9zb2Z0LmNvbQFBdXRoPUJlYXJlciBFd0JBQWwzQkFBVUZGcFVBbzdKM1ZlMGJqTEJXWldDY2xSQzNFb0FBAQE=

S: 535 5.7.3 Authentication unsuccessful
```