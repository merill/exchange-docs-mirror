---
layout: Conceptual
title: Manage calendar permissions in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/shared-calendars/manage-calendar-permissions
Manager: tpolitis
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Add, change, and remove Exchange Online calendar folder permissions with supported PowerShell cmdlets while preserving delegate configuration boundaries.
author: Shanefe
ms.author: shanefe
ms.service: exchange-online
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ai-usage: ai-assisted
ms.localizationpriority: medium
ms.topic: how-to
ms.date: 2026-10-07T00:00:00.0000000Z
locale: en-us
document_id: d4142503-ac30-08f7-c305-199bd7fa8912
document_version_independent_id: 43c339cd-05df-0c0c-03af-8a6e4451b84e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/shared-calendars/manage-calendar-permissions.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/shared-calendars/manage-calendar-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/shared-calendars/manage-calendar-permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: ba87fd69-a9e8-8dcf-b796-ea039ee040a4
---

# Manage calendar permissions in Exchange Online | Microsoft Learn

Use Exchange Online PowerShell to add, change, or remove a user's calendar folder permission. Configure complete delegate relationships in Outlook while the calendar owner is signed in.

## Prerequisites

Before you begin:

- Open an Exchange Online PowerShell session.
- Use an account that has permission to manage mailbox folders.
- Identify the calendar owner's primary SMTP address and the user who needs access.
- Choose the least-permissive named role that meets the requirement.

The examples use these variables:

```powershell
$CalendarOwner = "owner@contoso.com"
$User = "user@contoso.com"
```

## Review the current permission

Run [Get-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/get-mailboxfolderpermission) before you make a change:

```powershell
Get-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar" -User $User
```

If the user already has an entry, change it instead of adding a duplicate entry.

## Add a calendar permission

Use [Add-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/add-mailboxfolderpermission) to create a permission entry. This example grants permission to view all calendar items without changing them:

```powershell
Add-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar" -User $User -AccessRights Reviewer
```

The command returns an error if the user already has a permission entry. Use the change procedure for an existing entry.

## Change a calendar permission

Use [Set-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/set-mailboxfolderpermission) to replace the access rights on an existing entry. This example lets the user create and manage all calendar items:

```powershell
Set-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar" -User $User -AccessRights Editor
```

To change the organization-wide fallback access for this calendar, update the `Default` entry:

```powershell
Set-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar" -User Default -AccessRights LimitedDetails
```

Important

The `Default` entry applies to authenticated users in the organization who don't have an explicit entry. Lowering it below `AvailabilityOnly` can prevent free/busy lookups for this calendar.

Keep unauthenticated access disabled unless your organization has a reviewed requirement to change it:

```powershell
Set-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar" -User Anonymous -AccessRights None
```

## Remove a calendar permission

Use [Remove-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/remove-mailboxfolderpermission) to remove all folder permissions assigned to a user:

```powershell
Remove-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar" -User $User -Confirm:$false
```

This action removes the user's entire permission entry. Use the change procedure when you only need to assign a different role.

## Verify the result

Read the entry again after the change:

```powershell
Get-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar" -User $User
```

Confirm that `AccessRights` matches the intended role. For a broader review of the calendar access control list, see the validation article.

## Manage delegates

Use Outlook to add, change, or remove a complete delegate relationship. This path coordinates the calendar's `Editor` role, the `Delegate` flag, meeting-request delivery, and send on behalf access.

Don't use calendar folder permission commands alone as a substitute for Outlook delegate configuration. A folder-level `Editor` entry without the `Delegate` flag is editor access, not a complete delegate relationship.