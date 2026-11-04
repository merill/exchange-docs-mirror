---
layout: Conceptual
title: Test mail flow by validating your connectors in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/test-mail-flow
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: "To validate and troubleshoot mail flow from Microsoft 365 or Office 365 to your organization's email server (also called on-premises server), validate your connectors. You can set up and validate connectors on the connectors page in the Exchange admin center (EAC). The built-in validation tests that your mail flow from Microsoft 365 or Office 365 reaches:"
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 6c8c2964-d553-4329-8166-6e508dd63fa0
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: ec98985c-8f7e-72cc-0336-79f9bf161dbd
document_version_independent_id: 6c092bac-72a5-8aec-b65b-ebb3fa5a1096
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/test-mail-flow.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/test-mail-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/test-mail-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 8d750576-e469-919b-fc60-0a7b7d0bdb4e
---

# Test mail flow by validating your connectors in Exchange Online | Microsoft Learn

To validate and troubleshoot mail flow from Microsoft 365 or Office 365 to your organization's email server (also called on-premises server), validate your connectors. You can set up and validate connectors on the **connectors** page in the Exchange admin center (EAC). The built-in validation tests that your mail flow from Microsoft 365 or Office 365 reaches:

- Your organization's email server
- A partner organization.

For more information, see [Validate connectors](use-connectors-to-configure-mail-flow/validate-connectors)

Mail flow issues can also happen when your MX record is not setup correctly. To verify your MX record, see [Find and fix issues after adding your domain or DNS records](/en-us/microsoft-365/admin/get-help-with-domains/find-and-fix-issues).

Note

These tests replace Microsoft 365 or Office 365 mail flow troubleshooting that was previously available in the [Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/o365).