---
layout: Conceptual
title: Exchange ActiveSync device settings with Exchange hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/activesync-settings
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: install-set-up-deploy
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Ent_O365_Hybrid
- Strat_EX_EXOBlocker
- Hybrid
- M365-email-calendar
ms.assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
description: Exchange ActiveSync devices are automatically reconfigured when a mailbox is moved from an Exchange on-premises organization to Microsoft 365 or Office 365. Exchange ActiveSync will find the new mailbox location in Microsoft 365 or Office 365 and update its configuration to talk directly to Microsoft 365 or Office 365. The Exchange ActiveSync device won't try to contact the on-premises Exchange server after it's been successfully redirected to Microsoft 365 or Office 365. With only a few exceptions (more on that below), the user no longer needs to manually set up their device for mail to keep working.
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 64782645-c171-ec34-aa6c-0e721291c709
document_version_independent_id: 331957d6-f6c6-b11c-80d8-7c336ff13ff8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/activesync-settings.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: activesync-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/activesync-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: f563ea16-fa39-ba35-cd06-cb428ef36b9c
---

# Exchange ActiveSync device settings with Exchange hybrid deployments | Microsoft Learn

Exchange ActiveSync devices are automatically reconfigured when a mailbox is moved from an Exchange on-premises organization to Microsoft 365 or Office 365. Exchange ActiveSync will find the new mailbox location in Microsoft 365 or Office 365 and update its configuration to talk directly to Microsoft 365 or Office 365. The Exchange ActiveSync device won't try to contact the on-premises Exchange server after it's been successfully redirected to Microsoft 365 or Office 365. With only a few exceptions (more on that below), the user no longer needs to manually set up their device for mail to keep working.

If you want to move a mailbox to Microsoft 365 or Office 365, see [Move mailboxes between on-premises and Exchange Online organizations in hybrid deployments](hybrid-deployment/move-mailboxes).

For more information about hybrid deployments, see [Exchange Server Hybrid Deployments](exchange-hybrid).

To use automatic redirection, your on-premises servers need to be running the latest releases of Exchange 2010, Exchange 2013, Exchange 2016, or later. You also need to have used the [Hybrid Configuration wizard](hybrid-configuration-wizard) to set up your hybrid deployment. The Exchange ActiveSync redirection functionality uses the Outlook on the web target URL that's set on the organization relationship object. This object is configured when the Hybrid Configuration wizard is run.

If your organization meets the requirements listed above, mobile devices should automatically be redirected to Microsoft 365 or Office 365 when a user's mailbox is moved, without any additional configuration. For the best experience, make sure your users' mobile devices are running the latest versions of their operating systems and e-mail clients. Some mobile devices, such as those running the Android operating system, might take longer than expected to be redirected. Additionally, some devices might not correctly interpret the Exchange ActiveSync 451 redirection instructions sent by Exchange. For these devices, users will still need to manually reconfigure or recreate their email account on the device. If you have questions about whether a device supports Exchange ActiveSync 451 redirection, contact the device manufacturer.

Automatic Exchange ActiveSync redirection isn't supported in the following scenarios:

- Moving mailboxes from Microsoft 365 or Office 365 to an on-premises Exchange organization.
- Moving mailboxes between on-premises Exchange organizations.
- Moving mailboxes from Exchange 2007 servers to Microsoft 365 or Office 365.