---
layout: Conceptual
title: Get started | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/admin-api-get-started
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
description: Learn how to make successful calls in the Exchange Online Admin API.
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
document_id: 370e4528-47c6-6af6-5b35-6931edbcd6fd
document_version_independent_id: fbb1b81a-20b0-f958-ef12-2dbf0954d64a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/admin-api-get-started.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/admin-api-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/admin-api-get-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 1b8263c6-3a9a-2a23-32ff-2936f6bb82e0
---

# Get started | Microsoft Learn

Note

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

This article shows you how to make your first successful Exchange Online Admin API call and explains the key behaviors and patterns that apply across all endpoints.

This article helps you with the following tasks:

- How to form a request (headers and body) to call the Exchange Online Admin API.
- Supported environments and base URLs to use for each environment.
- How pagination and property selection work.
- When and how to use **X-AnchorMailbox** for routing.
- Common issues and best practices.

The Exchange Online Admin API provides a REST-based way to execute specific PowerShell cmdlets, replacing legacy Exchange Web Services (EWS) scenarios. For more information, see [Overview of the Exchange Online Admin API](admin-api-overview).

## Prerequisite: Set up authentication and permissions

Before you can make your first call to the Exchange Online Admin API, you need to set up authentication and permissions so your app or script can securely access your organization. For complete instructions, see [Authentication and authorization for the Exchange Online Admin API](admin-api-authentication).

Here are the summarized steps:

1. **Register an app in Microsoft Entra ID**: Create an app registration for delegated or app-only access.
2. **Grant API permissions**:
    - **Delegated**: `Exchange.ManageV2`.
    - **App-only**: `Exchange.ManageAsAppV2`.
3. **Obtain admin consent**: Ensure the permissions are consented to at the organization level.
4. **Assign RBAC roles**: Assign roles to the user (delegated) or service principal (app-only) that cover the objects you manage.
5. **Acquire an access token**: Use delegated or app-only flows to get a valid OAuth token.
6. **Know your organization context**: Identify your TenantID (GUID) and base URL.

## Supported environments and base URLs

The Exchange Online Admin API is available in all Exchange Online environments. Each environment uses a different base URL for requests, so make sure you use the correct URL for your environment as described in the following table:

| Environment | Base URL |
| --- | --- |
| Microsoft 365 or Microsoft 365 GCC | `https://outlook.office365.com` |
| Office 365 operated by 21Vianet (China) | `https://outlook.office365.cn` |
| Microsoft 365 GCC High | `https://outlook.office365.us` |
| Microsoft 365 DoD | `https://outlook-dod.office365.us` |

The final request URL depends on your environment and includes your TenantID and the endpoint name using the following syntax:

```json
POST <BaseUrl>/adminapi/v2.0/<TenantID>/<EndpointName>
```

For example:

```json
POST https://outlook.office365.com/adminapi/v2.0/0550b473-9fd2-4dbb-a058-a1640b4bf458/OrganizationConfig
```

## Request model (headers and body)

Every Exchange Online Admin API call uses the POST method and follows a consistent request model. The body must include a CmdletInput envelope that specifies the cmdlet name and supported parameters within the selected REST endpoint.

For details on supported cmdlets and parameters, see [Exchange Online Admin API endpoints reference](admin-api-endpoints-reference).

- **Required headers**:

    - **Authorization**: `Bearer <access_token>`.
    - **Content-Type**: `application/json`
    - **X-AnchorMailbox**: A routing key value as described in the upcoming X-AnchorMailbox routing hint section.
- **Body**:

    ```json
    {
      "CmdletInput": {
        "CmdletName": "<Cmdlet Name>",
        "Parameters": {
          /* parameters supported for this cmdlet in the endpoint & their value */
        }
      }
    }
    ```

Note

Passing unsupported cmdlets or parameters for the endpoint results in the error: **400 Bad Request**. Always check the endpoint's specific documentation for allowed cmdlets and parameters.

## First call example

Now that you know the request structure and headers, let's make your first successful call. This example uses the Microsoft 365 base URL and retrieves your organization configuration.

