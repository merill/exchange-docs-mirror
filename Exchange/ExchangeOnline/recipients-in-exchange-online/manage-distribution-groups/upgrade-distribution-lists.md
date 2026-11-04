---
layout: Conceptual
title: Upgrade Distribution Lists to Microsoft 365 Groups | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/upgrade-distribution-lists
Manager: serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Use the Exchange admin center (EAC) to upgrade Distribution Lists to Microsoft 365 Groups.
ms.topic: upgrade-and-migration-article
author: Benny-54
ms.author: serdars
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2023-07-05T00:00:00.0000000Z
locale: en-us
document_id: eb77f7ee-9ab6-1621-86d5-981c8e8876b7
document_version_independent_id: 9f037852-8a7c-ff9b-6613-25026324cde4
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/upgrade-distribution-lists.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-distribution-groups/upgrade-distribution-lists
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/upgrade-distribution-lists.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: b0939b85-4e5f-a08f-0cf6-744a03c74e56
---

# Upgrade Distribution Lists to Microsoft 365 Groups | Microsoft Learn

Tenant admins can upgrade Distribution Groups (also referred to as Distribution Lists or DL) to Microsoft 365 Groups, provided the DL matches certain conditions. In the new workflow, tenant admin can select the desired DL in Exchange admin center (EAC) and send upgrade request to DL owners. DL owner can then decide whether or not to upgrade the DL to Microsoft 365 Group. After successful conversion, the Microsoft 365 Group will have all the members of DL along with email addresses stamped on the DL.

Note

DL owners cannot directly upgrade DL to Microsoft 365 Group; the process can be initiated only by admins.

## Prerequisites

The admin must have:

1. Exchange Administrator roles assigned.
2. A mailbox.

The Distribution Group being upgraded must be eligible for upgrade. You can run the following PowerShell command to view Distribution Groups eligible for upgrade:`Get-EligibleDistributionGroupForMigration`.

## Convert an existing Distribution List to a Microsoft 365 Group

Admins can select the Distribution List and trigger an email to the owner(s) of the eligible Distribution List from the Exchange admin center. Owners of the eligible Distribution List can upgrade it to a Microsoft 365 Group by selecting it in the email. It takes a maximum of 5 to 10 minutes for the upgrade to complete. Both owners and admins can see the upgraded Distribution List in the Microsoft 365 Groups section once the upgrade is done.

To convert an existing Distribution List to a Microsoft 365 Group, do the following:

1. In the **Exchange Admin Center**, go to **Recipients** &gt; **Group** &gt; **Distribution List** and select the specific Distribution List. Admins can now see the new option "**Send upgrade request**". The email isn't sent at this stage.

    [![screenshot-of-how-to-select-the-distribution-list.](../../exchangeonline/media/select-recipients.png)](../../exchangeonline/media/select-recipients.png#lightbox)
2. If the Distribution List is eligible for an upgrade, select the owners to send this email. You can either choose all the owners or specific owners to send this email.

    [![screenshot-of-how-to-send-request-to-owner.](../../exchangeonline/media/send-request.png)](../../exchangeonline/media/send-request.png#lightbox)
3. Select **Send Request**.

    [![screenshot-of-how-to-upgrade-the-sent-request.](../../exchangeonline/media/request-sent-successfully.png)](../../exchangeonline/media/request-sent-successfully.png#lightbox)

Note

You can upgrade only cloud-managed, simple, non-nested Distribution Lists to Microsoft 365 groups. For more information, check this article: [You can't upgrade distribution lists to Microsoft 365 groups.](/en-us/exchange/troubleshoot/groups-and-distribution-lists/cannot-upgrade-distribution-lists-to-office-365-groups)

If the Distribution List isn't eligible for an upgrade. You get the following error message for such Distribution Lists.

[![screenshot-of-error-message-for-ineligible-distribution-list.](../../exchangeonline/media/error-message-dl.png)](../../exchangeonline/media/error-message-dl.png#lightbox)

The end user gets the email. And once the user selects the **Upgrade** in the email, the Distribution List gets converted to a Microsoft 365 Group.

[![screenshot-of-how-to-upgrade-request-in-email.](../../exchangeonline/media/upgrade-email.png)](../../exchangeonline/media/upgrade-email.png#lightbox)

[![screenshot-of-how-to-upgrade-the-initiated-process.](../../exchangeonline/media/upgraded-successfully.png)](../../exchangeonline/media/upgraded-successfully.png#lightbox)

Note

The email address of the Distribution List will not change when users upgrade.