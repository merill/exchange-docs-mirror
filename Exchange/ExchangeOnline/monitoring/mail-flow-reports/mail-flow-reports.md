---
layout: Conceptual
title: Mail flow reports in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mail-flow-reports
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: serdars
author: serdars
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
description: Admins can learn about the mail flow reports that are available in the new Exchange admin center.
ms.custom: 
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: 17d04b61-f141-9dba-598d-cb341873d2c7
document_version_independent_id: 69dc98b5-9d48-48a7-c7c9-ed0cbe0586bd
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mail-flow-reports.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mail-flow-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mail-flow-reports.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 62423583-c1b8-0a4d-e6cc-d5b511af6db2
---

# Mail flow reports in the new EAC in Exchange Online | Microsoft Learn

Administrators can use mail flow reports in the new Exchange admin center (new EAC) to establish baselines and discover trends to fix issues related to mail flow in their organization.

Note

Mail flow reports are currently not available in the GCC High or DoD environments.

The following mail flow reports are available:

- [Auto forwarded messages report](mfr-auto-forwarded-messages-report)
- [Email issues for priority accounts report](mfr-email-issues-for-priority-accounts-report)
- [Exchange transport rule report](mfr-exchange-transport-rule-report)
- [Inbound messages report](mfr-inbound-messages-and-outbound-messages-reports)
- [Non-accepted domain report](mfr-non-accepted-domain-report)
- [Non-delivery details report](mfr-non-delivery-details-report)
- [Outbound messages report](mfr-inbound-messages-and-outbound-messages-reports)
- [Queued messages report](mfr-queued-messages-report)
- [SMTP AUTH clients report](mfr-smtp-auth-clients-report)
- [Top domain mail flow status report](mfr-top-domain-mailflow-status-report)
- [Mailboxes exceeding receiving limits report](mailboxes-exceeding-receiving-limits-report)
- [Dynamic Distribution Groups report](mfr-dynamic-distribution-groups-report)
- [Reply-all storm protection report](reply-all-storm-protection-report)
- [Outbound messages in Transit Security report](outbound-messages-in-transit-security-report)

## Permissions required to view mail flow reports

To view and use mail flow reports, you need to be a member of one of the following role groups in Exchange Online:

- Compliance Administrator
- Exchange Administrator
- Organization Management
- Security Administrator&lt;sup&gt;\*
- Security Reader^\*^
- View-Only Recipients

For more information, see [Permissions in Exchange Online](../../permissions-exo/permissions-exo) and [Manage role groups in Exchange Online](../../permissions-exo/role-groups).

&lt;sup&gt;\* You manage these role groups in the Microsoft Entra admin center (https://aad.portal.azure.com).

## Where to find mail flow reports

Open the new EAC at https://admin.exchange.microsoft.com, expand **Reports**, and then select **Mail flow**.

To go directly to the mail flow reports, open https://admin.exchange.microsoft.com/#/reports/mailflowreportsmain.