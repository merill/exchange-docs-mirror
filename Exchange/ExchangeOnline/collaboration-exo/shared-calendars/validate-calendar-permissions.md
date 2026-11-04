---
layout: Conceptual
title: Validate calendar permissions in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/shared-calendars/validate-calendar-permissions
Manager: tpolitis
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Review Exchange Online calendar access control entries, delegate flags, special identities, and mailbox-level permissions with public PowerShell cmdlets.
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
document_id: 3b2fbb75-a3c4-8c3e-de05-1964cf64eed0
document_version_independent_id: 8497a70d-b4cf-3f14-dc08-d2dce3fae5d2
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/shared-calendars/validate-calendar-permissions.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/shared-calendars/validate-calendar-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/shared-calendars/validate-calendar-permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 770af56f-4c15-e3ac-3373-3444c82592fa
---

# Validate calendar permissions in Exchange Online | Microsoft Learn

Validate calendar folder permissions separately from mailbox-level permissions. This process helps you confirm the assigned role, identify delegate flags, and distinguish calendar access from Full Access.

## Prerequisites

Before you begin:

- Open an Exchange Online PowerShell session.
- Use an account that has permission to read mailbox and mailbox-folder permissions.
- Identify the calendar owner's primary SMTP address.
- Identify the user whose access you want to validate, if the review concerns one user.

The examples use these variables:

```powershell
$CalendarOwner = "owner@contoso.com"
$User = "user@contoso.com"
```

## Review the calendar access control list

Use [Get-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/get-mailboxfolderpermission) to return the calendar access control list:

```powershell
Get-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar" |
    Format-Table User, AccessRights, SharingPermissionFlags
```

Confirm the following values:

- `Default` is present. Its typical role is `AvailabilityOnly`.
- `Anonymous` is present. Its typical role is `None`.
- Each explicitly granted user has the intended `AccessRights`.
- A complete Outlook delegate entry has `Editor` access and includes `Delegate` in `SharingPermissionFlags`.
- `CanViewPrivateItems` appears only when the user is intended to view private calendar items.

To return one user's entry, run:

```powershell
Get-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar" -User $User
```

## Review identity details

Return additional identity properties when you need to determine whether a permission entry still maps to a directory recipient:

```powershell
$Permissions = Get-MailboxFolderPermission -Identity "${CalendarOwner}:\Calendar"

$Permissions | Select-Object `
    @{Name = "DisplayName"; Expression = { $_.User.DisplayName }},
    @{Name = "PrimarySmtpAddress"; Expression = { $_.User.RecipientPrincipal.PrimarySmtpAddress }},
    @{Name = "UserType"; Expression = { $_.User.UserType }},
    @{Name = "IsGroup"; Expression = { $_.User.RecipientPrincipal.IsGroup }},
    AccessRights,
    SharingPermissionFlags |
    Format-Table -AutoSize
```

Interpret the output as follows:

- `UserType: Internal` and `IsGroup: False` identifies a standard internal user entry.
- `UserType: External` identifies a recipient whose access is associated with external calendar sharing.
- `UserType: Unknown` or a missing recipient principal can indicate that the directory object no longer resolves.
- `IsGroup: True` identifies a group entry. Don't use a group as an Outlook delegate; assign delegate access to individual users.
- A list of individual rights instead of a named role indicates a granular permission assignment.

This validation identifies the state of the entry. Use supported permission administration or Outlook delegate configuration to make intentional changes.

## Review mailbox-level Full Access

Use [Get-MailboxPermission](/en-us/powershell/module/exchangepowershell/get-mailboxpermission) to review mailbox-level access:

```powershell
Get-MailboxPermission -Identity $CalendarOwner |
    Format-Table User, AccessRights, IsInherited, Deny
```

Look for directly assigned `FullAccess` entries that affect the user you are validating. Inherited entries for Exchange and Windows system identities are expected.

Full Access and calendar folder permissions serve different purposes. The presence or absence of Full Access doesn't replace the calendar role shown by the folder permission command.

## Record the validation result

Record these values for the reviewed user:

- Calendar owner.
- Permission identity.
- Named role or granular rights.
- `SharingPermissionFlags`.
- User type and group status.
- Direct mailbox-level Full Access, if present.

Compare the recorded values with the intended access before you make a change.