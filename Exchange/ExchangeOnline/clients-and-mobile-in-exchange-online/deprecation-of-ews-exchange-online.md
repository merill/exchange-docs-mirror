---
layout: Conceptual
title: Deprecation of Exchange Web Services in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/deprecation-of-ews-exchange-online
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
f1.keywords:
- NOCSH
ms.topic: article
ai-usage: ai-assisted
author: chrisda
ms.author: tmechelke
ms.service: exchange-online
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid: MET150
description: Learn about deprecation of Exchange Web Services (EWS) in Exchange Online
audience: Admin
ms.date: 2025-04-01T00:00:00.0000000Z
locale: en-us
document_id: 1cb5eb0b-92e6-92ab-0b7e-c13c6ac7ac83
document_version_independent_id: d01fa1c6-846a-209f-0a25-1480752456ca
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/deprecation-of-ews-exchange-online.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/deprecation-of-ews-exchange-online
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/deprecation-of-ews-exchange-online.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: a21fe27f-f46a-8cc8-6380-fedfe32c7b15
---

# Deprecation of Exchange Web Services in Exchange Online | Microsoft Learn

In 2018, we announced that [Exchange Web Services (EWS) will no longer receive functionality updates](https://techcommunity.microsoft.com/blog/exchange/upcoming-changes-to-exchange-web-services-ews-api-for-office-365/608055). In 2023, we announced that [EWS will be disabled in Exchange Online in October 2026](https://devblogs.microsoft.com/microsoft365dev/retirement-of-exchange-web-services-in-exchange-online/). See blog post [Exchange Online EWS, Your Time is Almost Up](https://techcommunity.microsoft.com/blog/exchange/exchange-online-ews-your-time-is-almost-up/4492361) for the latest updates on timeline and disablement process.

| **Are you here because your Exchange Online EWS applications have stopped working? [Read this](https://techcommunity.microsoft.com/blog/exchange/exchange-online-ews-application-stopped-working-do-this-/4566215)** |
| --- |

The [Midnight Blizzard security incident](https://www.microsoft.com/security/blog/2024/01/25/midnight-blizzard-guidance-for-responders-on-nation-state-attack/) in January 2024 involved EWS and elevated the urgency of the EWS deprecation effort. The scope was also widened from third party applications to include all Microsoft applications. We're working diligently to remove EWS dependencies in all Microsoft products. For example:

- Microsoft Outlook
- Microsoft Office
- Microsoft Teams
- Microsoft Dynamics 365

You can find the latest information on Microsoft products that use EWS here: [Baseline Security Mode Settings](/en-us/microsoft-365/baseline-security-mode/baseline-security-mode-settings#exchange-web-services-requirements)

This work accelerated the need to close parity gaps between EWS and Microsoft Graph for many scenarios. Other efforts are underway in the following scenarios:

- Close the remaining parity gaps that affect specific scenarios for third party applications.
- Provide guidance for alternative solutions.

To learn if your third party applications use EWS, see [this article](https://aka.ms/ewsIdentifyApps).

Many application scenarios are already supported with [direct mappings between EWS operations and Graph APIs](https://aka.ms/ews2graphMap).

To move your organization to a stronger security posture, we recommend identifying your active EWS applications and starting their migration now.

To simplify and accelerate your analysis and migration, we introduced the [EWS Usage Reports](/en-us/microsoft-365/admin/activity-reports/ews-usage), the [EWS Analyzer tool](https://aka.ms/ewsTools), and a tutorial for [AI assisted code analysis and refactoring](https://aka.ms/ewsToolsAITutorial).

## Roadmap for parity gaps

The following EWS API gaps are prioritized for delivery. Estimated availability dates are targets and might change. If an EWS capability isn't listed in this roadmap table, don't plan on a corresponding Microsoft Graph or Exchange Admin API capability being available before EWS is fully disabled.

| Gap | Capability description | ETA |
| --- | --- | --- |
| Import-Export (Archive) | Export and import mailbox items in archive mailboxes in a full-fidelity format. | Q4 CY2026 |
| Import-Export (Public Folder) | Export and import public folder items in a full-fidelity format. This capability doesn't include public folder CRUD APIs. | Q4 CY2026 |
| Import-Export (Group) | Export and import items in Microsoft 365 Group mailboxes in a full-fidelity format. | Q4 CY2026 |
| In-Place Archive (Generic CRUD) | Access and manage mailbox items in an existing In-Place Archive. This capability doesn't create archive mailboxes. | Q4 CY2026 |
| Notes | Access and manage Exchange mailbox notes (`IPM.StickyNote`) through Microsoft Graph. | Q3 CY2026 |
| Exchange Admin API | Manage selected Exchange recipient and mailbox settings, including folder permissions, through Exchange Admin APIs. | Q4 CY2026 |
| Sovereign Cloud availability | Make Exchange workload APIs required for EWS migration available in supported sovereign clouds. | Q4 CY2026 |
| Report Message | Report a message as junk, phishing, or not junk, which improves mail filtering. | Q4 CY2026 |
| Non-draft MIME update/creation | Create or update non-draft messages by using MIME content. | Q4 CY2026 |
| User Configuration objects | Access and manage user configuration objects stored as folder-associated items in mailbox folders. | Q4 CY2026 |
| Contact Lists | Access and manage personal contact lists stored in a mailbox. | Q3 CY2026 |
| Additional Contact Properties | Access additional personal contact properties that are available in EWS but not Microsoft Graph. | Q3 CY2026 |
| Mark All Items As Read | Update the read state of all messages in a mail folder in one operation. | Q4 CY2026 |

### Confirmed capabilities that won't be added

The following EWS capabilities won't be added to Microsoft Graph. Plan migrations without a Graph equivalent for these capabilities.

| Capability | Description |
| --- | --- |
| Generic Public Folder CRUD | Generic folder and item create, read, update, and delete operations in Public Folders. Public Folder import and export is a separate capability. |
| Generic Microsoft 365 Group mailbox CRUD | Generic mailbox folder and item CRUD for Microsoft 365 Group mailboxes. Use the supported Microsoft Graph APIs for group conversations, threads, and posts. Group mailbox import and export is a separate capability. |
| Discovery Mailbox access | Generic mailbox, folder, and item access for legacy Discovery Mailboxes. Use Microsoft Purview eDiscovery APIs and workflows for supported discovery capabilities. |

## EWS deprecation timeline

- **July 2018**: [EWS deprecation announced](https://techcommunity.microsoft.com/blog/exchange/upcoming-changes-to-exchange-web-services-ews-api-for-office-365/608055).
- **2023**: [EWS disablement date set to 10/2026](https://aka.ms/ewsDeprecation).
- **January 2024**: [Midnight Blizzard](https://aka.ms/mblizz) security incident.
- **2025**:
    - [Import and export of mailboxes in preview (except Microsoft 365 Groups and public folder mailboxes)](/en-us/graph/mailbox-import-export-concept-overview).
    - [EWS Code Analyzer released](https://aka.ms/ewsTools) ([Blog Post](https://aka.ms/ewsToolsPost))
    - [EWS Usage Reports released](https://aka.ms/ewsAdminUsage)
    - [EWS Usage Reporting tool released](https://aka.ms/ewsToolsUsage)
    - [AI Assisted EWS Migration Tutorial released](https://aka.ms/ewsToolsAITutorial)
    - [Administration API preview](/en-us/exchange/reference/admin-api-overview)
    - Allow admins to [manually disable EWS](https://aka.ms/EWSEnabledChange) at the organization and user levels.
- **Upcoming**:
    - Fill parity gaps to support migration for Microsoft and third party applications.
    - Remove EWS dependencies from Microsoft applications.
        - [Outlook mail Connector for PowerBI desktop](/en-us/power-query/connectors/microsoft-exchange-graph)
        - [Changes to the Exchange Online connector in Excel Power Query](https://support.microsoft.com/excel/power-query-exchange-connector-changes)
- **October 2026**: EWS starts to be disabled globally for all organizations. Full details of the process can be found [here](https://aka.ms/EWSEndgame).
- **April 2027**: EWS is fully disabled.

## Call To Action

Don't wait for all parity gaps to be closed. You can be proactive by doing the following steps:

- **Investigate** the EWS footprint of all internal and third party applications in your organization. Start with [EWS Usage Reports](/en-us/microsoft-365/admin/activity-reports/ews-usage)[(direct link)](https://admin.cloud.microsoft/?#/reportsUsage/EWSWeeklyUsage).
- Work with your **security and executive teams** to prioritize EWS deprecation for internal applications.
- Identify applications and components you can **migrate now** and start the implementation. Use the [EWS Analyzer](https://aka.ms/ewsTools) tool and [AI assistance](https://aka.ms/ewsToolsAITutorial) to analyze and refactor EWS code or reimplement in low-code approach with [Power Platform](https://www.microsoft.com/power-platform) or as a [Copilot Agent](/en-us/copilot/agents).
- Work with your **vendors** to prioritize their migration from EWS.

## Resources

- [Exchange Online EWS, Your Time is Almost Up](https://techcommunity.microsoft.com/blog/exchange/exchange-online-ews-your-time-is-almost-up/4492361)
- [Midnight Blizzard](https://aka.ms/mblizz)
- [Exchange Blog - Migration Series](https://aka.ms/ews2graphGettingStarted)
- [Microsoft 365 Developer Blog](https://devblogs.microsoft.com/microsoft365dev/)
- [EWS to Graph API Mappings](https://aka.ms/ews2graphMap)
- [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)
- [How to disable EWS at the organization and user level](https://aka.ms/EWSEnabledChange)
- [EWS Usage Reports released](https://aka.ms/ewsAdminUsage)
- [EWS Usage Reporting tool released](https://aka.ms/ewsToolsUsage)
- [EWS Migration Tools](https://aka.ms/ewsTools)
- [AI Assisted EWS Migration Tutorial](https://aka.ms/ewsToolsAITutorial)
- [Understand HTTP 403 responses in Exchange Online](/en-us/exchange/client-developer/exchange-web-services/how-to-control-access-to-ews-in-exchange#understand-http-403-responses-in-exchange-online)