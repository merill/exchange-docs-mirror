---
layout: Conceptual
title: MailboxFolderPermission endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/admin-api-endpoints-mailbox-folder-permission
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
description: Learn about the MailboxFolderPermission endpoint in the Exchange Online Admin API.
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
document_id: 125d1d57-10ea-32c5-60a2-4bc26c078bc2
document_version_independent_id: 8812fd09-ef69-5fb2-034d-2b31a5cddf30
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/admin-api-endpoints-mailbox-folder-permission.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/admin-api-endpoints-mailbox-folder-permission
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/admin-api-endpoints-mailbox-folder-permission.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: 66b6973a-3611-f956-c418-61af5cf22b54
---

# MailboxFolderPermission endpoint | Microsoft Learn

Note

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

The MailboxFolderPermission endpoint in the Exchange Online Admin API lets you manage permissions on mailbox folders.

Typical use cases include:

- List existing permissions on a mailbox folder.
- Grant permissions to a user or group on a mailbox folder.
- Modify permissions for an existing user or group on a mailbox folder.
- Remove permissions for an existing user or group from a mailbox folder.

The Exchange Online Admin API provides a REST-based way to execute specific PowerShell cmdlets, replacing legacy Exchange Web Services (EWS) scenarios. For more information, see [Overview of the Exchange Online Admin API](admin-api-overview).

