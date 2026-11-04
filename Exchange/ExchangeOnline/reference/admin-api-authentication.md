---
layout: Conceptual
title: Authentication and authorization | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/admin-api-authentication
Manager: bagol
ms.subservice: exo-address-books
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.topic: article
author: chrisda
ms.author: chrisda
ms.reviewer: vivepai
description: Learn about authentication and authorization for the Exchange Online Admin API.
ms.collection:
- exchange-online
search.appverid: 
audience: Admin
f1.keywords: 
ms.custom: 
ms.service: exchange-online
ms.localizationpriority: medium
ms.date: 2026-09-25T00:00:00.0000000Z
locale: en-us
document_id: 243881e3-6eff-8ea3-d863-9aa551110b70
document_version_independent_id: 3ec5ebfa-0b82-26dd-a5bf-fab73e483ede
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/admin-api-authentication.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/admin-api-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/admin-api-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 413abaa8-3950-4789-dc24-0428993e5ae7
---

# Authentication and authorization | Microsoft Learn

Note

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

This article covers the authentication and authorization requirements for using endpoints for the Exchange Online Admin API.

The Exchange Online Admin API provides a REST-based way to run specific PowerShell cmdlets, replacing legacy Exchange Web Services (EWS) scenarios. For more information, see [Overview of the Exchange Online Admin API](admin-api-overview).

To access the Admin API, your app must establish its identity, obtain the right permissions, and follow best practices for secure token handling. At a high level, the process involves the following key steps:

1. Register an app in Microsoft Entra ID

    Create an app registration to establish an identity for your app and configure credentials (client secret or certificate). This registration enables your app to request tokens from Microsoft Entra ID.
2. Assign required API permissions

    Add the necessary OAuth scopes to your app registration:

    - Delegated flow: `Exchange.ManageV2`.
    - App-only flow: `Exchange.ManageAsAppV2`.
3. Step 3: Assign RBAC permissions

    Exchange Online uses role-based access control (RBAC) to determine which endpoints, cmdlets, and objects the caller can manage. Assign the appropriate RBAC roles to the user (for delegated access) or to the app's service principal (for app-only access).
4. Step 4: Get an access token

    Use OAuth 2.0 flows to acquire tokens from Microsoft Entra ID:

    - Delegated flow for user-based access.
    - App-only flow for service-to-service access.
5. Step 5: Use the access token

## Step 1: Register an app in Microsoft Entra ID

To call the Exchange Online Admin API, you first must register your app in Microsoft Entra ID. An app is like a class object. A service principal is like an instance of the class. For more information, see [Application and service principal objects in Microsoft Entra ID](/en-us/entra/identity-platform/app-objects-and-service-principals). For a detailed visual flow about creating applications in Microsoft Entra ID, see https://aka.ms/azuread-app.