```json
POST https://outlook.office365.com/adminapi/v2.0/12345678-90ab-cdef-1234-567890abcdef/OrganizationConfig
Authorization: Bearer <access_token>
Content-Type: application/json
X-AnchorMailbox: <appropriate routing key>

{
  "CmdletInput": {
    "CmdletName": "Get-OrganizationConfig"
  }
}
```

**Expected outcome**: **200 OK** and a JSON payload containing org-level properties (for example, `MailTipsAllTipsEnabled` and `MailTipsExternalRecipientsTipsEnabled`).

## X-AnchorMailbox routing hint

The **X-AnchorMailbox** header is **mandatory** for all v2.0 Admin API calls. It provides a routing hint that directs the request to the correct backend server. Without a routing hint, requests can be routed inefficiently or fail completely. Providing the correct mailbox identifier ensures the request reaches the mailbox's home server, reduces latency, avoids unnecessary hops, and improves consistency.

To add the header to your request, use the following syntax:

```json
X-AnchorMailbox: <routing key>
```

Supported routing key values are described in the following table:

| Routing key | Format | Example |
| --- | --- | --- |
| UPN (preferred) | `AAD-UPN:<user@domain>` | `AAD-UPN:alex@contoso.com` |
| SMTP | `AAD-SMTP:<user@domain>` | `AAD-SMTP:alex@contoso.com` |
| Microsoft Entra object ID / External Directory Object ID (EDOID) | `OID:<ExternalDirectoryObjectId>@<tenantId>` | `OID:80db1853-38c7-4ff3-945b-1e9a78119cb0@ab9f5dac-33ac-4f91-a9f4-8720b942f1a8` |
| Mailbox GUID | `MBX:<mailboxGuid>@<tenantId>` | `MBX:80db1853-38c7-4ff3-945b-1e9a78119cb0@ab9f5dac-33ac-4f91-a9f4-8720b942f1a8` |
| System mailbox (app-only) | `APP:SystemMailbox{<systemMailboxGuid>}@<tenantIdOrOrganization>` | `APP:SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}@contoso.onmicrosoft.com` |

Tip

Use UPN for stability across mailbox renames. Use the system mailbox format for app-only scenarios.

### When to use which routing key

- **Operations that bind to a particular mailbox**: For calls that target a specific mailbox ( [/Mailbox](admin-api-endpoints-mailbox) , [/MailboxFolderPermission](admin-api-endpoints-mailbox-folder-permission) ), use a routing key of the target mailbox. For example:

    ```json
    X-AnchorMailbox: UPN:alex@contoso.com
    ```
- **All other operations with no specific mailbox target**: Use one of the following keys based on the scenario:

    - **Delegated (user) flow**: Use a routing key of the admin who's running the API. For example:

        ```json
        X-AnchorMailbox: UPN:admin@contoso.com
        ```
    - **App-only flow**: Use a routing key for the organization's system mailbox. For example:

        ```json
        X-AnchorMailbox: APP:SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}@contoso.onmicrosoft.com
        ```

        Note

        The system mailbox GUID value is the same across all organizations and is `bb558c35-97f1-4cb9-8ff7-d53741dc928c`.

## Pagination

Some Exchange Online Admin API endpoints return large results. Endpoints that support pagination are clearly identified in the individual endpoint documentation. Pagination helps you retrieve results in smaller chunks and avoid timeouts or throttling.

- To specify the number of items per page, use the *ResultSize* parameter in your request body.
- If more results are available, the response includes an `@odata.nextLink` property with a continuation URL.
- To get the next page, POST to the `@odata.nextLink` URL using the same headers and authentication.

If you don't use the *ResultSize* parameter, the API returns a maximum of 1,000 entries by default. To retrieve all entries in a single request, use the value `Unlimited` for the *ResultSize* parameter if the value is supported.

Use the following methods for best practices with pagination:

- Keep parameters consistent for requests across pages.
- \*\*The generated @odata.nextLink is valid only for 5-10 minutes from the time of generation. If you try to use an expired link, the request might fail. To avoid errors, complete paginated calls within 5 minutes of receiving the `@odata.nextLink` property.

**Example request**:

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/Mailbox
Authorization: Bearer <access_token>
Content-Type: application/json
X-AnchorMailbox: <Routing key>

