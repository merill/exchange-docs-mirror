---
layout: Conceptual
title: DistributionGroupMember endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/admin-api-endpoints-distribution-group-member
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
description: Learn about the DistributionGroupMember endpoint in the Exchange Online Admin API.
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
document_id: 56a5d606-678b-3ce5-bacd-965690c4230b
document_version_independent_id: 678bad10-43e5-bddf-4446-ccd594f8f48f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/admin-api-endpoints-distribution-group-member.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/admin-api-endpoints-distribution-group-member
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/admin-api-endpoints-distribution-group-member.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 6a2174fb-8bf3-a56a-85a7-4ce4c6535dc3
---

# DistributionGroupMember endpoint | Microsoft Learn

Note

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

The DistributionGroupMember endpoint in the Exchange Online Admin API retrieves the members of a specified distribution group. The endpoint returns a collection of recipient objects representing group membership and related directory information.

Typical use cases include:

- Expanding distribution lists for mail routing.
- Expanding Room lists to display list of all the members.

Note

The response of this endpoint includes members who are hidden from address lists.

The Exchange Online Admin API provides a REST-based way to execute specific PowerShell cmdlets, replacing legacy Exchange Web Services (EWS) scenarios. For more information, see [Overview of the Exchange Online Admin API](admin-api-overview).

## Endpoint URL

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/DistributionGroupMember
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

```json
{
  "CmdletInput": {
    "CmdletName": "Get-DistributionGroupMember",
    "Parameters": {
      "Identity": "<distribution group identity>",    // required
      "ResultSize": <Integer | "Unlimited">           // optional (pagination)
    }
  }
}
```

### Pagination

The *ResultSize* parameter controls pagination. By default, up to 1,000 results are returned.

If more results are available, the response includes an `@odata.nextLink` property with a continuation URL. To fetch the next page, issue a new POST request to the URL in `@odata.nextLink` with the same body.

### Property selection

This endpoint supports the `$select` query parameter to return only specific properties in the response. For example:

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/DistributionGroupMember?$select=DisplayName,PrimarySmtpAddress
```

## Supported cmdlets and parameters

The supported cmdlet for this endpoint is [Get-DistributionGroupMember](/en-us/powershell/module/exchangepowershell/get-distributiongroupmember). Any other cmdlet in the body of this endpoint results in an error.

Only the parameters described in the following table are available through the REST endpoint:

| Parameter | Required | Type | Description |
| --- | --- | --- | --- |
| Identity | Required | String | Specifies the distribution group to retrieve membership information about. Valid values are the group name, email address, or GUID. Subject to *ResultSize*, the cmdlet returns all group members, including hidden recipients. |
| ResultSize | Optional | Integer or Unlimited | Limits the number of results returned. Valid values are an integer (for example, 10) or the value `"Unlimited"`. |

## Response overview

Note

During Preview, the endpoint includes the full **Get-DistributionGroupMember** cmdlet output in the API response. During the transition to public release, the response will be limited to the core properties listed in this section (properties needed for the EWS‑equivalent scenario). We recommend you use the properties listed in this section only. We'll document any changes to the available properties.

The response is a JSON array of group members. Each recipient object contains details and metadata information. The following properties are returned:

- **Identity**: Canonical identity of the recipient (used for management operations).
- **Alias**: Mail alias (if applicable).
- **EmailAddresses**: All proxy addresses for the recipient (including SMTP: and smtp: entries).
- **PrimarySmtpAddress**: Primary SMTP address for the recipient (corresponds to the SMTP: value in **EmailAddresses**).
- **DisplayName**: Recipient display name.
- **FirstName**
- **LastName**
- **Name**: Exchange display name (often mirrors DisplayName).
- **RecipientType**: For possible values, see [RecipientType](/en-us/powershell/module/exchangepowershell/get-recipient#-recipienttype).
- **RecipientTypeDetails**: For possible values, see [RecipientTypeDetails](/en-us/powershell/module/exchangepowershell/get-recipient#-recipienttypedetails).
- **HiddenFromAddressListsEnabled**: Is the recipient hidden from membership in the distribution group.

## Examples

- **Example 1: Get all members of a distribution group**:

    This example retrieves a maximum of 1,000 members of the specified distribution group because we aren't using the *ResultSize* parameter.

    ```json
    POST /adminapi/v2.0/<TenantID>/DistributionGroupMember HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Get-DistributionGroupMember",
        "Parameters": {
          "Identity": "marketing@contoso.com"
        }
      }
    }
    ```
- **Example 2: Limit results using ResultSize**:

    This example limits the results to 10 members of the specified distribution group by setting the *ResultSize* parameter to the value 10.

    ```json
    POST /adminapi/v2.0/<TenantID>/DistributionGroupMember HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>>
    
    {
      "CmdletInput": {
        "CmdletName": "Get-DistributionGroupMember",
        "Parameters": {
          "Identity": "marketing@contoso.com",
          "ResultSize": 10
        }
      }
    }
    ```