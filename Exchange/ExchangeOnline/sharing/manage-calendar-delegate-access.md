---
layout: Conceptual
title: Manage calendar sharing and delegate access with Microsoft Graph | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/manage-calendar-delegate-access
Manager: dcscontentpm
ms.subservice: sharing
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how to use Microsoft Graph to manage calendar permissions, access shared calendars, create events, and troubleshoot common API responses.
author: Cloud-Writer
ms.author: meerak
audience: ITPro
ms.reviewer: shanefe
ms.localizationpriority: medium
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
ms.service: exchange-online
ms.topic: how-to
ms.date: 2026-10-27T00:00:00.0000000Z
locale: en-us
document_id: 58633a5a-17f0-1158-c5e6-4458fbb8afd4
document_version_independent_id: d942930e-3e7e-7ce4-c1ec-69d0cb79d91a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/manage-calendar-delegate-access.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/manage-calendar-delegate-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/manage-calendar-delegate-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 2485e91d-9389-e2c5-9223-b602fe4b0805
---

# Manage calendar sharing and delegate access with Microsoft Graph | Microsoft Learn

Microsoft Graph can read and manage shared or delegated Outlook calendars. Use the Microsoft Graph v1.0 endpoints for new integrations.

A calendar owner can share a calendar with another user and assign a permission role. A delegate can manage meetings in the owner's primary calendar. Sharing and delegation must be established before an application accesses the calendar. The owner sends an invitation, and the recipient accepts it or explicitly adds the calendar in Outlook.

## Before you begin

- Register the application in Microsoft Entra ID.
- Choose delegated or application access according to the application's sign-in model.
- Grant only the Microsoft Graph permissions required by the operation.
- Confirm that the calendar owner has shared or delegated the calendar to the user when the application uses delegated access.
- Use the calendar owner's user ID or user principal name and the correct calendar ID.

The least-privileged permission depends on the endpoint and operation. For example:

| Operation | Least-privileged Microsoft Graph permission |
| --- | --- |
| List a user's calendars | `Calendars.ReadBasic` |
| List calendar permissions | `Calendars.ReadBasic` |
| Create, update, or delete a calendar permission | `Calendars.ReadWrite` |
| Create an event | `Calendars.ReadWrite` |
| Read a calendar view | `Calendars.ReadBasic` |

Check the permissions table in the documentation for each endpoint. Requirements can differ for user and group calendars and between delegated and application access.

## Calendar permission roles

Microsoft Graph represents each share recipient or delegate with a `calendarPermission` resource. Supported roles include:

| Role | Access |
| --- | --- |
| `none` | No access |
| `freeBusyRead` | View free/busy status |
| `limitedRead` | View free/busy status, titles, and locations |
| `read` | View event details except private-event details |
| `write` | View and edit non-private events |
| `delegateWithoutPrivateEventAccess` | Delegate write access without private-event details |
| `delegateWithPrivateEventAccess` | Delegate write access including private-event details |
| `custom` | Custom calendar permissions |

Only the calendar owner can list, create, update, or delete calendar permissions on behalf of the owner. Listing permissions on behalf of a recipient or delegate returns an empty collection.

## Manage calendar permissions

### List permissions

```http
GET https://graph.microsoft.com/v1.0/users/{userId}/calendar/calendarPermissions
```

### Create a permission

The following request shares the signed-in user's primary calendar with read access:

```http
POST https://graph.microsoft.com/v1.0/me/calendar/calendarPermissions
Content-Type: application/json

{
  "emailAddress": {
    "name": "Delegate Name",
    "address": "delegate@contoso.com"
  },
  "role": "read"
}
```

### Update a permission

Only the `role` property can be updated. To change another property, delete the permission and create a new one.

```http
PATCH https://graph.microsoft.com/v1.0/users/{userId}/calendar/calendarPermissions/{permissionId}
Content-Type: application/json

{
  "role": "write"
}
```

### Delete a permission

```http
DELETE https://graph.microsoft.com/v1.0/users/{userId}/calendar/calendarPermissions/{permissionId}
```

## Access calendars and events

### List calendars

List the calendars available through the requested user's calendar collection:

```http
GET https://graph.microsoft.com/v1.0/users/{userId}/calendars
```

For the signed-in user, use:

```http
GET https://graph.microsoft.com/v1.0/me/calendars
```

