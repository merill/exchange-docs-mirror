---
layout: Conceptual
title: Calendar sharing in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/calendar-share-overview
Manager: dcscontentpm
ms.subservice: sharing
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how to choose, configure, and troubleshoot calendar sharing scenarios for users, delegates, external organizations, and internet recipients.
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
ms.topic: concept-article
ms.date: 2026-10-27T00:00:00.0000000Z
locale: en-us
document_id: 0bad3ac6-51e2-2a30-1432-3d891dfb5371
document_version_independent_id: e321e706-fb3e-7bce-ce5f-6a4ca967eee9
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/calendar-share-overview.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/calendar-share-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/calendar-share-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 52f16608-2bf5-c192-a650-f3f2e6151cf3
---

# Calendar sharing in Exchange Online | Microsoft Learn

## Overview

This article helps Microsoft 365 tenant administrators identify common calendar-sharing scenarios, understand the improved shared-calendar model, and select the appropriate configuration or troubleshooting guidance.

Exchange Online supports several sharing scenarios:

- Sharing between users in the same Microsoft 365 tenant.
- Sharing between Microsoft 365 tenants.
- Sharing between Exchange Online and Exchange Server organizations.
- Publishing a calendar to recipients who do not use a trusted Exchange organization.

Tip

Start by identifying the calendar owner, the recipient, and whether their mailboxes are in the same tenant. These details determine the sharing method and expected synchronization behavior.

## Choose the sharing approach

