---
layout: Conceptual
title: Permissions in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/permissions-exo/permissions-exo
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
description: Exchange Online in Microsoft 365 and Office 365 includes a large set of predefined permissions, based on the Role Based Access Control (RBAC) permissions model, which you can use right away to easily grant permissions to your admins and users. You can use the permissions features in Exchange Online so that you can get your new organization up and running quickly.
ms.topic: article
author: Simonv100
ms.author: simonklan
ms.assetid: 3a219732-87e7-4f11-96bc-8edd2cc91926
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-07-13T00:00:00.0000000Z
locale: en-us
document_id: 3f333b76-dca6-5f8d-2cf2-6e3d01faba4c
document_version_independent_id: e4286faa-224b-06aa-994d-29ee568c0aca
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/permissions-exo/permissions-exo.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: permissions-exo/permissions-exo
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/permissions-exo/permissions-exo.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 2400738f-210f-f7b1-3abc-1f77a0614154
---

# Permissions in Exchange Online | Microsoft Learn

Global roles in Microsoft Entra ID allow you to manage permissions and access to capabilities in all of Microsoft 365, which also includes Exchange Online. For more information, see [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal).

But, if you need to limit permissions and capabilities to features in Exchange Online, you can assign **Exchange Online** permissions in the Exchange admin center (EAC) and in Exchange Online PowerShell.

To manage Exchange Online permissions in the EAC, go to **Roles** &gt; **Admin roles** or go directly to the **Admin roles** page at https://admin.exchange.microsoft.com/#/adminRoles.

You need to be member of the **Organization Management** role group in Exchange Online. Specifically, the **Role Management** role in Exchange Online allows users to view, create, and modify Exchange Online role groups. By default, that role is assigned only to the **Organization Management** role group.

Exchange Online includes a large set of predefined permissions, based on the Role Based Access Control (RBAC) permissions model, which you can use right away to easily grant permissions to your admins and users. You can use the permissions features in Exchange Online to get your new organization up and running quickly.

Tip

Managing permissions in Exchange Online gives users access to features in the EAC and Exchange Online PowerShell. To grant permissions to other features, such as compliance features in the Microsoft Purview compliance portal, or security features in the Microsoft Defender portal, see the following articles:

- [Permissions in the Microsoft Purview compliance portal](/en-us/purview/purview-compliance-portal-permissions)
- [Microsoft Defender for Office 365 permissions in the Microsoft Defender portal](/en-us/defender-office-365/mdo-portal-permissions)

Several advanced RBAC features and concepts aren't discussed in this article. If the functionality described in this article doesn't meet your needs, and you want to further customize your permissions model, see [Understanding Role Based Access Control](../understanding-role-based-access-control-exchange-2013-help).

## Role-based permissions

Exchange Online permissions are based on the RBAC permissions model. RBAC is the same permissions model that's used by most Microsoft 365 services and Exchange Server; so if you're familiar with the permission structure in these services, granting permissions in Exchange Online should be familiar.

- A **role** or **management role** grants the permissions to do a set of tasks. Exchange Online permissions use the following types of roles:

    - **Administrator roles**: Defines the set of tasks that an admin can do. When an administrator role is assigned to a **role group**, and an admin or user is a member of that role group, that person is granted the permissions provided by the role. These roles are listed and described in this article.
    - **End-user roles**: These roles, which are assigned using **role assignment policies**, enable users to manage aspects of their own mailbox and distribution groups that they own. End-user roles begin with the prefix `My`. For more information, see the section later in this article.
    - **Application roles**: These role names that start or end with 'Application' are part of RBAC for Applications in Exchange Online. For more information, see [Role Based Access Control for Applications in Exchange Online](/en-us/exchange/permissions-exo/application-rbac).

    Roles give users permissions to perform tasks by making Exchange Online cmdlets available to users. Because the EAC and Exchange Online PowerShell use cmdlets to manage Exchange Online, granting access to a cmdlet gives the admin or user permission to do the task in either of the Exchange Online management interfaces.