## Endpoint URL

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/MailboxFolderPermission
```

Tip

Use the base URL for your environment as described in [Supported environments and base URLs](admin-api-get-started#supported-environments-and-base-urls).

## Request model

### Headers

```json
Authorization: Bearer <auth token>
Content-Type: application/json
X-AnchorMailbox: <routing hint>
```

For **X-AnchorMailbox** values, see [X-AnchorMailbox routing hint](admin-api-get-started#x-anchormailbox-routing-hint).

### Body

Note

The Identity examples below use \\ as required by JSON syntax for a literal backslash. The actual folder path the API receives uses a single \ (for example, alex@contoso.com:\Calendar). If you're using a tool or SDK that serializes JSON for you (for example, PowerShell, Python, or Postman's raw JSON editor), write a single \ in your code — the serializer adds the extra \ automatically. If you're constructing raw JSON (for example, in a curl request body), use \\.

- **Get-MailboxFolderPermission**:

    ```json
    {
      "CmdletInput": {
        "CmdletName": "Get-MailboxFolderPermission",
        "Parameters": {
          "Identity": "alex@contoso.com:\\Calendar",   // Required. Format: <mailbox>:\<FolderPath>
          "ResultSize": <Integer | "Unlimited">        // optional (pagination)
        }
      }
    }
    ```
- **Add-MailboxFolderPermission**:

    ```json
    {
      "CmdletInput": {
        "CmdletName": "Add-MailboxFolderPermission",
        "Parameters": {
          "Identity": "alex@contoso.com:\\Calendar",  // target folder
          "User": "delegate1@contoso.com",            // grantee
          "AccessRights": "Editor",                    // role or granular rights
          "SharingPermissionFlags": "ViewPrivateItems" // Calendar-only flag(s)
        }
      }
    }
    ```
- **Set-MailboxFolderPermission**:

    ```json
    {
      "CmdletInput": {
        "CmdletName": "Set-MailboxFolderPermission",
        "Parameters": {
          "Identity": "alex@contoso.com:\\Calendar",
          "User": "delegate1@contoso.com",
          "AccessRights": "PublishingEditor",          // optional
          "SharingPermissionFlags": "ReceiveCopiesOfMeetingMessages", // optional (Calendar-only)
          "SendNotificationToUser": false              // optional
        }
      }
    }
    ```
- **Remove-MailboxFolderPermission**:

    ```json
    {
      "CmdletInput": {
        "CmdletName": "Remove-MailboxFolderPermission",
        "Parameters": {
          "Identity": "alex@contoso.com:\\Calendar",
          "User": "delegate1@contoso.com",
          "SendNotificationToUser": true               // optional
        }
      }
    }
    ```

### Pagination

The *ResultSize* parameter on the **Get-MailboxFolderPermission** cmdlet controls pagination. By default, up to 1,000 results are returned.

If more results are available, the response includes an `@odata.nextLink` property with a continuation URL. To fetch the next page, issue a new POST request to the URL in `@odata.nextLink` with the same body.

### Property selection

This endpoint supports the `$select` query parameter to return only specific properties in the response.

## Supported cmdlets and parameters

The following list describes the cmdlets and parameters supported by this endpoint. Other cmdlets in the body of this endpoint result in an error.

- [Get-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/get-mailboxfolderpermission):

    Only the parameters for **Get-MailboxFolderPermission** described in the following table are available through the REST endpoint:

    | Parameter | Required | Type | Description |
    | --- | --- | --- | --- |
    | Identity | Required | String | Target folder using the syntax: `<Mailbox UPN or Alias or Email address or Name>:\<FolderPath>`. For example, `alex@contoso.com:\Calendar` or `alex:\Inbox\Reports`. |
    | ResultSize | Optional | Integer or Unlimited | Limits the number of results returned. Valid values are an integer (for example, 10) or the value `"Unlimited"`. |
- [Add-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/add-mailboxfolderpermission):

    Only the parameters for **Add-MailboxFolderPermission** described in the following table are available through the REST endpoint:

    | Parameter | Required | Type | Description |
    | --- | --- | --- | --- |
    | Identity | Required | String | Target folder using the syntax: `<mailbox UPN or alias>:\<FolderPath>`. For example, `alex@contoso.com:\Calendar` or `alex:\Inbox\Reports`. |
    | User | Required | User or group who gets permission to the mailbox folder. Valid values are the UPN or email address, or well-known security principals (for example, `Default` or `Anonymous`). |  |
    | AccessRights | Required | String or array. | One of the following types of values:<br>    - **Role**: For example, `Owner`, `Editor`, or `Reviewer`.<br>    - **Granular rights**: For example, `CreateItems`, `DeleteAllItems`, or `FolderVisible`. Multiple values use the syntax: `["Role1","Role2"...]` |
    | SharingPermissionFlags | Optional | String or array | **Calendar only**. Configure `ViewPrivateItems` and/or `ReceiveCopiesOfMeetingMessages` |
- [Set-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/set-mailboxfolderpermission):

    Only the parameters for **Set-MailboxFolderPermission** described in the following table are available through the REST endpoint:

    | Parameter | Required | Type | Description |
    | --- | --- | --- | --- |
    | Identity | Required | String | Target folder using the syntax: `<mailbox UPN or alias>:\<FolderPath>`. For example, `alex@contoso.com:\Calendar` or `alex:\Inbox\Reports`. |
    | User | Required | User or group who gets permission to the mailbox folder. Valid values are the UPN or email address, or well-known security principals (for example, `Default` or `Anonymous`). |  |
    | AccessRights | Required | String or array. | One of the following types of values:<br>    - **Role**: For example, `Owner`, `Editor`, or `Reviewer`.<br>    - **Granular rights**: For example, `CreateItems`, `DeleteAllItems`, or `FolderVisible`. Multiple values use the syntax: `["Role1","Role2"...]` |
    | SharingPermissionFlags | Optional | String or array | **Calendar only**. Configure `ViewPrivateItems` and/or `ReceiveCopiesOfMeetingMessages` |
    | SendNotificationToUser | Optional | Boolean | The value `True` sends a notification to the user or group who gets permission about the change. **NOTE**: This parameter is in staged rollout and might not be available in all organizations. |
- [Remove-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/remove-mailboxfolderpermission):

    Only the parameters for **Remove-MailboxFolderPermission** described in the following table are available through the REST endpoint:

    | Parameter | Required | Type | Description |
    | --- | --- | --- | --- |
    | Identity | Required | String | Target folder using the syntax: `<mailbox UPN or alias>:\<FolderPath>`. For example, `alex@contoso.com:\Calendar` or `alex:\Inbox\Reports`. |
    | User | Required | User or group who gets permission to the mailbox folder. Valid values are the UPN or email address, or well-known security principals (for example, `Default` or `Anonymous`). |  |
    | SendNotificationToUser | Optional | Boolean | The value `True` sends a notification to the user or group who gets permission about the change. **NOTE**: This parameter is in staged rollout and might not be available in all organizations. |

## Response overview

Note

During Preview, the endpoint includes the full **Get‑MailboxFolderPermission** cmdlet output in the API response. During the transition to public release, the response will be limited to the core properties listed in this section (properties needed for the EWS‑equivalent scenario). We recommend you use the properties listed in this section only. We'll document any changes to the available properties.

- The **Get-MailboxFolderPermission** response is a pageable JSON array of permission entries for the specified mailbox folder. Each entry typically includes the grantee, access rights, folder identity, and metadata. The following properties are returned:

    - **Identity**: The target folder identity using the syntax: `<mailbox>:\<FolderPath>`.
    - **FolderName**: The folder display name. For example, `Inbox` or `Calendar`.
    - **User**: Unique identity of the user or group who gets permissions on the folder. For example, display name, SMTP address, or UPN.
    - **AccessRights**: The Role or granular rights granted to the user or group on the mailbox folder. For example, `Reviewer`, `Editor`, or `CreateItems`.
    - **SharingPermissionFlags**: Calendar-only flags. For example, `ViewPrivateItems` or `ReceiveCopiesOfMeetingMessages`.
    - **IsValid**: Indicates whether the permission entry is valid.
    - **ObjectState**: Permission entry state (internal state metadata).
- The **Add-MailboxFolderPermission**, **Set-MailboxFolderPermission**, and **Remove-MailboxFolderPermission** cmdlets return `HTTP 200 OK` on success.

    - By default, these operations don't return a payload.
    - Depending on the operation and service behavior, **Set-MailboxFolderPermission** might return the updated permission entry.

## Examples

- **Example 1: Get paged calendar permissions**:

    This example returns up to 50 permission entries on the Calendar folder of the specified mailbox. Use `@odata.nextLink` to continue.

    ```json
    POST /adminapi/v2.0/<TenantID>/MailboxFolderPermission HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Get-MailboxFolderPermission",
        "Parameters": {
          "Identity": "alex@contoso.com:\\Calendar",
          "ResultSize": 50
        }
      }
    }
    ```
- **Example 2: Add Editor permission with ViewPrivateItems**:

    This example grants the **Editor** role to the specified delegate and enables viewing private items (Calendar-only flag).

    ```json
    POST /adminapi/v2.0/<TenantID>/MailboxFolderPermission HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Add-MailboxFolderPermission",
        "Parameters": {
          "Identity": "alex@contoso.com:\\Calendar",
          "User": "delegate1@contoso.com",
          "AccessRights": "Editor",
          "SharingPermissionFlags": "ViewPrivateItems"
        }
      }
    }
    ```
- **Example 3: Update an existing delegate's permissions without notification**:

    This example modifies the specified delegate's role on the specified mailbox to PublishingEditor and to receive copies of meeting invites. The delegate isn't notified about the change.

    ```json
    POST /adminapi/v2.0/<TenantID>/MailboxFolderPermission HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Set-MailboxFolderPermission",
        "Parameters": {
          "Identity": "alex@contoso.com:\\Calendar",
          "User": "delegate1@contoso.com",
          "AccessRights": "PublishingEditor",
          "SharingPermissionFlags": "ReceiveCopiesOfMeetingMessages",
          "SendNotificationToUser": false
        }
      }
    }
    ```
- **Example 4: Remove a delegate's permissions with notification**:

    This example removes all of the specified delegate's permissions from the specified mailbox folder. The delegate is notified about the change.

    ```json
    POST /adminapi/v2.0/<TenantID>/MailboxFolderPermission HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Remove-MailboxFolderPermission",
        "Parameters": {
          "Identity": "alex@contoso.com:\\Inbox",
          "User": "delegate1@contoso.com",
          "SendNotificationToUser": true
        }
      }
    }
    ```