{
  "CmdletInput": {
    "CmdletName": "Get-Mailbox",
    "Parameters": {
      "ResultSize": 50
    }
  }
}
```

**Follow-up page**:

- POST to the `@odata.nextLink` URL (use same method).
- Don't change parameters between pages.

## Property selection with $select

The Exchange Online Admin API supports the `$select` query parameter on all endpoints. Use `$select` to return only the properties you need in the response payload. This strategy helps reduce the size of the response and minimizes parsing overhead on the client.

If a property specified in the `$select` clause is invalid, the service skips that property and returns the remaining valid properties.

Append `$select` as a query parameter to the endpoint URL. Separate multiple properties with commas:

```json
POST https://<base-url>/adminapi/v2.0/<TenantID>/<EndpointName>?$select=Property1,Property2,...
```

For example, replace &lt;TenantID&gt;, &lt;access\_token&gt;, and &lt;routing key&gt; with the appropriate values to return only the display name and primary SMTP address for mailboxes:

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/Mailbox?$select=DisplayName,PrimarySmtpAddress
Authorization: Bearer <access_token>
Content-Type: application/json
X-AnchorMailbox: <routing key>

{
  "CmdletInput": {
    "CmdletName": "Get-Mailbox"
  }
}
```

## Common issues and how to fix them

This section describes frequent issues you might encounter when working with the Exchange Online Admin API.

### 401 Unauthorized

- **Cause**:
    - Missing, invalid, or expired OAuth token.
    - Incorrect scope.
- **Fix**:
    - Ensure your app has right scopes assigned:
        - Delegated: `Exchange.ManageV2`.
        - App-only: `Exchange.ManageAsAppV2`.
    - Acquire a new token in case the original token expired.
    - Verify correct TenantID and app registration details are passed in the requests.

### 403 Forbidden

- **Cause**: Missing RBAC role or trying to manage objects outside your scope.
- **Fix**:
    - Assign the required RBAC roles to the user (delegated) or service principal (app-only).
    - Confirm that the object is within your management scope.

### 400 Bad Request

- **Cause**: Unsupported or incorrectly formatted parameter.
- **Fix**:
    - Check the cmdlet details for the endpoint and cmdlet combination.
    - Only include parameters supported by the cmdlet in the REST endpoint.

### Wrong base URL

- **Cause**: The wrong base URL for your environment.
- **Fix**: Use the correct base URL for your organization.

### Pagination issues

- **Cause**: Changing parameters between paged calls or ignoring `@odata.nextLink`.
- **Fix**:
    - Keep parameters consistent across all pages.
    - Always POST to the `@odata.nextLink` URL.
    - If you don't use the *ResultSize* parameter, the API defaults to 1,000 entries per page.

### Routing errors

- **Cause**: Missing or incorrect **X-AnchorMailbox** header for mailbox-scoped operations.
- **Fix**:
    - Include **X-AnchorMailbox** with the mailbox UPN (preferred) or SMTP address.
    - Validate the value before sending the request.

## Best practices

Follow the guidelines in this section to ensure reliable and efficient use of the Exchange Online Admin API.

- **Authentication and security**:

    - Use app-only authentication with certificates or managed identities for production workloads.
    - Request only the permissions you need (`Exchange.ManageV2` or `Exchange.ManageAsAppV2`).
    - Assign minimal RBAC roles to reduce risk.
- **Request design**:

    - Always use POST for all operations, including **Get-\*** cmdlets.
    - Include only parameters supported for the cmdlet in the endpoint.
    - Use **X-AnchorMailbox** for all operations.
- **Performance optimization**:

    - Use `$select` to reduce response payload size.
    - Combine `$select` with pagination for large datasets.
    - Use the *ResultSize* parameter. Otherwise, the API defaults to 1,000 entries per page.
- **Resilience and error handling**:

    - Implement retry logic for throttling (HTTP 429) and honor Retry-After.
    - Log request IDs from error responses for troubleshooting.
    - Validate parameters before sending requests to avoid 400 Bad Request.
- **Routing and environment awareness**:

    - Use the correct base URL for your organization.
    - Include **X-AnchorMailbox** for all requests to avoid routing errors.