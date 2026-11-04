---
layout: Conceptual
title: Auto-archiving in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/messaging-records-management/auto-archiving
Manager: laurawi
ms.subservice: purview-data-lifecycle-management
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
author: k-reagle
ms.author: kreagle
ms.reviewer: lusassl-msft
ms.service: purview
ms.topic: overview
ms.date: 2026-06-26T00:00:00.0000000Z
description: Auto-archiving in Exchange Online automatically moves oldest mailbox items to archive when usage exceeds 96% of quota.
locale: en-us
document_id: 960e320f-d3f1-977e-cfea-3054a97fb944
document_version_independent_id: 1407fd7a-b79c-dc66-d109-a234d0f4e9c7
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/auto-archiving.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/messaging-records-management/auto-archiving
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/auto-archiving.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: e0febc8b-7d3b-4298-8121-a77b8c6da0b0
---

# Auto-archiving in Exchange Online | Microsoft Learn

Auto-archiving is a new feature for Exchange Online that enters public preview in November 2025. Currently in private preview for selected customers, this feature is designed to prevent disruptions in mail flow when a user's mailbox exceeds 96% of its quota. Auto-archiving automatically moves the oldest items, excluding those items tagged with "Never Move to Archive" from the primary mailbox to the archive mailbox, keeping mailbox usage below the safe threshold of 96%.

## Use cases

- Preventing mail flow disruptions due to full mailbox quotas.
- Automatically managing mailbox size to maintain operational efficiency.

## Auto-archiving description

Auto-archiving introduces threshold-based archiving that complements existing time-based archiving policies. When mailbox utilization exceeds 96% of its quota, items are automatically moved to the archive mailbox until usage drops below the threshold. This feature ensures real-time monitoring and management of mailbox health.

Note

This feature is called Auto-Archiving, which is different from [Auto expanding Archive](/en-us/purview/autoexpanding-archiving).

### Requirements

- The archive mailbox must be provisioned for the user.
- The archive mailbox must have remaining storage capacity.
- Exchange Online user must be enabled, unless RecipientTypeDetails is SharedMailbox.

### Considerations

- Items tagged with "Never Move to Archive" are excluded from auto-archiving.
- Auto-archiving temporarily overrides existing archiving policies when triggered.
- The feature doesn't change deletion or retention policies.
- Auto-archiving can't be disabled at the organization level, however autoarchive threshold can be configured for organization.
- Auto-archiving can be enabled/disabled per mailbox.

### How it works:

- The Managed Folder Assistant continuously monitors the primary mailbox size. As and when primary mailbox size exceeds 96% of the current mailbox quota and provided the archive mailbox is provisioned and has remaining space, Managed Folder Assistant automatically archives the **oldest** items first until usage drops below the threshold. The same concept applies to Recoverable Items ("Dumpster") folders when they near their quota.
- Auto-Archiving attempts to move 3% of data in each run until mailbox size is below the threshold. Percentage is calculated based on ProhibitSendReceiveQuota/RecoverableItemsQuota. So, if ProhibitSendReceiveQuota/RecoverableItemsQuota is 100 GB, then auto-archiving attempts to move 3 GB in a single run.
- Auto-Archiving doesn't archive data received less than 60 days ago.

Note

Oldest items under **Top of Information Store** are archived based on received date.

#### Enable auto-archiving for specific users

Auto-archiving feature can be enabled or disabled at mailbox level (the default setting is enabled):

Example how to disable auto-archiving feature for a user:

```powershell
Set-Mailbox <user mailbox> -AutoArchivingEnabled $false
```

#### Configure auto-archiving threshold for organization

To adjust the threshold setting at the organization level, use (example changing AutoArchivingThresholdPercentage from 96 to 90):

```powershell
Set-OrganizationConfig –AutoArchivingThresholdPercentage 90
```

**Default Value:** 96 **Valid Range:** 80–100

Note

Setting the threshold to **100 disables auto-archiving for the tenant**.

#### Diagnostics available for auto-archiving feature

Administrators can access detailed diagnostics using the Exchange Online shell for individual mailbox:

```powershell
Export-MailboxDiagnosticLogs -Identity <user mailbox> -ComponentName MRM
```

```plaintext
[Sample MailboxLog]:
<Date>;
method: PublishDiagnosticsLog; ...
Auto-Archiving completed for mailbox: <MbxGuid>.
Items archived till date: <Date>.
Total items archived: <ItemCount>,
Total bytes archived: <Size>.
Auto-Archiving was triggered to move <xyz GB> of data because mailbox utilization crossed 96%.
```

### Examples

For example, when a user’s mailbox reaches 96% utilization and has an archive mailbox with available space, the Managed Folder Assistant (MFA) automatically moves the oldest items, based on their received date, from the primary mailbox to the archive mailbox. This feature ensures uninterrupted mail flow and prevents storage-related disruptions.

## Availability

- Available on the [Microsoft Roadmap](https://www.microsoft.com/microsoft-365/roadmap?id=515172).

## Pricing

- Same licenses requirements for time-based archiving [Microsoft 365 licensing guidance for security & compliance.](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance#licenses-for-email-archiving)

## Limitations

- Auto-archiving feature doesn't provision archive mailboxes. Exchange Online Administrators must enable these archives manually.
- If the main archive mailbox is full and auto-expanding archive isn't enabled, auto-archiving isn't moving items.

## FAQs

**❓When does auto-archiving get triggered?**
Auto-archiving is triggered when a user's primary mailbox exceeds 96% utilization and the archive mailbox is provisioned with available storage. More specifically, values of ProhibitSendReceiveQuota (for visible mailbox items) and RecoverableItemsQuota (for items in Recoverable Items folders) are evaluated. But both are applied independently. Suppose that the user's RecoverableItem size is greater than 96%, older items from RecoverableItems get archived. And similarly, if visible items size is greater than 96%, older items from user's visible mailbox folders get archived. 

**❓Are items with the "Never Move to Archive" tag affected?**
No, items or folders tagged with "Never Move to Archive" are excluded from auto-archiving. 

**❓Which item classes are supported for auto-archiving?**
All item classes are supported except "IPM.Appointment," "IPM.AppointmentSeries," "IPM.Task," "IPM.Contact," "IPM.DistList," "IPM.File," and "IPM.File.Document." 

**❓Do users notice changes?**
If auto-archiving is triggered, the oldest items are being moved to the "Online Archive" tree while preserving the folder structure, ensuring mail remains accessible and searchable. 

**❓Does auto-archiving provision archive mailboxes?**
No, archive mailboxes must be provisioned manually. 

**❓Does auto-archiving enable auto-expanding archives?**
No, auto-expanding archives must be enabled manually to ensure no disruptions when the main archive is full. 

**❓Does auto-archiving require a default archiving policy?**
No, emails can be automatically archived without a default archiving policy if the archive mailbox is provisioned. 

**❓Does auto-archiving change retention policies?**
No, auto-archiving relocates items to the archive to prevent primary mailbox quota lockouts but doesn't change deletion or retention behaviors. 

**❓Does auto-archiving trigger for mailboxes under retention hold?**
Yes, auto-archiving process mailboxes under retention hold to prevent mail flow disruptions while preserving compliance. 

**❓How can specific information be prevented from being archived?**
Prevent specific information from being archived by applying "Never Move to Archive" tag.