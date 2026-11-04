---
layout: Conceptual
title: Understand calendar and delegate permissions in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/shared-calendars/understand-calendar-delegate-permissions
Manager: tpolitis
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how Exchange Online calendar roles, special identities, delegate flags, and mailbox-level access differ when you plan calendar access.
author: Shanefe
ms.author: shanefe
ms.service: exchange-online
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ai-usage: ai-assisted
ms.localizationpriority: medium
ms.topic: concept-article
ms.date: 2026-10-07T00:00:00.0000000Z
locale: en-us
document_id: 07d04043-7c85-a229-aa05-5f84543d6b0b
document_version_independent_id: 94ac212a-1ca8-2702-1f83-0faddf45d2a8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/shared-calendars/understand-calendar-delegate-permissions.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/shared-calendars/understand-calendar-delegate-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/shared-calendars/understand-calendar-delegate-permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: c27473fa-d51e-0247-59be-ced879917249
---

# Understand calendar and delegate permissions in Exchange Online | Microsoft Learn

Exchange Online calendar access combines folder permissions with optional delegate behavior. Choose the least-permissive role that lets a user complete the required work, and treat mailbox-level access as a separate permission.

## Calendar permission roles

A calendar permission entry grants a named role or a set of granular rights to a user. Named roles are easier to review and maintain.

| Role | Read | Create | Edit | Delete | Typical use |
| --- | --- | --- | --- | --- | --- |
| `Owner` | All items | Yes | All items | All items | Full control of the calendar folder, including folder-owner capabilities. |
| `PublishingEditor` | All items | Yes | All items | All items | Editor access plus permission to create subfolders. |
| `Editor` | All items | Yes | All items | All items | Manage all calendar items. This is also the role required for delegate flags. |
| `PublishingAuthor` | All items | Yes | Own items | Own items | Author access plus permission to create subfolders. |
| `Author` | All items | Yes | Own items | Own items | Create items and manage only items created by that user. |
| `NoneditingAuthor` | All items | Yes | No | Own items | Create items without editing them later. |
| `Reviewer` | All items | No | No | No | View access to calendar items without permission to change them. |
| `Contributor` | No | Yes | No | No | Create items without viewing existing items. |
| `LimitedDetails` | Free/busy, subject, and location | No | No | No | View availability and limited meeting details. |
| `AvailabilityOnly` | Free/busy only | No | No | No | View availability without meeting details. |
| `None` | No | No | No | No | No calendar access. |

Granular rights can combine individual capabilities such as `ReadItems`, `CreateItems`, `EditOwnedItems`, `EditAllItems`, `DeleteOwnedItems`, `DeleteAllItems`, `CreateSubfolders`, `FolderOwner`, `FolderContact`, and `FolderVisible`. Use a named role when it meets the requirement. A named role makes the intended access clearer during later reviews.

## Default and Anonymous identities

Every calendar includes two special permission entries:

- `Default` applies to authenticated users in the organization who don't have an explicit permission entry. Its typical value is `AvailabilityOnly`.
- `Anonymous` applies to callers who aren't authenticated and don't have access through a calendar-sharing relationship. Its typical value is `None`.

Changing `Default` changes the baseline calendar access for the organization. Lowering it below `AvailabilityOnly` can prevent users from retrieving free/busy information for that calendar.

Increasing `Anonymous` above `None` can expose calendar information more broadly than intended. Use a calendar-sharing relationship when an external recipient needs access.

## Delegate access

A delegate manages a calendar on behalf of its owner, who is also called the principal. An Outlook delegate has the `Editor` calendar role and a `Delegate` sharing permission flag.

The `SharingPermissionFlags` value applies only to calendar folders and requires the `Editor` role:

- `None` adds no delegate behavior.
- `Delegate` identifies the user as an Outlook delegate.
- `CanViewPrivateItems` lets the user view private calendar items. Delegate access doesn't include this capability by default.

The flags can be combined as `Delegate,CanViewPrivateItems`.

Delegate access also coordinates meeting-request delivery and related delegate settings. Configure delegate relationships from Outlook while the calendar owner is signed in. Exchange Online PowerShell is appropriate for calendar folder permission administration and validation, but it isn't the preferred method for creating a complete delegate relationship.

## Calendar permissions and mailbox permissions

Calendar folder access and mailbox-level access are different:

- A calendar role grants access only to the calendar folder.
- Full Access grants mailbox-level access but doesn't define the user's calendar role.
- Send on behalf lets a user send messages on behalf of a mailbox owner. Outlook grants this right as part of delegate configuration, but it can also exist without delegate access.

Review both folder-level and mailbox-level permissions when you evaluate a user's effective access.