### Read a calendar view

Use `calendarView` to return event instances in a specified time range. Include ISO 8601 offsets; if an offset is omitted, Microsoft Graph interprets the value as UTC.

```http
GET https://graph.microsoft.com/v1.0/users/{ownerId}/calendar/calendarView?startDateTime=2026-05-01T00:00:00Z&endDateTime=2026-05-31T23:59:59Z&$select=subject,start,end,organizer
```

### Create an event

An application with the required permission can create an event in the specified user's primary calendar:

```http
POST https://graph.microsoft.com/v1.0/users/{ownerId}/calendar/events
Content-Type: application/json

{
  "subject": "Team meeting",
  "start": {
    "dateTime": "2026-05-01T10:00:00",
    "timeZone": "Pacific Standard Time"
  },
  "end": {
    "dateTime": "2026-05-01T11:00:00",
    "timeZone": "Pacific Standard Time"
  },
  "attendees": [
    {
      "emailAddress": {
        "address": "attendee@contoso.com",
        "name": "Attendee Name"
      },
      "type": "required"
    }
  ]
}
```

## Troubleshoot common responses

### 401 Unauthorized or InvalidAuthenticationToken

1. Acquire a new access token.
2. Confirm that the token audience is Microsoft Graph.
3. Confirm that the token contains the required delegated scopes or application roles.
4. Verify the application's Microsoft Entra consent configuration.

### 403 Forbidden

1. Compare the granted Microsoft Graph permissions with the endpoint's permissions table.
2. For delegated access, confirm that the signed-in user has access to the owner's calendar.
3. Confirm that the request uses the intended delegated or application access model.
4. If the operation manages calendar permissions, confirm that it is performed on behalf of the calendar owner.

### 404 Not Found

1. Verify the user ID or user principal name.
2. List the user's calendars and use the returned calendar ID.
3. Confirm that the shared calendar was accepted or explicitly added in Outlook.
4. Confirm that the calendar or event has not been deleted.

### 429 Too Many Requests

Wait for the number of seconds specified by the `Retry-After` response header, and then retry the request. If the response does not include `Retry-After`, use exponential backoff. Avoid continuous polling and unnecessary collection scans.

## Implementation guidance

- Request only the permissions needed by the application.
- Use `$select` to request only required properties when the endpoint supports it.
- Follow the URL in `@odata.nextLink` until it is no longer returned when reading a paged collection.
- Treat access tokens and request headers as sensitive data. Remove tokens and personal data before sharing diagnostic output.
- Use [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to test requests with a tenant administrator-approved account and permissions.

## Microsoft documentation

- [Share or delegate a calendar in Outlook](/en-us/graph/outlook-share-or-delegate-calendar)
- [Calendar permission resource](/en-us/graph/api/resources/calendarpermission)
- [List calendar permissions](/en-us/graph/api/calendar-list-calendarpermissions)
- [Create a calendar permission](/en-us/graph/api/calendar-post-calendarpermissions)
- [Update a calendar permission](/en-us/graph/api/calendarpermission-update)
- [Delete a calendar permission](/en-us/graph/api/calendarpermission-delete)
- [List calendars](/en-us/graph/api/user-list-calendars)
- [List a calendar view](/en-us/graph/api/calendar-list-calendarview)
- [Create an event](/en-us/graph/api/user-post-events)
- [Microsoft Graph permissions reference](/en-us/graph/permissions-reference)
- [Microsoft Graph paging](/en-us/graph/paging)
- [Microsoft Graph throttling guidance](/en-us/graph/throttling)
- [Share an Outlook calendar with other people](https://support.microsoft.com/office/share-an-outlook-calendar-with-other-people-353ed2c1-3ec5-449d-8c73-6931a0adab88)

## Related calendar-sharing articles

- [Calendar sharing overview](/en-us/exchange/sharing/calendar-share-overview)
- [Publishing and subscribing](/en-us/exchange/sharing/publish-subscribe-calendars)
- [External sharing](/en-us/exchange/sharing/configure-external-calendar-share)
- [Resolve issues with calendar sharing in classic Outlook for Windows](/en-us/troubleshoot/exchange/calendars/sharing/resolve-legacy-calendar-share-issues)
- [Resolve issues with modern calendar sharing](/en-us/troubleshoot/exchange/calendars/sharing/resolve-modern-calendar-share-issues)