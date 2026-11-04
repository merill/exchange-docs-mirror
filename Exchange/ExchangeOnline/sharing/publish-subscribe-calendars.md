---
layout: Conceptual
title: Publish and subscribe to calendars in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/publish-subscribe-calendars
Manager: dcscontentpm
ms.subservice: sharing
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how to configure anonymous calendar publishing, distribute HTML or ICS links, subscribe to published calendars, and troubleshoot access.
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
document_id: 953fe4f6-6b4a-ad61-0ac3-2f0adc816426
document_version_independent_id: 29588e6e-b781-2ec4-0cae-1ccd3cbf013a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/publish-subscribe-calendars.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/publish-subscribe-calendars
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/publish-subscribe-calendars.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 63a1dab6-9632-7596-720b-32bc6bd74dc2
---

# Publish and subscribe to calendars in Exchange Online | Microsoft Learn

Calendar publishing provides an anonymous, internet-accessible view of a calendar. A published calendar can be viewed in a browser through an HTML link or subscribed to through an ICS link. The subscribing service periodically retrieves data from the ICS endpoint.

Publishing is different from federated external sharing. Use publishing for recipients or services that do not have a federation relationship with your Exchange organization. Because anyone who has a publishing URL can access the information exposed by that URL, configure the sharing policy and published detail level carefully.

## Prerequisites and limitations

- The sharing policy assigned to the mailbox must include an `Anonymous` entry that permits calendar sharing.
- The publishing endpoint must be publicly reachable without authentication. Internal or intranet URLs are not supported for internet calendar subscriptions.
- The publishing organization controls the information exposed by the calendar. The subscribing service controls how frequently it checks for updates.
- An HTML link presents the calendar in a browser. An ICS link is intended for calendar subscriptions or a one-time ICS download.

## Configure the sharing policy

Use Exchange Online PowerShell to review the policy assigned to the mailbox and the domains configured in that policy:

```powershell
Get-Mailbox user@contoso.com | Format-List SharingPolicy
Get-SharingPolicy "Default Sharing Policy" | Format-List Domains
```

An `Anonymous` domain entry controls calendar publishing. If the policy does not contain an `Anonymous` entry that permits calendar sharing, users assigned that policy cannot publish their calendars.

For the supported values and syntax, see [Set-SharingPolicy](/en-us/powershell/module/exchangepowershell/set-sharingpolicy#-domains).

## Publish a calendar

Users can publish a calendar in Outlook on the web:

1. Open **Settings**.
2. Select **Calendar** &gt; **Shared calendars**.
3. Under **Publish a calendar**, select the calendar and the permitted detail level.
4. Select **Publish**.
5. Copy the HTML link for browser access or the ICS link for a subscription.

Administrators can also enable publishing with Exchange Online PowerShell:

```powershell
Set-MailboxCalendarFolder user@contoso.com:\Calendar -PublishEnabled $true
```

Review all available publishing settings, including the date range and detail level, in [Set-MailboxCalendarFolder](/en-us/powershell/module/exchangepowershell/set-mailboxcalendarfolder).

To inspect the current publishing configuration and URLs:

```powershell
Get-MailboxCalendarFolder user@contoso.com:\Calendar |
    Format-List PublishEnabled,PublishDateRangeFrom,PublishDateRangeTo,DetailLevel,PublishedCalendarUrl,PublishedICalUrl
```

Treat publishing URLs as sensitive. If a URL has been distributed more broadly than intended, disable publishing and publish the calendar again before distributing the new URL.

## Subscribe to a published calendar

To add an internet calendar in Outlook, use the ICS publishing URL. Outlook creates a separate, read-only calendar for the subscription. Updates depend on the polling schedule of the subscribing service and are not immediate.

An ICS file can also be imported as a one-time copy. An imported file is not a subscription and does not receive later changes from the source calendar.

For user instructions covering calendar sharing, publishing, and ICS import, see [Share an Outlook calendar as view-only with others](https://support.microsoft.com/outlook/sharing/share-an-outlook-calendar-as-view-only-with-others).

## Troubleshoot publishing

1. Confirm that the mailbox has the expected sharing policy.
2. Confirm that the policy permits anonymous calendar sharing at the intended detail level.
3. Use `Get-MailboxCalendarFolder` to confirm that publishing is enabled and that the HTML and ICS URLs are present.
4. Test the HTML URL in a private browser window. It should open without prompting for credentials.
5. Test the ICS URL in a browser. It should download an ICS file without prompting for credentials.
6. If either URL is unreachable, verify that the complete URL was copied and that the publishing endpoint is publicly accessible.

## Troubleshoot subscriptions

1. Test the ICS URL in a browser before adding it to Outlook.
2. Confirm that the endpoint does not require authentication.
3. Confirm that the downloaded content is a valid ICS file rather than an HTML error or sign-in page.
4. Remove and add the subscription again if the stored URL is incorrect.
5. Allow for the subscribing service's polling interval before determining that updates are not being retrieved.

If the source URL cannot be reached from a browser, resolve the endpoint or publishing configuration before troubleshooting the calendar client.

## Related calendar-sharing articles

- [Calendar sharing overview](/en-us/exchange/sharing/calendar-share-overview)
- [External calendar sharing](/en-us/exchange/sharing/configure-external-calendar-share)
- [Resolve issues with calendar sharing in classic Outlook for Windows](/en-us/troubleshoot/exchange/calendars/sharing/resolve-legacy-calendar-share-issues)
- [Resolve issues with modern calendar sharing](/en-us/troubleshoot/exchange/calendars/sharing/resolve-modern-calendar-share-issues)
- [Delegate access and calendar sharing via REST](/en-us/exchange/sharing/manage-calendar-delegate-access)