1. Open the Microsoft Entra admin center at https://entra.microsoft.com.
2. In the search box at the top of the page, enter **App registrations** and select it from the results.

    [![Screenshot of the Microsoft Entra admin center with App Reg entered in the search box and App registrations selected in the Services section on the page.](../exchangeonline/media/admin-api-01-search-app-registration.png)](../exchangeonline/media/admin-api-01-search-app-registration.png#lightbox)
3. On the App registrations page, select **New registration**.

    [![Screenshot of the App registrations page in the Microsoft Entra admin center with New registration highlighted.](../exchangeonline/media/admin-api-02-new-app-registration.png)](../exchangeonline/media/admin-api-02-new-app-registration.png#lightbox)
4. On the **Register an application** page, configure the application settings:

    - **Name**: Enter a descriptive name (for example, Exchange Admin API Client).
    - **Supported account types**: Select one of the following values:
        - Single-organization apps: Select **Accounts in this organizational directory only**.
        - Multitenant delegated scenarios: Select **Accounts in any organizational directory**.
    - **Redirect URI (optional)**: Required for delegated flow.
        - **Platform**: Select **Web**.
        - **URI**: Enter the URL where the access token is sent (for example, `https://localhost` for testing).

    When you're finished on the **Register an application** page, select **Register**.

    [![Screenshot fo the Register an application page with the previously described values entered or selected.](../exchangeonline/media/admin-api-03-new-app-registration.png)](../exchangeonline/media/admin-api-03-new-app-registration.png#lightbox)

You're taken to the **Overview** page of the app you registered. Stay on the page for the next step.

Note

You can't create credentials for native applications because they can't be used for automated service-to-service calls.

## Step 2: Assign required API permissions

1. On **Overview** page of the app you created in the previous step, select **API permissions** from the **Manage** section.

    [![Screenshot of the Overview page of the app you registered in the previous step.](../exchangeonline/media/admin-api-04-api-permissions-starting-page.png)](../exchangeonline/media/admin-api-04-api-permissions-starting-page.png#lightbox)
2. On the **API permissions** page for the app, select **Add a permission**.

    [![Screenshot of the API permissions page with Add a permission highlighted.](../exchangeonline/media/admin-api-05-api-permissions-addition-page.png)](../exchangeonline/media/admin-api-05-api-permissions-addition-page.png#lightbox)
3. In the **Request API permissions** flyout that opens, select the **APIs my organization uses** tab, enter **Office 365 Exchange Online** in the search box, and then select it from the results.

    [![Screenshot of the APIs my organization uses tab on the Request API permission flyout with Office 365 Exchange Online entered in the search box.](../exchangeonline/media/admin-api-06-api-permissions-addition-page.png)](../exchangeonline/media/admin-api-06-api-permissions-addition-page.png#lightbox)
4. On the **What type of permissions does your application require?** flyout, make one of the following selections:

    - App-only flow: Select **Application permissions**, expand **Exchange**, select **Exchange.ManageAsAppV2**, and then select **Add permissions**.

        [![Screenshot of the What type of permissions does your application require? flyout with the values for app-only flow selected.](../exchangeonline/media/admin-api-07-api-permissions-addition-page-app-only.png)](../exchangeonline/media/admin-api-07-api-permissions-addition-page-app-only.png#lightbox)
    - Delegated flow: Select **Delegated permissions**, expand **Exchange**, select **Exchange.ManageV2**, and then select **Add permissions**.

        [![Screenshot of the What type of permissions does your application require? flyout with the values for delegated flow selected.](../exchangeonline/media/admin-api-08-api-permissions-addition-page-delegated.png)](../exchangeonline/media/admin-api-08-api-permissions-addition-page-delegated.png#lightbox)
5. Back on the **API permissions** page, verify the selections from the previous step are listed:

    - **Office 365 Exchange Online** &gt; **Exchange.ManageAsApp**:
        - Type: Application
        - Admin consent required: Yes
    - **Office 365 Exchange Online** &gt; **Exchange.ManageV2**:
        - Type: Delegated
        - Admin consent required: Yes
6. Select **Grant admin consent for**, review the confirmation dialog, and select **Yes**.

    [![Screenshot of the results of selecting Grant admin consent for.](../exchangeonline/media/admin-api-10-api-grant-admin-permission.png)](../exchangeonline/media/admin-api-10-api-grant-admin-permission.png#lightbox)

## Step 3: Assign RBAC permissions

After registering your app and granting API permissions, you must configure Exchange RBAC roles. OAuth scopes let your app obtain tokens, but RBAC determines which cmdlets and objects the caller can manage. Without the appropriate RBAC role assignments, even valid tokens fail with the error: **403 Forbidden**.

Use the steps in one of the following subsections based on the nature of your app.

### Permissions for delegated (user) flow

For delegated scenarios, the user on whose behalf the app acquires the token must have the necessary RBAC roles assigned in Exchange Online. Common role examples:

- **Recipient Management** for mailbox and folder operations.
- **Organization Management** for organization-level settings.
- **View-Only Organization Management** for read-only org operations.

Assign these roles via the Exchange admin center or Exchange Online PowerShell. For instruction, see [Manage role groups in Exchange Online](../permissions-exo/role-groups).

### Permissions for app-only flow

For app-only scenarios, the service principal representing your app must have sufficient permissions. You have the following options:

- **Assign Microsoft Entra roles (recommended for simplicity)**: Grant a built-in Microsoft Entra role to the enterprise application. For example, **Exchange Administrator** for full Exchange Online permissions:

    1. In the Microsoft Entra admin center at https://entra.microsoft.com, select **Roles & admins**.
    2. On the **Roles and administrators | All roles** page, select the **Exchange Administrator** role by clicking anywhere in the row other than the check box next to the first column.
    3. On the **Exchange Administrator | Assignments** page that opens, select **Add assignments**, choose your app, and then select **Confirm**.
- **Assign built-in or custom Exchange RBAC role groups (least privilege)**: Create or use existing custom role groups in Exchange Online that contain only the cmdlets your app needs and add the service principal to those groups. This approach avoids broad privileges and aligns with least-privilege security. For more information, see [App-only authentication in Exchange Online PowerShell](/en-us/powershell/exchange/app-only-auth-powershell-v2#assign-custom-role-groups-to-the-application-using-service-principals).

The following table lists the built-in RBAC role required for each endpoint.

| Endpoint | Required Exchange role group |
| --- | --- |
| /OrganizationConfig  /AcceptedDomain | View-Only Organization Management |
| /Mailbox  /MailboxFolderPermission  /DistributionGroupMember  /DynamicDistributionGroupMember | Recipient Management |

For even more granular control, consider using custom role groups that include only the specific management roles (cmdlet sets) your application needs. This approach follows least-privilege security and reduces risk compared to broad roles like Exchange Administrator or Global Administrator, which exceed the scope required for typical Admin API operations.

## Step 4: Get an access token

To call the Exchange Online Admin API, your app must get an OAuth 2.0 access token from Microsoft Entra ID. As previously mentioned, Admin API supports the following flows:

- Authorization code flow (delegated) with refresh token: Your app acts on behalf of a signed-in user and can also obtain a refresh token for silent renewal if the request includes the `offline_access` scope.
- Client credentials flow (app-only): Your app acts as itself (no user). Used for service/background scenarios. Refresh tokens aren't issued in this flow.

Use the `/.default` scope of the resource when requesting tokens (for example, `https://outlook.office365.com/.default`). This method tells Microsoft Entra ID to issue a token containing the application permissions (roles) previously granted for that resource.

### Authorization code flow (delegated) with refresh token

Use this flow when you need user context. To get a refresh token, you must request `offline_access` in the authorization and token requests. For more information, see [Refresh tokens in the Microsoft identity platform](/en-us/entra/identity-platform/refresh-tokens) and [Scopes and permissions in the Microsoft identity platform](/en-us/entra/identity-platform/scopes-oidc).

#### Step 1: Send the user to sign-in and consent

The user needs to authorize the app to act on their behalf. The app redirects the user to the `/authorize` endpoint in the Microsoft identity platform. Through this endpoint, Microsoft Entra ID signs the user in and requests their consent for the permissions the app requests. After consent, Microsoft Entra ID returns an authorization code to the app. The app can then redeem this code at the `/token` endpoint of the Microsoft identity platform for an access token.

The following example shows a request to the `/authorize` endpoint. In the request URL, you call the `/authorize` endpoint and specify the required and recommended properties as query parameters. For example:

```json
GET https://login.microsoftonline.com/<TenantID>/oauth2/v2.0/authorize
    ?client_id=<ClientID>
    &response_type=code
    &redirect_uri=<RedirectURI> # must exactly match the app registration
    &response_mode=query
    &scope=https://outlook.office365.com/.default offline_access
    &state=12345
```

The parameters are described in the following table:

| Parameter | Required | Description |
| --- | --- | --- |
| TenantID | Required | The organization where you request permission. The value can be the TenantID GUID or the friendly name. |
| client\_id | Required | The Client ID assigned to the app by the the registration portal. Also known as the appId. |
| response\_type | Required | Must include the value `code` for OAuth 2.0 authorization code flow. |
| redirect\_uri | Recommended | The redirect URI of the app in URL-encoded format, where authentication responses are sent and received by the app. It must match one of the redirect URIs you registered in the app registration portal. |
| scope | Required | A space-separated list of the Exchange Online Admin API permissions you want the user to consent to. These permissions can include resource permissions (`https://outlook.office365.com/.default` in this scenario) and OIDC scopes, such as `offline_access`, which indicates that the app needs a refresh token for long-lived access to resources. |
| response\_mode | Recommended | Specifies the method to send the resulting token back to the app. Valid values are `query` or `form_post`. |
| state | Recommended | A value included in the request that's also returned in the token response. It can be a string of any content. You typically use a random, unique value to prevent cross-site request forgery attacks. This property also encodes information about the user's state in the app before the authentication request occurred, such as the page or view they were on. |

- The user signs in and consents. Microsoft Entra ID redirects to your `redirect_uri` with `?code=<authorization_code>`.
- Using `offline_access` enables issuing a refresh token later. For more information, see [Refresh tokens in the Microsoft identity platform](/en-us/entra/identity-platform/refresh-tokens) and [Scopes and permissions in the Microsoft identity platform](/en-us/entra/identity-platform/scopes-oidc).

#### Step 2: Redeem the authorization code for tokens

The app uses the authorization code from the previous step to request an access token by sending a POST request to the `/token` endpoint.

```json
POST https://login.microsoftonline.com/<TenantID>/oauth2/v2.0/token
Content-Type: application/x-www-form-urlencoded

client_id=<ClientID>
&client_secret=<ClientSecret>                  # confidential clients only
&grant_type=authorization_code
&code=<authorization_code>
&redirect_uri=<RedirectURI>
&scope=https://outlook.office365.com/.default offline_access
```

The parameters are described in the following table:

| Parameter | Required | Description |
| --- | --- | --- |
| TenantID | Required | The organization where you request permission. The value can be the TenantID GUID or the friendly name. |
| client\_id | Required | The Client ID assigned to the app by the the registration portal. Also known as the appId. |
| grant\_type | Required | The value must be `authorization_code` for authorization code flow. |
| scope | Required | A space-separated list of scopes. The scopes your app requests must be equivalent to or a subset of the scopes requested in Step 1: Send the user to sign-in and consent. |
| code | Required | The authorization code you got in Step 1: Send the user to sign-in and consent. |
| redirect\_uri | Required | The same redirect URI value you used to acquire the authorization code in Step 1: Send the user to sign-in and consent. |
| client\_secret | Required for web apps | The client secret that you created in the app registration portal for your app. |

A successful response includes:

- `access_token`: Bearer. Typically, about 60 minutes.
- `refresh_token`: Present, because `offline_access` was requested.
- `id_token`: Optional. Returned if the scope `openid` was requested. For more information, see [Microsoft identity platform app types and authentication flows](/en-us/entra/identity-platform/authentication-flows-app-scenarios) and [Refresh tokens in the Microsoft identity platform](/en-us/entra/identity-platform/refresh-tokens).

Tip

Store the TenantID (`tid`) value from the token claims. You need it to form Admin API URLs and future token requests. For more information, see [Microsoft identity platform app types and authentication flows](/en-us/entra/identity-platform/authentication-flows-app-scenarios).

#### Step 3: Refresh the access token silently (no user prompt)

Access tokens are short lived, and the app must refresh them after they expire to continue accessing resources. The app refreshes an access token by submitting another POST request to the `/token` endpoint:

- Provide the `refresh_token` instead of the `code` in the request body.
- Specify `refresh_token` instead of `authorization_code` as the grant\_type.

```json
POST https://login.microsoftonline.com/<TenantID>/oauth2/v2.0/token
Content-Type: application/x-www-form-urlencoded

client_id=<ClientID>
&client_secret=<ClientSecret>
&grant_type=refresh_token
&refresh_token=<refresh_token>
&scope=https://outlook.office365.com/.default offline_access
```

The parameters are described in the following table:

| Parameter | Required | Description |
| --- | --- | --- |
| TenantID | Required | The organization where you request permission. The value can be the TenantID GUID or the friendly name. |
| client\_id | Required | The Client ID assigned to the app by the the registration portal. Also known as the appId. |
| grant\_type | Required | The value must be `refresh_token`. |
| refresh\_token | Required | The refresh\_token your app got during the token request in Step 2: Redeem the authorization code for tokens. |
| scope | Required | A space-separated list of scopes. The scopes your app requests must be equivalent to or a subset of the scopes it requested in Step 2: Redeem the authorization code for tokens. |
| client\_secret | Required for web apps | The client secret that you created in the app registration portal for your app. |

A successful response includes the following results:

- Returns a new access\_token and often a new refresh\_token to replace the old one.
- Refresh tokens last longer than access tokens. The default is about 90 days for confidential clients, and 24 hours for SPA redirect URIs. The tokens they can be revoked at any time, so handle reauthentication when needed. For more information, see [Refresh tokens in the Microsoft identity platform](/en-us/entra/identity-platform/refresh-tokens).

### Client credentials flow (app-only)

Use this flow for service-to-service calls without a user. After admin consent to application permissions (for example, `Exchange.ManageAsAppV2`) and assigning the required RBAC roles, request a token using the app's own credentials. No refresh token is issued. Request new access tokens as needed.

To acquire an access token, send a POST request to the `/token` identity platform endpoint. In this request, the client uses the client secret.

```json
POST https://login.microsoftonline.com/<TenantID>/oauth2/v2.0/token
Content-Type: application/x-www-form-urlencoded

client_id=<ClientID>
&client_secret=<ClientSecret>                   # or client assertion (certificate)
&grant_type=client_credentials
&scope=https://outlook.office365.com/.default
```

The parameters are described in the following table:

| Parameter | Condition | Description |
| --- | --- | --- |
| TenantID | Required | The organization where you request permission. The value can be the TenantID GUID or the friendly name. |
| client\_id | Required | The application ID assigned to the app by the the registration portal. |
| scope | Required | The app ID URI of the resource with the `.default` suffix. For the Exchange Online Admin API, the resource app ID URI is `https://outlook.office365.com/`, so the scope value is `https://outlook.office365.com/.default`.  This value informs the Microsoft identity platform endpoint to include all app-level permissions the admin consented to in the access token. |
| client\_secret | Required | The client secret that you generated for your app in the app registration portal. Verify the value is URL encoded. |
| grant\_type | Required | The value must be `client_credentials`. |

## Step 5: Use the access token

After you get an access token as described in Step 4: Get an access token, include the access token in the Authorization header for each subsequent API call:

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/OrganizationConfig
Authorization: Bearer <access_token>
Content-Type: application/json

 { "CmdletInput": { "CmdletName": "Get-OrganizationConfig" } }
```

## Use the Microsoft Authentication Library (MSAL)

This article contains the required protocol details when you manually create an issue raw HTTP requests to get tokens for client secrets. In production apps, use a built-in or supported authentication library to get security tokens and call protected web APIs. For example, the [Microsoft Authentication Library (MSAL)](/en-us/entra/identity-platform/msal-overview).

The MSAL and other supported authentication libraries simplify the process by handling details so you can focus on the functionality of your app. For example:

- Validation.
- Cookie handling.
- Token caching.
- Secure connections.

Microsoft maintains a wide selection of code samples that demonstrate supported authentication libraries with the Microsoft identity platform. To access these code samples, see [Microsoft identity platform code samples](/en-us/entra/identity-platform/sample-v2-code?tabs=apptype#service--daemon).

For examples on how to get tokens using certificates, see [Microsoft identity platform and the OAuth 2.0 client credentials flow](/en-us/entra/identity-platform/v2-oauth2-client-creds-grant-flow).