---
layout: Conceptual
title: Organization Config | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/org-config-transfer-attributes/organization-config
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
ms.reviewer: dstrome
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: article
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
description: The available Organization configuration transfer attributes that are copied by the Hybrid Configuration wizard from your on-premises organization to Exchange Online.
ms.date: 2018-10-10T00:00:00.0000000Z
locale: en-us
document_id: a1ee00fa-22c2-5d93-4e2d-74c8c4575815
document_version_independent_id: 06af1d7f-c2db-ad54-9b2d-fe6f416ba0fa
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/org-config-transfer-attributes/organization-config.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: org-config-transfer-attributes/organization-config
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/org-config-transfer-attributes/organization-config.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: d14d8fdc-8e98-ef6f-9ce3-a7d914c619da
---

# Organization Config | Microsoft Learn

The following attributes of Organization Config are copied from an on-premises Exchange organization to Exchange Online when the **Organization Configuration Transfer** option is selected in the Hybrid Configuration wizard.

| OrganizationConfig | Available In |
| --- | --- |
| ActivityBasedAuthenticationTimeoutEnabled | Exchange 2010, 2013, 2016, 2019 |
| ActivityBasedAuthenticationTimeoutInterval | Exchange 2010, 2013, 2016, 2019 |
| ActivityBasedAuthenticationTimeoutWithSingleSignOnEnabled | Exchange 2010, 2013, 2016, 2019 |
| AppsForOfficeEnabled | Exchange 2013, 2016, 2019 |
| AsyncSendEnabled | Exchange 2016, 2019 |
| BookingsEnabled | Exchange 2016, 2019 |
| ByteEncoderTypeFor7BitCharsets | Exchange 2010, 2013, 2016, 2019 |
| ConnectorsActionableMessagesEnabled | Exchange 2016, 2019 |
| ConnectorsEnabled | Exchange 2016, 2019 |
| DefaultPublicFolderAgeLimit | Exchange 2013, 2016, 2019 |
| DefaultPublicFolderDeletedItemRetention | Exchange 2013, 2016, 2019 |
| DefaultPublicFolderIssueWarningQuota | Exchange 2013, 2016, 2019 |
| DefaultPublicFolderMaxItemSize | Exchange 2013, 2016, 2019 |
| DefaultPublicFolderMovedItemRetention | Exchange 2013, 2016, 2019 |
| DefaultPublicFolderProhibitPostQuota | Exchange 2013, 2016, 2019 |
| DirectReportsGroupAutoCreationEnabled | Exchange 2016, 2019 |
| DistributionGroupDefaultOU | Exchange 2010, 2013, 2016, 2019 |
| DistributionGroupNameBlockedWordsList | Exchange 2010, 2013, 2016, 2019 |
| DistributionGroupNamingPolicy | Exchange 2010, 2013, 2016, 2019 |
| ElcProcessingDisabled | Exchange 2016, 2019 |
| EndUserDLUpgradeFlowsDisabled | Exchange 2016, 2019 |
| EwsAllowEntourage | Exchange 2010, 2013, 2016, 2019 |
| EwsAllowList | Exchange 2010, 2013, 2016, 2019 |
| EwsAllowMacOutlook | Exchange 2010, 2013, 2016, 2019 |
| EwsAllowOutlook | Exchange 2010, 2013, 2016, 2019 |
| EwsApplicationAccessPolicy | Exchange 2010, 2013, 2016, 2019 |
| EwsBlockList | Exchange 2010, 2013, 2016, 2019 |
| EwsEnabled | Exchange 2010, 2013, 2016, 2019 |
| ExchangeNotificationEnabled | Exchange 2010, 2013, 2016, 2019 |
| ExchangeNotificationRecipients | Exchange 2010, 2013, 2016, 2019 |
| FocusedInboxOn | Exchange 2016, 2019 |
| HierarchicalAddressBookRoot | Exchange 2010, 2013, 2016, 2019 |
| IPListBlocked | Exchange 2016, 2019 |
| IsAgendaMailEnabled | Exchange 2016, 2019 |
| LeanPopoutEnabled | Exchange 2016, 2019 |
| LinkPreviewEnabled | Exchange 2016, 2019 |
| MailTipsAllTipsEnabled | Exchange 2010, 2013, 2016, 2019 |
| MailTipsExternalRecipientsTipsEnabled | Exchange 2010, 2013, 2016, 2019 |
| MailTipsGroupMetricsEnabled | Exchange 2010, 2013, 2016, 2019 |
| MailTipsLargeAudienceThreshold | Exchange 2010, 2013, 2016, 2019 |
| MailTipsMailboxSourcedTipsEnabled | Exchange 2010, 2013, 2016, 2019 |
| OAuth2ClientProfileEnabled | Exchange 2013, 2016, 2019 |
| PerTenantSwitchToESTSEnabled | Exchange 2016, 2019 |
| PreferredInternetCodePageForShiftJis | Exchange 2010, 2013, 2016, 2019 |
| PublicComputersDetectionEnabled | Exchange 2013, 2016, 2019 |
| PublicFoldersEnabled | Exchange 2013, 2016, 2019 |
| ReadTrackingEnabled | Exchange 2010, 2013, 2016, 2019 |
| RefreshSessionEnabled | Exchange 2016, 2019 |
| RemotePublicFolderMailboxes | Exchange 2013, 2016, 2019 |
| RequiredCharsetCoverage | Exchange 2010, 2013, 2016, 2019 |
| SiteMailboxCreationURL | Exchange 2013, 2016, 2019 |
| SmtpActionableMessagesEnabled | Exchange 2016, 2019 |
| UnblockUnsafeSenderPromptEnabled | Exchange 2016, 2019 |