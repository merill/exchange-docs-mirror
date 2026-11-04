---
layout: Conceptual
title: Feature permissions in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/permissions-exo/feature-permissions
Manager: dansimp
ms.subservice: exo-roles
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: The permissions required to perform tasks to manage Microsoft Exchange Online vary depending on the procedure being performed or the cmdlet you want to run.
ms.topic: how-to
author: Simonv100
ms.author: simonklan
ms.assetid: 15073ce1-0917-403b-8839-02a2ebc96e16
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.custom: seo-marvel-apr2020
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 871b8dd8-981b-fb2a-f237-3add128e7c12
document_version_independent_id: c71fa9f4-c432-4433-9125-e1b4aebbdd19
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/permissions-exo/feature-permissions.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: permissions-exo/feature-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/permissions-exo/feature-permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 9bf7fcf2-602a-910e-5ccf-591df2496f8f
---

# Feature permissions in Exchange Online | Microsoft Learn

The permissions required to perform tasks to manage Microsoft Exchange Online vary depending on the procedure being performed or the cmdlet you want to run.

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.
2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](../understanding-role-based-access-control-exchange-2013-help).
3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    Note

    You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](../delegate-role-assignments-exchange-2013-help).

## Exchange Online permissions

You can use the features in the following table to manage your Exchange Online organization and recipients. Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information about these role groups, see [Role groups](permissions-exo#role-groups-in-exchange-online).

| Feature | Permissions required |
| --- | --- |
| Anti-malware | Organization Management <br> Hygiene Management |
| Anti-spam | Organization Management <br> Hygiene Management |
| Arbitration | Organization Management |
| Client Access user settings | Organization Management |
| Data loss prevention (DLP) | Organization Management <br> Compliance Management |
| Discovery mailboxes - Create | Organization Management <br> Recipient Management |
| Distribution groups | Organization Management <br> Recipient Management |
| Domains | Organization Management |
| Microsoft 365 or Office 365 connectors | Organization Management |
| In-Place eDiscovery | Discovery Management <br>**Note**: By default, the Discovery Management role group doesn't have any members. No users, including admins, have the required permissions to search mailboxes. For more information, see [Assign eDiscovery permissions in Exchange](../security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions). |
| In-Place Hold | Discovery Management <br> Organization Management <br><br>**Notes**: <br><br>- To create a query-based In-Place Hold, a user requires both the Mailbox Search and Legal Hold roles to be assigned via membership in a role group that has both roles assigned. To create an In-Place Hold without using a query, which places all mailbox items on hold, you must have the Legal Hold role assigned. The Discovery Management role group is assigned both roles.<br>- The Organization Management role group is assigned the Legal Hold role. Members of the Organization Management role group can place an In-Place Hold on all items in a mailbox, but can't create a query-based In-Place Hold. |
| Journal archiving | Organization Management <br> Recipient Management |
| Journaling | Organization Management <br> Records Management |
| Linked user | Organization Management <br> Recipient Management |
| Mail flow | Organization Management |
| Mail flow rules | Organization Management |
| Mailbox settings | Organization Management <br> Recipient Management |
| Message Encryption | Organization Management <br> Compliance Management <br><br> Records Management |
| Message trace | Organization Management <br> Compliance Management <br><br> Help Desk |
| Messaging records management | Compliance Management <br> Organization Management <br><br> Records Management |
| Mobile devices | Organization Management <br> Recipient Management |
| Organization configuration | Organization Management |
| Outlook on thew web mailbox policies | Organization Management <br> Recipient Management |
| Permissions and delegation | Organization Management |
| Public folders | Organization Management <br> Public Folder Management <br><br> Mail-enabled public folders require Recipient Management |
| POP3 and IMAP4 permissions | Organization Management |
| Quarantine | Organization Management <br> Hygiene Management |
| Recipients | Organization Management <br> Recipient Management |
| Retention policies | Organization Management <br> Recipient Management <br><br> Records Management |
| Role assignments | Organization Management |
| Supervision | Organization Management |
| Unified Messaging | Organization Management <br> Unified Messaging Management |
| View-only administrator audit logging | Organization Management <br> Records Management |
| View reports | Organization Management: Users have access to mailbox reports and mail protection reports. <br> View-Only Organization Management: Users have access to mailbox reports. <br><br> View-Only Recipients: Users have access to mail protection reports. <br><br> Compliance Management: Users have access to mail protection reports and data loss prevention (DLP) reports (if their subscription has DLP capabilities). |

Note

To find the permissions that are required to run any Exchange Online cmdlet, see [Find the permissions required to run any Exchange cmdlet](/en-us/powershell/exchange/find-exchange-cmdlet-permissions).