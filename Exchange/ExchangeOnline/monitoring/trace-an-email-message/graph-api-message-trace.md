---
layout: Conceptual
title: Graph-based message trace API onboarding guide | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/trace-an-email-message/graph-api-message-trace
Manager: anaruxa
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: lusassl
author: lusassl-msft
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
ms.custom: 
description: Admins can use the Graph API to trace email messages in Exchange Online.
ms.date: 2026-02-02T00:00:00.0000000Z
locale: en-us
document_id: 6b14ada1-520d-1989-ff44-f52816015fda
document_version_independent_id: 1e7b9c13-4c1e-fec6-f00d-66438cf60721
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/trace-an-email-message/graph-api-message-trace.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/trace-an-email-message/graph-api-message-trace
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/trace-an-email-message/graph-api-message-trace.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 556490d7-e1a2-7e39-e76f-faaec8073d9b
---

# Graph-based message trace API onboarding guide | Microsoft Learn

This article walks you through how to onboard to the [Graph-based Message Trace API](/en-us/graph/api/resources/exchangemessagetrace). This Microsoft Graph REST API lets you trace email messages that have passed through your Exchange Online organization within the last 90 days.

If you're new to Microsoft Graph, start with the [Microsoft Graph overview](/en-us/graph/overview).

## Prerequisites

Before you onboard to the Graph-based message trace API, make sure that the following requirements are met.

### Configure authentication

To call Microsoft Graph, your application must obtain an access token from the Microsoft identity platform. For background information, see [Authentication and authorization basics](/en-us/graph/auth/auth-concepts). This article uses app-only authentication. App-only authentication lets the app run without a signed-in user. For more information, see [Get access without a user](/en-us/graph/auth-v2-service?tabs=http). The following sections describe the required setup steps.

#### Register an application

Register an app in the Microsoft identity platform. For step-by-step instructions, see [Register an application with the Microsoft identity platform](/en-us/graph/auth-register-app-v2).

Caution

For production workloads, Microsoft recommends using a certificate over secrets. Don't use self-signed certificates. They can reduce the security of your application due to various factors like use of an outdated hash and cipher suites or lack of validation. Get certificates from a well-known trusted certificate authority.

During registration, record the following information:

- The Application (client) ID
- One of the following credentials:
    - A client secret
    - A certificate
    - A federated identity credential

#### Configure Microsoft Graph permissions

Grant your application the required application permissions in Microsoft Entra ID.

1. In the Microsoft Entra admin center, open App registrations, and then select your app.
2. Select `API permissions`, and then choose `Add a permission`.
3. Select `Microsoft Graph`, and then select `Application permissions`.
4. Add the `ExchangeMessageTrace.Read.All` permission.
5. Grant admin consent for your tenant.

#### Request an access token

