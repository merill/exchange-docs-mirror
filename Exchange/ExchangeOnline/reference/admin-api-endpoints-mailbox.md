---
layout: Conceptual
title: Mailbox endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/admin-api-endpoints-mailbox
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
description: Learn about the Mailbox endpoint in the Exchange Online Admin API.
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
document_id: 2d76b0f5-f766-88c0-3562-8138320f0227
document_version_independent_id: 338ba993-349c-808b-89aa-c6d8d46039ed
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/admin-api-endpoints-mailbox.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/admin-api-endpoints-mailbox
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/admin-api-endpoints-mailbox.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 882025f2-91f3-bd58-1e62-13b793917280
---

# Mailbox endpoint | Microsoft Learn

Note

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

The Mailbox endpoint in the Exchange Online Admin API lets you view and manage Send on behalf delegates.

Typical use cases include:

- List mailboxes or retrieve details for a specific mailbox.
- Inspect delegate configuration for SendOnBehalfTo, including optional display names for delegates.
- Update Send on behalf delegates by overwriting the full delegate list or making incremental changes (add/remove).

The Exchange Online Admin API provides a REST-based way to execute specific PowerShell cmdlets, replacing legacy Exchange Web Services (EWS) scenarios. For more information, see [Overview of the Exchange Online Admin API](admin-api-overview).

## Endpoint URL

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/Mailbox
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

- **Get-Mailbox**:

    ```json
    {
      "CmdletInput": {
        "CmdletName": "Get-Mailbox",
        "Parameters": {
          "Identity": "alex@contoso.com",                        //optional
          "ResultSize": <Integer | "Unlimited">,                 //optional (pagination)
          "IncludeGrantSendOnBehalfTowithDisplayNames": true     //optional
        }
      }
    }
    ```
- **Set-Mailbox (overwrite delegates)**:

    ```json
    {
      "CmdletInput": {
        "CmdletName": "Set-Mailbox",
        "Parameters": {
          "Identity": "alex@contoso.com",      //required
          "GrantSendOnBehalfTo": [             //required
            "delegate1@contoso.com",
            "delegate2@contoso.com"
          ]
        }
      }
    }
    ```
- **Set-Mailbox (add/remove delegates)**:

    ```json
    {
      "CmdletInput": {
        "CmdletName": "Set-Mailbox",
        "Parameters": {
          "Identity": "alex@contoso.com",                //required
          "GrantSendOnBehalfTo": {                       //required
            "add": ["delegate3@contoso.com"],
            "remove": ["delegate1@contoso.com"],
            "@odata.type": "#Exchange.GenericHashTable"
          }
        }
      }
    }
    ```

### Pagination

The *ResultSize* parameter on the **Get-Mailbox** cmdlet controls pagination. By default, up to 1,000 results are returned.

If more results are available, the response includes an `@odata.nextLink` property with a continuation URL. To fetch the next page, issue a new POST request to the URL in `@odata.nextLink` with the same body.

### Property selection

This endpoint supports the `$select` query parameter to return only specific properties in the response.

## Supported cmdlets and parameters

The following list describes the cmdlets and parameters supported by this endpoint. Other cmdlets in the body of this endpoint result in an error.

- [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox):

    Only the parameters for **Get-Mailbox** described in the following table are available through the REST endpoint:

    | Parameter | Required | Type | Description |
    | --- | --- | --- | --- |
    | Identity | Optional | String | Specifies the mailbox to retrieve information about. Valid values are name, distinguished name, alias, user principal name (UPN), GUID, or other unique identifier. If omitted and subject to *ResultSize*, the cmdlet returns all mailboxes. |
    | ResultSize | Optional | Integer or Unlimited | Limits the number of results returned. Valid values are an integer (for example, 10) or the value `"Unlimited"`. |
    | IncludeGrantSendOnBehalfToWithDisplayNames | Optional | Boolean | The value `True` includes SendOnBehalfTo delegate entries with their display names. **NOTE**: This parameter is in staged rollout and might not be available in all organizations. |
- [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox):

    Only the parameters for **Set-Mailbox** described in the following table are available through the REST endpoint:

    | Parameter | Required | Type | Description |
    | --- | --- | --- | --- |
    | Identity | Optional | String | Specifies the target mailbox. Valid values are name, distinguished name, alias, UPN, GUID, or other unique identifier. |
    | GrantSendOnBehalfTo | Required | Collection or hash table | - **Overwrite**: List of SMTP address for the complete delegate list. For example, `["bob@contoso.com","carol@contoso.com"]`.<br>    - **Add/remove**: Hash table with `add` and/or `remove` arrays to modify the delegate list. For example, `{ "add" : ["dave@contoso.com"], remove : ["carol@contoso.com"] }`. |