- A **role group** makes it easier to assign **roles** to admins. When a role is assigned to a role group, the permissions granted by the role are granted to all the members of the role group. Exchange Online permissions include default role groups for the most common tasks and functions that you need to assign. You can also create custom role groups. We recommend adding individual users as **members** to the default role groups or custom role groups instead of assigning roles directly to users. Role group members can be Exchange Online users and members of other role groups.

    Adding users to Exchange Online role groups grants administrative rights to users in Exchange Online without even requiring to add them to Microsoft Entra roles. Users receive the permissions granted by the role group in Exchange Online only without permission to other Microsoft 365 features or workload.

[![Role, role group and member relationship.](../exchangeonline/media/itpro_security_rbac_exo_simplifiedrolegrouprelationship.png)](../exchangeonline/media/itpro_security_rbac_exo_simplifiedrolegrouprelationship.png#lightbox)

The rest of this article describes the administrator roles and role groups in Exchange Online.

Tip

A **role assignment policy** is a type of role group that's used to assign **end-user roles** to users. For more information, see [Role assignment policies in Exchange Online](role-assignment-policies).

### Role groups in Exchange Online

The table in this section lists the default administrator role groups that are available in Exchange Online, and the roles that are assigned to the role groups by default. To grant permissions to a user to perform tasks in Exchange Online, add them to the appropriate role group.

If you work in a small organization that has only a few admins, you might need to add those admins to the Organization Management role group only, and you might never need to use the other role groups. If you work in a larger organization, you might have admins who perform specific tasks administering Exchange Online, such as recipient configuration. In those cases, you might add one administrator to the Recipient Management role group and another administrator to the Organization Management role group. Those admins can then manage their specific areas of Exchange Online, but they don't have permissions to manage areas they're not responsible for.

As a further example, if an admin is added to the Audit Logs role group, they only have access to the parameter set relating to audit settings within the `Set-Mailbox` cmdlet. If another admin is added to the Mail Recipients role group, they have access to a much larger parameter set within the `Set-Mailbox` cmdlet, allowing management of recipients to a greater extent.

If the built-in role groups in Exchange Online don't match the job function of your admins, you can create role groups and add roles to them. For more information, see [Manage role groups in Exchange Online](role-groups).

Tip

Unless otherwise noted, the same roles group and role assignments are used in [the Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/standalone-eop).

| Role group | Description | Default roles assigned |
| --- | --- | --- |
| Communication Compliance | The role assignments in this role group give access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Communication Compliance Admin  Communication Compliance Investigation |
| Communication Compliance Administrators | The role assignments in this role group give access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Communication Compliance Admin |
| Compliance Administrator | Manage settings for device management, data loss prevention, reports, and preservation. | Communication Compliance Admin  Insider Risk Management Admin |
| Compliance Management | Members can configure and manage compliance settings within Exchange in accordance with their policies. | Audit Logs  Compliance Admin  Data Loss Prevention  Information Rights Management  Journaling  Message Tracking  Retention Management  Transport Rules  View-Only Audit Logs  View-Only Configuration  View-Only Recipients |
| Discovery Management | Members can perform searches of mailboxes in the Exchange Online organization for data that meets specific criteria and can also configure legal holds on mailboxes. | Legal Hold  Mailbox Search |
| ExchangeServiceAdmins\_-&lt;unique value&gt;¹ | Membership in this role group is synchronized across services and is managed centrally. You can't manage this role group in Exchange Online.  This role group doesn't have any roles assigned to it. However, it's a member of the Organization Management role group (as Exchange Service Administrator) and inherits the permissions provided by that role group.  You can add members to this role group by adding users to the Microsoft Entra ID Exchange admin role in the Microsoft 365 admin center. | n/a |
| Help Desk | Members can view and manage the configuration for individual recipients and view recipients in an Exchange organization. Members of this role group can only manage the configuration each user can manage on their own mailbox. | Reset Password  User Options  View-Only Recipients |
| Hygiene Management | Members can manage Exchange anti-spam features, grant permissions for antivirus products to integrate with Exchange, and manage mail flow rules. | Transport Hygiene  View-Only Configuration  View-Only Recipients |
| Information Protection | Full control over all information protection features, including sensitivity labels and their policies, DLP; all classifier types, activity and content explorers; and all related reports. | Information Protection Admin  Information Protection Analyst²  Information Protection Investigator  Information Protection Reader |
| Information Protection Admins | The role assignments in this role group give access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Information Protection Admin |
| Information Protection Analysts | The role assignments in this role group give access to the [Search-UnifiedAuditLog](/en-us/powershell/module/exchangepowershell/search-unifiedauditlog) cmdlet in Exchange Online. | Information Protection Analyst² |
| Information Protection Investigators | Search the unified audit log | Information Protection Investigator |
| Information Protection Readers | Search the unified audit log and view the Mail Traffic and Mail Traffic Summary reports. | Information Protection Reader |
| Insider Risk Management | Manage access control for Insider risk management. | Insider Risk Management Admin  Insider Risk Management Investigation |
| Insider Risk Management Admins | The role assignments in this role group give access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Insider Risk Management Admin |
| Insider Risk Management Investigators | The role assignments in this role group give access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Insider Risk Management Investigation |
| Organization Management | Members have administrative access to the entire Exchange Online organization and can perform almost any task in Exchange Online. **Important**: Because the Organization Management role group is a powerful role, only users that perform organizational-level administrative tasks that can potentially impact the entire Exchange Online organization should be members of this role group. | Audit Logs  Communication Compliance Admin  Communication Compliance Investigation  Compliance Admin  Data Loss Prevention  Distribution Groups  E-Mail Address Policies  Federated Sharing  Information Protection Admin  Information Protection Analyst²  Information Protection Investigator  Information Protection Reader  Information Rights Management  Insider Risk Management Admin  Insider Risk Management Investigation  Journaling  Legal Hold  Mail Enabled Public Folders  Mail Recipient Creation  Mail Recipients  Mail Tips  Message Tracking  Migration  Move Mailboxes  Org Custom Apps  Org Marketplace Apps  Organization Client Access  Organization Configuration  Organization Transport Settings  Privacy Management Admin  Privacy Management Investigation  Public Folders  Recipient Policies  Remote and Accepted Domains  Reset Password  Retention Management  Role Management  Security Admin  Security Group Creation and Membership  Security Reader  TenantPlacesManagement  Transport Hygiene  Transport Rules  User Options  View-Only Audit Logs  View-Only Configuration  View-Only Recipients |
| Privacy Management | The role assignments in this role group give access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Privacy Management Admin  Privacy Management Investigation |
| Privacy Management Administrators | The role assignments in this role group give access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Privacy Management Admin |
| Privacy Management Investigators | The role assignments in this role group give access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Privacy Management Investigation |
| Recipient Management | Members have administrative access to create or modify Exchange Online recipients within the Exchange Online organization. | Distribution Groups  Mail Recipient Creation  Mail Recipients  Message Tracking  Migration  Move Mailboxes  Recipient Policies  Reset Password |
| Records Management | Members can configure compliance features, such as retention policy tags, message classifications, and mail flow rules (also known as transport rules). | Audit Logs  Journaling  Message Tracking  Retention Management  Transport Rules |
| RIM-MailboxAdmins&lt;GUID&gt; | Not used | ApplicationImpersonation |
| Security Administrator | Membership in this role group is synchronized across services and is managed centrally. You can't manage this role group in Exchange Online.  You can add members to this role group by adding users to the Microsoft Entra Security admin role in the Microsoft 365 admin center. | Security Admin  SensitivityLabelAdministrator |
| Security Operator | Manage security alerts, and also view reports and settings of security features. | Tenant AllowBlockList Manager |
| Security Reader | Membership in this role group is synchronized across services and is managed centrally. You can't manage this role group in Exchange Online.  You can add members to this role group by adding users to the Microsoft Entra Security reader role in the Microsoft 365 admin center. | Security Reader |
| TenantAdmins\_-&lt;unique value&gt; | Membership in this role group is synchronized across services and is managed centrally. You can't manage this role group in Exchange Online.  This role group doesn't have any roles assigned to it. However, it's a member of the Organization Management role group (as Company Administrator) and inherits the permissions provided by that role group.  You can add members to this role group by adding users to the Microsoft Entra ID **Global Administrator** role in the Microsoft 365 admin center. **Important**: Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role. | n/a |
| View-Only Organization Management | Members can view the properties of any object in the Exchange Online organization. | View-Only Configuration  View-Only Recipients |

¹ This role group isn't available in [the Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/standalone-eop).

² By default, this role isn't assigned any role group in [the Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/standalone-eop).

## Roles in Exchange Online

The table in this section lists the available administrator roles and the role groups that they're assigned to by default.

Roles that **aren't** assigned to the Organization Management role group by default are marked with ^\*^

Tip

- Role names that start with the prefix 'My' (for example, MyContactInformation) are end-user roles. End-user roles are assigned to users in role assignment policies, which allow users to operate on objects they own (for example, their own account or distribution groups they created). For more information, see [Role assignment policies in Exchange Online](role-assignment-policies).
- Role names that start or end with 'Application' are part of RBAC for Applications in Exchange Online. For more information, see [Role Based Access Control for Applications in Exchange Online](application-rbac).
- Many of the compliance-related roles that are also available in Microsoft Purview compliance and Microsoft Entra don't offer much capability in Exchange Online by themselves.
- Unless otherwise noted, the same roles and role group assignments are used in [the Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/standalone-eop).

| Role | Description | Default role group assignments |
| --- | --- | --- |
| Address Lists^\*^ | Enables admins to manage address lists, global address lists, and offline address lists in an organization. | None |
| Audit Logs | Search the administrator audit log and view the results. | Compliance Management  Organization Management  Records Management |
| Communication Compliance Admin | This role gives access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Communication Compliance  Communication Compliance Administrators  Compliance Administrator  Organization Management |
| Communication Compliance Investigation | This role gives access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Communication Compliance  Organization Management |
| Compliance Admin | Lets people view and edit settings and reports for compliance features. | Compliance Management  Organization Management |
| Data Loss Prevention | This role was related to the older mail flow rule (transport rule)related Data Loss Prevention (DLP) settings in the organization. This role gives access to report and mail flow rule management in Exchange Online. | Compliance Management  Organization Management |
| Distribution Groups | Create and manage all distribution groups, mail-enabled security groups, and members. | Organization Management  Recipient Management |
| E-Mail Address Policies | Enables admins to manage email address policies in an organization. | Organization Management |
| Federated Sharing | Enables admins to manage cross-forest and cross-organization sharing in an organization. | Organization Management |
| Information Protection Admin | This role gives access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Information Protection  Information Protection Admins  Organization Management |
| Information Protection Analyst | This role gives access to the [Search-UnifiedAuditLog](/en-us/powershell/module/exchangepowershell/search-unifiedauditlog) cmdlet in Exchange Online. | Information Protection  Information Protection Analysts¹  Organization Management |
| Information Protection Investigator | Search the unified audit log. | Information Protection  Information Protection Investigators  Organization Management |
| Information Protection Reader | Search the unified audit log and view the Mail Traffic and Mail Traffic Summary reports. | Information Protection  Information Protection Readers  Organization Management |
| Information Rights Management | Manage the Information Rights Management (IRM) features of Exchange in an organization. | Compliance Management  Organization Management |
| Insider Risk Management Admin | This role gives access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Compliance Administrator  Insider Risk Management  Insider Risk Management Admins  Organization Management |
| Insider Risk Management Investigation | This role gives access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Insider Risk Management  Insider Risk Management Investigators  Organization Management |
| Journaling | Enables admins to manage journaling configuration in an organization. | Compliance Management  Organization Management  Records Management |
| Legal Hold | Enables admins to configure whether data within a mailbox should be retained for litigation purposes in an organization. | Discovery Management  Organization Management |
| Mail Enabled Public Folders | Enables admins to configure whether individual public folders are mail-enabled or mail-disabled in an organization. | Organization Management |
| Mail Recipient Creation | Create and remove mail users and mail contacts. | Organization Management  Recipient Management |
| Mail Recipients | Modify existing mail users and mail contacts. | Organization Management  Recipient Management |
| Mail Tips | Enables admins to manage MailTip settings in an organization. | Organization Management |
| Mailbox Import Export^\*^ | Enables admins to import and export mailbox content. | None |
| Mailbox Search^\*^ | Enables admins to search the content of one or more mailboxes in an organization. | Discovery Management |
| Message Tracking | Enables admins to track messages in an organization. | Compliance Management  Organization Management  Recipient Management  Records Management |
| Migration | Enables admins to migrate mailboxes and mailbox content into or out of an organization. | Organization Management  Recipient Management |
| Move Mailboxes | Enables admins to move mailboxes. | Organization Management  Recipient Management |
| O365SupportViewConfig^\*^ | Not used | None |
| Org Custom Apps | Enables users to view and modify their org custom apps. | Organization Management |
| Org Marketplace Apps | Enables users to view and modify their org marketplace apps. | Organization Management |
| Organization Client Access | Enables admins to manage Client Access settings in an organization. | Organization Management |
| Organization Configuration | Enables admins to manage organization-wide settings. | Organization Management |
| Organization Transport Settings | Enables admins to manage hybrid and organization-wide mail transport settings. | Organization Management |
| Privacy Management Admin | This role gives access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Organization Management  Privacy Management  Privacy Management Administrators |
| Privacy Management Investigation | This role gives access to the [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction) cmdlet in Exchange Online. | Organization Management  Privacy Management  Privacy Management Investigators |
| Public Folders | Enables admins to manage public folders in an organization. | Organization Management |
| Recipient Policies | Enables admins to manage recipient policies (authentication policies, data encryption policies, mobile device mailbox policies, and Outlook on the web mailbox policies) in an organization. | Organization Management  Recipient Management |
| Remote and Accepted Domains | Manage remote domains, accepted domains, and connectors. | Organization Management |
| Reset Password | Enables admins to set room mailbox passwords. | Help Desk  Organization Management  Recipient Management |
| Retention Management | Lets people manage retention policies. | Compliance Management  Organization Management  Records Management |
| Role Management | Enables admins to manage management role groups, role assignment policies, management roles, role entries, assignments, and scopes in an organization. | Organization Management |
| Security Admin | Manages the configuration and reports for all security and protection features. | Organization Management  Security Administrator |
| Security Group Creation and Membership | Create and manage mail-enabled security groups. | Organization Management |
| Security Reader | View the configuration and reports for security and protection features. | Organization Management  Security Reader |
| SensitivityLabelAdministrator^\*^ | Lets people edit sensitivity label properties. | Security Administrator |
| Tenant AllowBlockList Manager^\*^ | Lets people manage the Tenant Allow/Blocklist. | Security Operator |
| TenantPlacesManagement | Lets people manage settings for [Microsoft Places](/en-us/deployoffice/places/deployment-guide-for-places). | Organization Management |
| Transport Hygiene | Manage anti-malware, anti-spam features, and anti-spoofing features. | Hygiene Management  Organization Management |
| Transport Rules | Create and manage mail flow rules (also known as transport rules). | Compliance Management  Organization Management  Records Management |
| User Options | Enables admins to view the Outlook on the web options of users in the organization. | Help Desk  Organization Management |
| View-Only Audit Logs | Searches the administrator audit log and views the results. | Compliance Management  Organization Management |
| View-Only Configuration | Views all of the organization and mail flow (non-recipient) settings in the organization. | Compliance Management  Hygiene Management  Organization Management  View-Only Organization Management |
| View-Only Recipients | View recipient properties and run message trace. | Compliance Management  Help Desk  Hygiene Management  Organization Management  View-Only Organization Management |

¹ By default, this role isn't assigned to any role groups in the Built-in security add-on for on-premises mailboxes.

## Microsoft 365 permissions in Exchange Online

When you create a user in the Microsoft 365 admin center, you can choose whether to assign various Microsoft Entra roles (for example, Exchange Administrator or Global Reader) to the user. Most of the Microsoft Entra roles grant administrative permissions to the user in Exchange Online.

Note

The account you used to create your Exchange Online organization is automatically assigned to the Global Administrator role.

The following table lists the Microsoft Entra roles and the Exchange Online role groups that they correspond to. For more information about these roles, see [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal).

| Microsoft Entra role | Exchange Online role group |
| --- | --- |
| Global Administrator | Organization Management **Note**: The Global Administrator role and the Organization Management role group are tied together using a special Company Administrator role group. The Company Administrator role group is managed internally and can't be modified directly. |
| Exchange Administrator | Organization Management |
| Global Reader | View-Only Organization Management |
| Helpdesk Administrator | Help Desk |
| Service Support Administrator | None |
| SharePoint Administrator | None |
| Teams Administrator | None |
| Exchange Recipient Administrator | Recipient Management |
| User Experience Success Manager | None |

Users can be granted administrative rights in Exchange Online without requiring to add them to Microsoft Entra roles by adding the user as a member of an Exchange Online role group. The user gets permissions in Exchange Online, but they don't get permissions in other Microsoft 365 workloads.

Important

Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.