Use the application ID and credential that you created during app registration to [request an access token from the Microsoft identity platform](/en-us/graph/auth-v2-service?tabs=http#step-3-request-an-access-token). Include the access token in the Authorization header when calling the Graph-based message trace API.

### Provision a service principal

To use the Graph-based message trace API, you must provision a service principal in your tenant for the Microsoft application with the following application (client) ID: `8bd644d1-64a1-4d4b-ae52-2e0cbf64e373`

This step creates a local representation of the multi-tenant Microsoft application in your tenant and enables authentication and authorization. For more background information, see [Create an enterprise application from a multitenant application.](/en-us/entra/identity/enterprise-apps/create-service-principal-cross-tenant?pivots=ms-graph).

#### Create the service principal by using Microsoft Graph PowerShell

You can provision the service principal by using the [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/get-started).

1. Connect to Microsoft Graph: 

    ```PowerShell
    Connect-MgGraph -Scopes "Application.ReadWrite.All"
    ```
2. Run the following request: 

    ```PowerShell
     Import-Module Microsoft.Graph.Applications
    
     $params = @{
       appId = "8bd644d1-64a1-4d4b-ae52-2e0cbf64e373"
     }
    
     New-MgServicePrincipal -BodyParameter $params
    ```

#### Create the service principal by using Microsoft Graph Explorer

You can provision the service principal by calling Microsoft Graph.

1. Go to [Graph explorer](https://aka.ms/ge)
2. Sign in with an account that has administrator permissions in the tenant where you want to create the service principal.
3. Run the following request:

    ```HTTP
    POST https://graph.microsoft.com/v1.0/servicePrincipals
    {
        "appId" : "8bd644d1-64a1-4d4b-ae52-2e0cbf64e373"
    }
    ```

After you create the service principal, provisioning might take several hours to complete. During this time, requests to the Graph-based message trace API can return `401 (Unauthorized)` errors:

`Service principal-less authentication failed: The service principal for App ID 8bd644d1-64a1-4d4b-ae52-2e0cbf64e373 was not found. Please create a service principal for this app in your tenant. Provisioning may take several hours to complete.`

## Call the message trace API

The Graph-based message trace API supports querying message trace data from the last **90 days**.

- If you call the API **without query parameters**, it returns data from the last **48 hours**.
- Each request can query **up to 10 days** of data. To retrieve a larger time range, split the request into multiple queries.

### Result limits and paging

By default, the API returns up to **1,000** results per request. You can control the number of returned items by using the `$top` query parameter.

- Supported range for `$top`: **1-5,000**
- Maximum results per request: **5,000**

If the total number of matching items exceeds the specified page size, the response includes an `@odata.nextLink` value.

To retrieve the next page of results, send a follow-up request by using the **entire URL** provided in `@odata.nextLink`. This URL already includes the required `$skiptoken` parameter. For more information, see [Paging Microsoft Graph data in your app](/en-us/graph/paging?tabs=http).

#### Optional Query Parameters

The following query parameters are supported when calling the Graph-based message trace API.

| Parameter | Description |
| --- | --- |
| `$filter` | Filters results by supported properties. You can filter on the following fields: `id`, `messageId`, `receivedDateTime`, `recipientAddress`, `senderAddress`, `status`, `subject`, `toIP` |
| `$top` | Specifies the maximum number of items to return in a single response. Supported values range from **1** to **5,000**. |
| `$skiptoken` | Retrieves the next page of results. Use the value provided in the `@odata.nextLink` property of the previous response. Do not create or modify this value manually. |

### Best Practices

- Use the `$top` query parameter to control the number of results returned per request.
- Narrow the query time range and apply additional filters (for example, `senderAddress`) whenever possible to reduce result size and improve performance.

### Examples

The following example shows a basic request to the Graph-based message trace API.

**Request headers:**

| Name | Description |
| --- | --- |
| Authorization | Bearer {access\_token} |

**HTTP Request:**

```HTTP
GET https://graph.microsoft.com/beta/admin/exchange/tracing/messageTraces
```

**Reponse:**

If the request is successful, the API returns an `HTTP 200 OK` response and a collection of `exchangeMessageTrace` objects in the response body:

```HTTP
HTTP/1.1 200 OK        
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#admin/exchange/tracing/messageTraces",
  "value": [
    {
      "id": "4451a062-48cb-e80d-e8c0-196330437ae6",
      "senderAddress": "sender@contoso.com",
      "recipientAddress": "recipient@contoso.com",
      "messageId": "<d9683b4c-127b-413a-ae2e-fa7dfb32c69d@contoso.com>",
      "receivedDateTime": "2025-06-13T10:30:00Z",
      "subject": "Quarterly Report",
      "size": 45678,
      "fromIP": "192.168.1.100",
      "toIP": "",
      "status": "delivered"
    }
  ]
}
```

#### Example 1: Filter messages by message trace ID

The following example retrieves a specific message trace by using the message trace ID.

```HTTP
GET https://graph.microsoft.com/beta/admin/exchange/tracing/messageTraces?$filter=id eq 'a3f6d2c1-5c3b-4f7a-9d1e-2c8f1b0a6e45'
```

#### Example 2: Filter messages by time range

To retrieve message traces for a specific time period, filter on the `receivedDateTime` property and specify both a start and end time:

```HTTP
$filter=receivedDateTime ge {startDate} and receivedDateTime le {endDate}
```

The following constraints apply:

- The time range must not exceed **10 days**.
- `{startDate}` must not be more than **90 days** before the current date.
- `{endDate}` must not be later than the current date.
- Specify both values in **ISO 8601** format `(YYYY-MM-DDThh:mm:ssZ)`.

The following example retrieves message traces for messages received between **January 20, 2026** and **January 23, 2026** (UTC):

```HTTP
GET https://graph.microsoft.com/beta/admin/exchange/tracing/messageTraces?$filter=receivedDateTime ge 2026-01-20T00:00:00Z and receivedDateTime le 2026-01-23T00:00:00Z
```

#### Example 3: Filter messages by subject

The subject property supports the `contains`, `startswith`, and `endswith` filter functions.

The following example lists message traces for messages where the subject contains "**Weekly digest**":

```HTTP
 GET https://graph.microsoft.com/beta/admin/exchange/tracing/messageTraces?$filter=contains(subject, 'Weekly digest')
```

#### Example 4: Filter messages by multiple conditions

You can combine multiple filter conditions by using logical operators.

The following example retrieves message traces for messages that were sent to `john@contoso.com` and have a delivery status of `delivered`:

```HTTP
GET https://graph.microsoft.com/beta/admin/exchange/tracing/messageTraces?$filter=recipientAddress eq 'john@contoso.com' and status eq 'delivered' 
```

## Get message trace details

The Graph-based message trace API provides the `getDetailsByRecipient` method to retrieve detailed information about the processing steps applied to an email message as it passed through your Exchange Online organization within the last **90 days**.

To call this method, you must provide:

- The message trace ID
- The recipient email address

### Examples

The following example retrieves message trace details for a specific message and recipient.

**Request headers:**

| Name | Description |
| --- | --- |
| Authorization | Bearer {access\_token} |

**HTTP Request:**

```HTTP
GET https://graph.microsoft.com/v1.0/admin/exchange/tracing/messageTraces/7e3b2b2e-1b5e-4b17-80cc-2af6c1d9a3b1/getDetailsByRecipient(recipientAddress='robert@contoso.com')
```

**Reponse:**

If the request is successful, the API returns an HTTP 200 OK response and a collection of [exchangeMessageTraceDetail](/en-us/graph/api/resources/exchangemessagetracedetail) objects in the response body:

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#Collection(microsoft.graph.exchangeMessageTraceDetail)",
  "value": [
    {
      "id": "7e3b2b2e-1b5e-4b17-80cc-2af6c1d9a3b1",
      "messageId": "<d9683b4c-127b-413a-ae2e-fa7dfb32c69d@contoso.com>",
      "dateTime": "2025-06-13T10:30:05Z",
      "event": "Receive",
      "action": "",
      "description": "Message received by: MN2PR00MB0670.namprd00.prod.outlook.com",
      "data": "<root><MEP ... String=\"Message Body\" /></root>"
    },
    {
      "id": "7e3b2b2e-1b5e-4b17-80cc-2af6c1d9a3b1",
      "messageId": "<d9683b4c-127b-413a-ae2e-fa7dfb32c69d@contoso.com>",
      "dateTime": "2025-06-13T10:30:10Z",
      "event": "Deliver",
      "action": "",
      "description": "The message was successfully delivered.",
      "data": "<root><MEP ... String=\"Message Body\" /></root>"
    }
  ]
}
```

## Throttling

To protect Exchange Online resources, ensure service availability, and provide a predictable experience for all tenants, the Graph-based message trace API enforces rate-based throttling. The message trace API and message trace detail API each have their own throttling limits, and requests to one API do not count against the quota of the other. For more information see [Microsoft Graph throttling guidance](/en-us/graph/throttling).

### Throttling limits

For each tenant:

- A maximum of **100 requests** is allowed within a **5-minute rolling window**.
- Throttling is applied only when the request rate exceeds this limit.
- If your automation issues requests more frequently, update it to stay within the allowed threshold.

### Request volume versus result size

The number of requests and the number of returned results are evaluated separately:

- A single message trace request can return up to **5,000 results**.
- Within a 5-minute rolling window, you can retrieve up to **500,000 results** (100 requests × 5,000 results).
- When requests are evenly distributed over time, you can retrieve up to **144 million results per day**.

These limits ensure fairness and maintain service availability across all tenants.

### Throttling behavior

If your requests exceed the throttling limit, the API returns the following error message:

`Your recent queries have surpassed the permitted limit, please try again later.`

Retry the request after the throttling window resets.

### Summary of limits

| **Method** | **Limit type** | **Limit** |
| --- | --- | --- |
| Message Trace | Per tenant | 100 requests per 5 minutes |
| Message Trace Detail | Per tenant | 100 requests per 5 minutes |