## Response overview

Note

During Preview, the endpoint includes the full **Get-Mailbox** cmdlet output in the API response. During the transition to public release, the response will be limited to the core properties listed in this section (properties needed for the EWS‑equivalent scenario). We recommend you use the properties listed in this section only. We'll document any changes to the available properties.

- The **Get-Mailbox** response is a JSON object or a list array with mailbox properties. The following properties are returned:

    - **Identity**: Canonical identifier for the mailbox (often the alias or distinguished name).
    - **Id**: Service identifier for the mailbox object.
    - **Name**: Unique Exchange display name for the mailbox.
    - **DisplayName**: User-friendly display name.
    - **UserPrincipalName**: Account associated with the mailbox.
    - **Alias**: Unique mailbox alias.
    - **ExternalDirectoryObjectId**: Microsoft Entra ID object GUID for the mailbox.
    - **RecipientType**: For possible mailbox values, see [RecipientType](/en-us/powershell/module/exchangepowershell/get-recipient#-recipienttype).
    - **RecipientTypeDetails**: For possible mailbox values, see [RecipientTypeDetails](/en-us/powershell/module/exchangepowershell/get-recipient#-recipienttypedetails).
    - **EmailAddresses**: All proxy addresses for the recipient (including SMTP: and smtp: entries).
    - **PrimarySmtpAddress**: Primary SMTP address for the recipient (corresponds to the SMTP: value in **EmailAddresses**).
    - **MaxSendSize**: Maximum message size the mailbox can send.
    - **GrantSendOnBehalfTo**: List of delegates (SMTP addresses) granted Send on behalf permissions for the mailbox.
    - **GrantSendOnBehalfToWithDisplayNames**: Same list with delegate display names (when requested).
- The **Set-Mailbox** cmdlet returns `HTTP 200 OK` on success. No response body is required for successful updates.

## Examples

- **Example 1: Simple Get-Mailbox (paged listing)**:

    This example lists the first 10 mailboxes in the organization. Use `@odata.nextLink` to continue.

    ```json
    POST /adminapi/v2.0/<TenantID>/Mailbox HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Get-Mailbox",
        "Parameters": {
          "ResultSize": 10
        }
      }
    }
    ```
- **Example 2: Get-Mailbox for a specific mailbox and include delegate display names**:

    This example returns mailbox details and SendOnBehalfTo delegates with display names.

    ```json
    POST /adminapi/v2.0/<TenantID>/Mailbox HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Get-Mailbox",
        "Parameters": {
          "Identity": "alex@contoso.com",
          "IncludeGrantSendOnBehalfTowithDisplayNames": true
        }
      }
    }
    ```
- **Example 3: Set-Mailbox: Overwrite the delegate list**:

    This example overwrites the SendOnBehalfTo list on the specified mailbox with the specified delegates.

    The result is: **200 OK**. `delegate1@contoso.com` and `delegate2@contoso.com` replace any/all existing SendOnBehalfTo delegates on the mailbox.

    ```json
    POST /adminapi/v2.0/<TenantID>/Mailbox HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Set-Mailbox",
        "Parameters": {
          "Identity": "alex@contoso.com",
          "GrantSendOnBehalfTo@odata.type": "#Collection(String)",
          "GrantSendOnBehalfTo": [
            "delegate1@contoso.com",
            "delegate2@contoso.com"
          ]
        }
      }
    }
    ```
- **Example 4: Set-Mailbox: Add delegates to the existing delegate list**:

    This example adds new SendOnBehalfTo delegates to the specified mailbox while preserving the existing delegates.

    The result is: **200 OK**. `delegate3@contoso.com` and `delegate4@contoso.com` are added to the existing list of delegates on the mailbox.

    ```json
    POST /adminapi/v2.0/<TenantID>/Mailbox HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Set-Mailbox",
        "Parameters": {
          "Identity": "alex@contoso.com",
          "GrantSendOnBehalfTo": {
            "add": [
              "delegate3@contoso.com",
              "delegate4@contoso.com"
            ],
            "@odata.type": "#Exchange.GenericHashTable"
          }
        }
      }
    }
    ```