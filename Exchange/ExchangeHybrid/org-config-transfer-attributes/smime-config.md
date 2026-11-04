---
layout: Conceptual
title: Smime Config attributes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/org-config-transfer-attributes/smime-config
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
ms.topic: reference
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
description: The available S/MIME Config attributes that are copied by the Hybrid Configuration wizard from your on-premises organization to Exchange Online.
ms.date: 2019-07-08T00:00:00.0000000Z
locale: en-us
document_id: f8e02d2f-4236-5d00-3d60-7336ebeedf3b
document_version_independent_id: 03f0df92-8abe-d119-af42-c6afe7a7fc81
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/org-config-transfer-attributes/smime-config.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: org-config-transfer-attributes/smime-config
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/org-config-transfer-attributes/smime-config.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: e40c3ada-4a87-7814-a81d-0c1825144d2e
---

# Smime Config attributes | Microsoft Learn

As soon as you select **Organization Configuration Transfer** in the Hybrid Configuration wizard, the following S/MIME Config attributes are copied from the on-premises Exchange organization to Exchange Online:

| SMIMEConfig | Available In |
| --- | --- |
| Identity | Exchange 2010, 2013, 2016, 2019 |
| Name | Exchange 2010, 2013, 2016, 2019 |
| OWACheckCRLOnSend | Exchange 2010, 2013, 2016, 2019 |
| OWADLExpansionTimeout | Exchange 2010, 2013, 2016, 2019 |
| OWAUseSecondaryProxiesWhenFindingCertificates | Exchange 2010, 2013, 2016, 2019 |
| OWACRLConnectionTimeout | Exchange 2010, 2013, 2016, 2019 |
| OWACRLRetrievalTimeout | Exchange 2010, 2013, 2016, 2019 |
| OWADisableCRLCheck | Exchange 2010, 2013, 2016, 2019 |
| OWAAlwaysSign | Exchange 2010, 2013, 2016, 2019 |
| OWAAlwaysEncrypt | Exchange 2010, 2013, 2016, 2019 |
| OWAClearSign | Exchange 2010, 2013, 2016, 2019 |
| OWAIncludeCertificateChainWithoutRootCertificate | Exchange 2010, 2013, 2016, 2019 |
| OWAIncludeCertificateChainAndRootCertificate | Exchange 2010, 2013, 2016, 2019 |
| OWAEncryptTemporaryBuffers | Exchange 2010, 2013, 2016, 2019 |
| OWASignedEmailCertificateInclusion | Exchange 2010, 2013, 2016, 2019 |
| OWABCCEncryptedEmailForking | Exchange 2010, 2013, 2016, 2019 |
| OWAIncludeSMIMECapabilitiesInMessage | Exchange 2010, 2013, 2016, 2019 |
| OWACopyRecipientHeaders | Exchange 2010, 2013, 2016, 2019 |
| OWAOnlyUseSmartCard | Exchange 2010, 2013, 2016, 2019 |
| OWATripleWrapSignedEncryptedMail | Exchange 2010, 2013, 2016, 2019 |
| OWAUseKeyIdentifier | Exchange 2010, 2013, 2016, 2019 |
| OWAEncryptionAlgorithms | Exchange 2010, 2013, 2016, 2019 |
| OWASigningAlgorithms | Exchange 2010, 2013, 2016, 2019 |
| OWAForceSMIMEClientUpgrade | Exchange 2010, 2013, 2016, 2019 |
| OWASenderCertificateAttributesToDisplay | Exchange 2010, 2013, 2016, 2019 |
| OWAAllowUserChoiceOfSigningCertificate | Exchange 2010, 2013, 2016, 2019 |