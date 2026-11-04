---
layout: Conceptual
title: Default Retention Policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/messaging-records-management/default-retention-policy
Manager: laurawi
ms.subservice: exo-security-compliance
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn how the Default MRM Policy in Exchange Online and on-premises Exchange works, how to manage retention for users, and best practices for compliance.
customer-intent: As an admin, I want to understand and manage the Default MRM Policy so that I can meet my organization's retention and compliance needs.
ms.topic: overview
author: k-reagle
ms.author: kreagle
ms.assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: Admin
search.appverid: MET150
ms.service: exchange-online
ms.custom: msecd-doc-authoring-1012
ai-usage: ai-assisted
ms.date: 2026-05-29T00:00:00.0000000Z
locale: en-us
document_id: f5be8284-bc52-a254-97eb-ef44b3cb002a
document_version_independent_id: 25c499c9-c274-933d-6c56-ae126c32079e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/default-retention-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/messaging-records-management/default-retention-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/default-retention-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 582d2ce7-870d-0e43-9ba0-0404f583b1fd
---

# Default Retention Policy in Exchange Online | Microsoft Learn

Important

Refer to the [Microsoft 365 security center](https://security.microsoft.com/homepage) and the [Microsoft Purview portal](https://purview.microsoft.com/) for Exchange security and compliance features. They're no longer available in the new [Exchange admin center](https://admin.exchange.microsoft.com).

Note

To proactively retain or delete mailbox content for information governance in Microsoft 365, we recommend that you use [retention policies and retention labels](/en-us/purview/retention) from the [Microsoft Purview portal](/en-us/purview/purview-portal), instead of messaging records management that's described on this page. However, you should continue using messaging records management to move messages to archive mailboxes.

If you currently use messaging records management, this older feature continues to work side-by-side with retention policies and retention labels. However, we recommend that going forward, you use retention policies and retention labels instead. They provide you with a single mechanism to centrally manage both retention and deletion of content across Microsoft 365.

Exchange creates the retention policy Default MRM Policy in your Exchange Online and on-premises Exchange organization. The policy is automatically applied to new users in Exchange Online. In on-premises organizations, the policy is applied when you create an archive for the mailbox. You can change the retention policy applied to a user at any time.

You can modify tags that are included in the Default MRM Policy. For example, you can change the retention age or retention actions, disable a tag, or modify the policy by adding or removing tags from it. The updated policy is applied to mailboxes the next time the Managed Folder Assistant processes them.

Note

The Default MRM Policy doesn't include a default tag to automatically delete content from the Deleted items folder as per [Extended email retention for deleted items in Office 365](https://www.microsoft.com/microsoft-365/blog/2015/02/20/extended-email-retention-deleted-items-office-365/). If you want to apply the 30-day retention or set a custom retention period, add an appropriate retention tag for deleted items folder to the Default MRM Policy.

## Retention tags linked to the Default MRM Policy

The following table lists the default retention tags linked to the Default MRM Policy.

| Name | Type | Retention age (days) | Retention action |
| --- | --- | --- | --- |
| Default 2 years move to archive | Default Policy Tag (DPT) | 730 | Move to Archive |
| Recoverable Items 14 days move to archive | Recoverable Items folder | 14 | Move to Archive |
| Personal 1 year move to archive | Personal tag | 365 | Move to Archive |
| Personal 5 year move to archive | Personal tag | 1,825 | Move to Archive |
| Personal never move to archive | Personal tag | Not applicable | Move to Archive |
| 1 Week Delete | Personal tag | 7 | Delete and Allow Recovery |
| 1 Month Delete | Personal tag | 30 | Delete and Allow Recovery |
| 6 Months Delete | Personal tag | 180 | Delete and Allow Recovery |
| 1 Year Delete | Personal tag | 365 | Delete and Allow Recovery |
| 5 Years Delete | Personal tag | 1,825 | Delete and Allow Recovery |
| Never Delete | Personal tag | Not applicable | Delete and Allow Recovery |
| Junk Email | Retention policy tag (RPT) | 30 | Delete and Allow Recovery |

## What you can do with the Default MRM Policy

| You can... | In Exchange Online... | In Exchange Server... |
| --- | --- | --- |
| Apply the Default MRM Policy automatically to new users | Yes, applied by default. No action is required. | Yes, applied by default if you also create an archive for the new user. <br> If you create an archive for the user later, the policy is applied automatically only if the user doesn't have an existing Retention Policy. |
| Modify the retention age or retention action of a retention tag linked to the policy | Yes | Yes |
| Disable a retention tag linked to the policy | Yes | Yes |
| Add a retention tag to the policy | Yes | Yes |
| Remove a retention tag from the policy | Yes | Yes |
| Set another policy as the default retention policy to be applied automatically to new users | No | No |

## Additional retention policy details

- A Retention Tag can be linked to more than one Retention Policy. For more information about managing [Retention tags and retention policies](retention-tags-and-policies), see the Microsoft Learn article about [inactive mailboxes in Office 365](/en-us/purview/inactive-mailboxes-in-office-365).
- The Default MRM Policy doesn't include a DPT to automatically delete items (but it does contain personal tags with the deleted retention action that users can apply to mailbox items). If you want to automatically delete items after a specified period, you can create a DPT with the required delete action and add it to the policy. For details, see [Create a Retention Policy](create-a-retention-policy) and [Add retention tags to or remove retention tags from a retention policy](add-or-remove-retention-tags).
- Retention policies are applied to mailbox users. The same policy applies to the user's mailbox and archive.