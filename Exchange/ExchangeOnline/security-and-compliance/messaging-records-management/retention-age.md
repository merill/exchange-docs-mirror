---
layout: Conceptual
title: How retention age is calculated in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/messaging-records-management/retention-age
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
description: Admins can learn how the Managed Folder Assistant (MFA) processes items in user mailboxes in Exchange Online.
ms.topic: article
author: k-reagle
ms.author: kreagle
ms.assetid: a7daf7aa-0411-4b26-a422-eefd1b113f9f
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-06-26T00:00:00.0000000Z
locale: en-us
document_id: a659b815-705f-fa0f-9867-db506cc2c474
document_version_independent_id: d85dba9c-c8d1-7d31-2af3-1a26a13c713f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/retention-age.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/messaging-records-management/retention-age
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/retention-age.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: 4c8aa9cd-1195-a984-a756-d67368978c4f
---

# How retention age is calculated in Exchange Online | Microsoft Learn

Note

To proactively retain or delete mailbox content for information governance in Microsoft 365, we recommend that you use [retention policies and retention labels](/en-us/purview/retention) from the [Microsoft Purview portal](https://purview.microsoft.com/), instead of messaging records management that's described on this page. However, you should continue using messaging records management to move messages to archive mailboxes.

If you currently use messaging records management, this older feature will continue to work side-by-side with retention policies and retention labels. However, we recommend that going forward, you use retention policies and retention labels instead. They provide you with a single mechanism to centrally manage both retention and deletion of content across Microsoft 365.

The Managed Folder Assistant (MFA) is one of many mailbox assistant processes that runs in Exchange Online. Its job is to process mailboxes that have a Retention Policy applied, add the Retention Tags included in the policy to the mailbox, and process items in the mailbox. If the items have a retention tag, the assistant tests the age of those items. If an item has exceeded its retention age, it takes the specified retention action. Retention actions include moving an item to the user's archive, deleting the item and allowing recovery, or deleting the item permanently.

See [Retention tags and retention policies](retention-tags-and-policies) for more information.

## Determining the age of different types of items

The retention age of mailbox items is calculated from the date of delivery or in the case of items like drafts that aren't delivered but created by the user, the date an item was created. When the Managed Folder Assistant processes items in a mailbox, it stamps a start date and an expiration date for all items that have retention tags with the **Delete and Allow Recovery** or **Permanently Delete** retention action. Items that have an archive tag are also stamped with a move date.

Items in the Deleted Items folder and items which may have a start and end date, such as calendar items (meetings and appointments) and tasks, are handled differently as shown in this table.

| If the item type is... | And the item is... | The retention age is calculated based on... |
| --- | --- | --- |
| Email message <br> Document <br><br> Fax <br><br> Journal item <br><br> Meeting request, response, or cancellation <br><br> Missed call <br><br> Notes | Not in the Deleted Items folder | Delivery date or date of creation |
| Email message <br> Document <br><br> Fax <br><br> Journal item <br><br> Meeting request, response, or cancellation <br><br> Missed call <br><br> Notes | In the Deleted Items folder | Date of delivery or creation unless the item was deleted from a folder that doesn't have an inherited or implicit retention tag. <br> If an item is in a folder that doesn't have an inherited or implicit retention tag applied, the item isn't processed by the MFA and therefore doesn't have a start date stamped by it. When the user deletes such an item, and the MFA processes it for the first time in the Deleted Items folder, it stamps the current date as the start date. |
| Calendar | Not in the Deleted Items folder | Nonrecurring calendar items expire according to their end date. <br> Recurring calendar items expire according to the end date of their last occurrence. Recurring calendar items with no end date don't expire. |
| Calendar | In the Deleted Items folder | A calendar item expires according to its message-received date, if one exists. If a calendar item doesn't have a message-received date, it expires according to its message-creation date. If a calendar item has neither a message-received date nor a message-creation date, it doesn't expire. |
| Task | Not in the Deleted Items folder | Nonrecurring tasks: <br> A nonrecurring task expires according to its `message-received date`, if one exists. <br><br> If a nonrecurring task doesn't have a `message-received date`, it expires according to its `message-creation date`. <br><br> If a nonrecurring task has neither a `message-received date` nor a `message-creation date`, it doesn't expire. <br><br> A recurring task expires according to the `end date` of its last occurrence. If a recurring task doesn't have an `end date`, it doesn't expire. <br><br> A regenerating task (which is a recurring task that regenerates a specified time after the preceding instance of the task is completed) doesn't expire. |
| Task | In the Deleted Items folder | A task expires according to its message-received date, if one exists. If a task doesn't have a message-received date, it expires according to its message-creation date. A task without a message-received or message-creation date does not expire. |
| Contact | In any folder | Contacts aren't stamped with a start date or an expiration date, so they're skipped by the Managed Folder Assistant and don't expire. |
| Corrupted | In any folder | Corrupted items are skipped by the Managed Folder Assistant and don't expire. |

## Examples

| If the user... | The retention tags on folder... | The Managed Folder Assistant... |
| --- | --- | --- |
| Receives a message in the Inbox on 01/26/2019. Deletes the message on 2/27/2019. | Inbox: Delete in 365 days <br> Deleted Items: Delete in 30 days | Processes the message in the Inbox on 1/26/2019; stamps it with a start date of 01/26/2019 and an expiration date of 01/26/2020. <br> Processes the message again in the Deleted Items folder on 2/27/2019. It recalculates the expiration date based on the same start date (01/26/2019). Because the item is older than 30 days, it's expired immediately. |
| Receives a message in the Inbox on 01/26/2019. Deletes the message on 2/27/2019. | Inbox: None (inherited or implicit) <br> Deleted Items: Delete in 30 days | Processes the message in the Deleted Items folder on 02/27/2019 and determines the item doesn't have a start date. <br> It stamps the current date as the start date, and 03/27/2019 as the expiration date. The item is expired on 3/27/2019, which is 30 days after the user deleted or moved it to the Deleted Items folder. |

## More Information

- In Exchange Online, the Managed Folder Assistant processes a mailbox once in seven days. This might result in items being expired up to seven days after the expiration date stamped on the item.
- Items in mailboxes placed on Retention Hold aren't processed by the Managed Folder Assistant until the Retention Hold is removed.
- If a mailbox is placed on In-Place Hold or Litigation Hold, expiring items are removed from the Inbox but preserved in the Recoverable Items folder until the mailbox is removed from [In-Place Hold and Litigation Hold](../in-place-and-litigation-holds).
- In hybrid deployments, the same retention tags and retention policies must exist in your on-premises and Exchange Online organizations in order to consistently move and expire items across both organizations. See [Export and Import Retention Tags](../../export-and-import-retention-tags-exchange-2013-help) for more information.