| Scenario | Approach | Public guidance |
| --- | --- | --- |
| Users are in the same Microsoft 365 tenant | Share the calendar directly and assign the required permission level | [Calendar sharing in Microsoft 365](https://support.microsoft.com/outlook/calendar-sharing-in-microsoft-365) |
| Users are in different Microsoft 365 tenants | Use Microsoft 365 Cross-Tenant Access Policy when it is available for the tenants | [Migrate to Microsoft 365 Cross-Tenant Access Policy](/en-us/exchange/sharing/migrate-to-m365-xtap) |
| Exchange Online shares with an on-premises Exchange organization | Configure an organization relationship and the required federation | [Sharing in Exchange Online](/en-us/exchange/sharing/sharing) |
| A user shares with an external internet recipient | Configure an appropriate sharing policy | [Sharing policies in Exchange Online](/en-us/exchange/sharing/sharing-policies/sharing-policies) |

Important

An on-premises Exchange organization is external to Exchange Online, including in a hybrid deployment. Do not treat this scenario as same-tenant sharing.

Microsoft 365 Cross-Tenant Access Policy is replacing organization relationships and sharing policies for free/busy, shared-calendar, and MailTips access between Microsoft 365 tenants. The feature might not yet be available in every tenant. Check the Microsoft 365 Message center and the [migration guidance](/en-us/exchange/sharing/migrate-to-m365-xtap) before changing an existing cross-tenant configuration.

## Calendar-sharing terminology

- **Calendar owner**: The mailbox user who shares a calendar.
- **Recipient**: The user who receives and accepts a calendar-sharing invitation.
- **Sharing invitation**: The email request that invites a recipient to access a calendar.
- **Delegate**: A user who manages another user's calendar.
- **Principal**: The mailbox whose calendar a delegate manages.
- **Local copy**: The synchronized copy of the owner's calendar in the recipient's mailbox.
- **Improved shared-calendar model**: The current service-based model that synchronizes the owner's calendar to a local copy in the recipient's mailbox.
- **Legacy shared-calendar model**: The earlier model in which classic Outlook for Windows connected directly to the shared mailbox by using MAPI.
- **Meeting invitation**: A meeting request that an organizer sends to attendees. It is different from a calendar-sharing invitation.

Use **owner** and **recipient**, or **principal** and **delegate**, when describing calendar sharing. Use **organizer** and **attendee** when describing meetings.

## Check the sharing configuration

Before troubleshooting, verify the following:

1. Confirm the calendar owner and recipient.
2. Determine whether both mailboxes are in the same Microsoft 365 tenant.
3. For cross-tenant sharing, confirm that the required Cross-Tenant Access Policy or organization relationship is configured.
4. For sharing with an external internet recipient, confirm that the sharing policy allows the recipient's domain and the requested detail level.
5. Confirm that the invitation was not changed by a mail-flow rule, transport service, or mail-hygiene service. Changes to the invitation can prevent it from being accepted.
6. Confirm that the owner granted the intended calendar permission and that the recipient accepted the current invitation.

For configuration details, see [Sharing in Exchange Online](/en-us/exchange/sharing/sharing).

## Shared mailboxes and group mailboxes

A shared mailbox includes a calendar, but a shared mailbox is not the same as a calendar that one user shares with another user. Administrators assign users access to the shared mailbox. For configuration guidance, see [Shared mailboxes in Exchange Online](/en-us/exchange/collaboration-exo/shared-mailboxes).

A Microsoft 365 group also includes a group calendar. The group calendar is part of the group's shared workspace and uses a different membership and access model from user-to-user calendar sharing.

When troubleshooting, first identify whether the affected calendar belongs to a user mailbox, shared mailbox, or Microsoft 365 group. The correct access and sharing configuration depends on the mailbox type.

## Adding a calendar from the directory

In Outlook, a user can add another user's calendar from the directory:

```text
Calendar > Add calendar > Add from directory > Select an account > Add
```

Adding a calendar from the directory can display availability based on the permissions assigned to the calendar. It does not necessarily create an improved shared-calendar relationship. Availability updates can be delayed because the client refreshes the information periodically.

## Improved shared-calendar model

The improved shared-calendar model is available for calendars shared between users whose mailboxes are hosted in Exchange Online. It provides:

- Consistent sharing permissions across Outlook applications.
- A consistent invitation-acceptance experience.
- Shared calendars that synchronize across supported devices.
- Immediate synchronization for supported same-tenant scenarios.
- Better performance when users view and edit shared calendars.

For the complete support matrix and synchronization behavior, see [Calendar sharing in Microsoft 365](https://support.microsoft.com/outlook/calendar-sharing-in-microsoft-365).

### How synchronization works

In the improved model, Exchange Online synchronizes the calendar from the principal's mailbox to a local copy in the delegate's mailbox. The delegate's Outlook client synchronizes with that local copy.

In the legacy model, classic Outlook for Windows connects directly to each mailbox whose calendar it opens.

![Diagram showing classic Outlook connecting directly to the calendar owner's mailbox through MAPI.](../exchangeonline/media/sharing/legacy-shared-calendar-model.png)

![Diagram showing the service synchronizing the owner's calendar to a local copy in the recipient's mailbox.](../exchangeonline/media/sharing/improved-shared-calendar-model.png)

Changing permissions does not by itself repair a synchronization problem. Verify both the permission configuration and the shared-calendar connection.

### Requirements

The improved experience requires:

- The calendar owner's mailbox and recipient's mailbox to be hosted in Exchange Online.
- Explicit permission to the shared calendar.
- A supported Outlook client and connection mode.
- The shared calendar to use the improved model.

Shared Calendar Improvements are enabled by default in current supported versions of Microsoft 365 Apps. For classic Outlook configuration details, see [How to enable and disable Outlook calendar sharing updates](https://support.microsoft.com/outlook/how-to-enable-and-disable-the-outlook-calendar-sharing-updates).

### Identify the model in classic Outlook

In classic Outlook for Windows, open the shared calendar's folder properties. A calendar using the improved model displays **(REST)**.

![Screenshot of Calendar Properties showing the REST designation in the folder type.](../exchangeonline/media/sharing/shared-calendar-folder-properties.png)

Administrators can also manage the **REST updates for calendars** Group Policy setting for supported versions of classic Outlook.

![Screenshot of the REST updates for calendars Group Policy setting and its configuration options.](../exchangeonline/media/sharing/calendar-rest-group-policy-setting.png)

## Automatic upgrades

Eligible existing shared calendars are upgraded to the improved model in the background. The upgrade is service-managed and does not require users to re-share their calendars or accept new invitations.

After a calendar is upgraded:

- Changes can synchronize immediately in supported scenarios.
- The synchronized copy includes events from up to one year before the upgrade date by default.
- Recurring events are included when an occurrence falls within or after the one-year window.

For current upgrade behavior and user-visible changes, see [Shared calendars updates in Outlook for Windows](https://support.microsoft.com/outlook/shared-calendars-updates-in-outlook-for-windows).

Exchange Online administrators can use the `SharedCalendarSyncStartDate` parameter to control the beginning of the synchronization range. For syntax and requirements, see [Set-MailboxCalendarFolder](/en-us/powershell/module/exchangepowershell/set-mailboxcalendarfolder).

## Troubleshoot synchronization

Use this sequence before changing the Outlook profile or removing the calendar:

1. Confirm that both mailboxes are in Exchange Online.
2. Confirm that the recipient has explicit calendar permission.
3. In classic Outlook, confirm whether the folder properties show **(REST)**.
4. Check whether the issue occurs in Outlook on the web as well as the desktop client.
5. Confirm that the affected event exists in the owner's calendar in Exchange Online.
6. Review the documented behavior changes and known issues for the improved model.
7. If the problem persists, open a Microsoft support request and include the owner, recipient, approximate event time, affected Outlook clients, and the results of the preceding checks.

Do not use legacy mitigations without first checking current public guidance. For example, disabling shared-calendar improvements or changing the **Download shared folders** setting is not a general fix for a calendar that uses the improved model.

See:

- [Shared calendars updates in Outlook for Windows](https://support.microsoft.com/outlook/shared-calendars-updates-in-outlook-for-windows)
- [Known issues with classic Outlook Desktop Shared Calendar Improvements](https://support.microsoft.com/support/known-issues/known-issues-with-classic-outlook-desktop-shared-calendar-improvements)

## Expected behavior and limitations

- Same-tenant shared calendars can synchronize changes immediately when they use the improved model.
- Cross-tenant and internet calendar scenarios can have longer synchronization intervals. The interval depends on the sharing type and the recipient's calendar service.
- Events older than one year are not included in the synchronized copy by default after an upgrade, unless an administrator configures a different synchronization start date.
- Some meeting and calendar behaviors change after upgrade. Review the documented behavior changes before treating a difference as a synchronization failure.
- If a user marks a meeting as **Private**, forwarding or redirection can be restricted. See [Mark email as Normal, Personal, Private, or Confidential in Outlook](https://support.microsoft.com/office/mark-your-email-as-normal-personal-private-or-confidential-in-outlook-4a76d05b-6c29-4a0d-9096-71784a6b12c1).

## Public references

- [Calendar sharing in Microsoft 365](https://support.microsoft.com/outlook/calendar-sharing-in-microsoft-365)
- [Sharing in Exchange Online](/en-us/exchange/sharing/sharing)
- [Sharing policies in Exchange Online](/en-us/exchange/sharing/sharing-policies/sharing-policies)
- [Migrate to Microsoft 365 Cross-Tenant Access Policy](/en-us/exchange/sharing/migrate-to-m365-xtap)
- [Shared calendars updates in Outlook for Windows](https://support.microsoft.com/outlook/shared-calendars-updates-in-outlook-for-windows)
- [How to enable and disable Outlook calendar sharing updates](https://support.microsoft.com/outlook/how-to-enable-and-disable-the-outlook-calendar-sharing-updates)
- [Known issues with classic Outlook Desktop Shared Calendar Improvements](https://support.microsoft.com/support/known-issues/known-issues-with-classic-outlook-desktop-shared-calendar-improvements)

## Related calendar-sharing articles

- [Publish and subscribe to calendars](/en-us/exchange/sharing/publish-subscribe-calendars)
- [Configure and troubleshoot external calendar sharing](/en-us/exchange/sharing/configure-external-calendar-share)
- [Resolve issues with calendar sharing in classic Outlook for Windows](/en-us/troubleshoot/exchange/calendars/sharing/resolve-legacy-calendar-share-issues)
- [Resolve issues with modern calendar sharing](/en-us/troubleshoot/exchange/calendars/sharing/resolve-modern-calendar-share-issues)
- [Use Microsoft Graph for delegate access and calendar sharing](/en-us/exchange/sharing/manage-calendar-delegate-access)