---
layout: Conceptual
title: Diagnostic cmdlets for Exchange Online provisioning issues | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/diagnostic-cmdlets/organization-diagnostic-cmdlets
Manager: anaruxa
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn about the diagnostic cmdlets that help identify and repair Exchange Online provisioning issues with domains, company objects, recipient objects, and RBAC configurations.
ms.topic: article
author: lusassl-msft
ms.author: lusassl
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-03-25T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: dea80b57-1e79-b288-fc76-6c46bfa4096c
document_version_independent_id: ed4c8298-48da-993f-70b7-f6eae599fa5c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/diagnostic-cmdlets/organization-diagnostic-cmdlets.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/diagnostic-cmdlets/organization-diagnostic-cmdlets
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/diagnostic-cmdlets/organization-diagnostic-cmdlets.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: bfd96c4b-838f-3af8-4a3a-c609fc404cac
---

# Diagnostic cmdlets for Exchange Online provisioning issues | Microsoft Learn

Exchange Online provides diagnostic cmdlets that help you identify and repair common provisioning issues. These cmdlets are part of the [Exchange Online PowerShell module](/en-us/powershell/exchange/exchange-online-powershell-v2). They check for mismatches between Microsoft Entra ID and Exchange Online, and they attempt automatic repairs when problems are found.

The following diagnostic cmdlets are available:

- **Invoke-ProvisioningAcceptedDomainDiagnostic**: Verifies and repairs accepted domain configurations.
- **Invoke-ProvisioningCompanyObjectDiagnostic**: Validates and repairs Company Object and service plan configurations.
- **Invoke-ProvisioningRecipientDiagnostic**: Identifies and repairs recipient object provisioning failures.
- **Invoke-ProvisioningVerifyRbacDiagnostic**: Analyzes and repairs role based access control (RBAC) configurations.

## Invoke-ProvisioningAcceptedDomainDiagnostic

The **Invoke-ProvisioningAcceptedDomainDiagnostic** cmdlet verifies whether your organization's email domains are correctly set up in Exchange Online. It identifies situations where a domain exists in Microsoft 365 (Microsoft Entra ID) but is missing, misconfigured, or not fully provisioned in Exchange Online.

If the diagnostic finds a mismatch, it attempts to automatically repair the domain configuration so Exchange Online can recognize and use the domain for email routing, mailbox provisioning, and address policy processing.

The automated repair might take the following actions:

- Recreate a missing accepted domain in Exchange Online.
- Fix incomplete or corrupted domain provisioning.
- Sync updated domain information from Microsoft Entra ID into Exchange Online.
- Resolve issues where email addresses for the domain can't be created or validated.

### Sample output of Invoke-ProvisioningAcceptedDomainDiagnostic

The following example shows the output of the **Invoke-ProvisioningAcceptedDomainDiagnostic** cmdlet when no issues are found:

```powershell
Invoke-ProvisioningAcceptedDomainDiagnostic
```

```output
The diagnostic execution will be logged with RunId: 01008ce9-742c-4735-a4c3-4ce02887ce1f

Cmdlet Parameters
=================

Parameter    Value
---------    -----

Tenant Exchange Online information
==================================

Property                  Value
--------                  -----
Name                      contoso.onmicrosoft.com
OrganizationStatus        Active
ServicePlan               BPOS_S_E15_0
DirSyncServiceInstance    exchange/namprd13-009-01

Tenant Entra ID Domain Information
==================================
contoso.onmicrosoft.com
Tenant Entra ID Initial Domain: contoso.onmicrosoft.com
Tenant Entra ID Default Domain: contoso.onmicrosoft.com
No shared domain information was found in Entra ID for the tenant.

Tenant Exchange Online Domain Information
=========================================
contoso.onmicrosoft.com
Tenant Exchange Online Default Domain: contoso.onmicrosoft.com

Tenant Global Locator Service Domain Information
=================================================
contoso.onmicrosoft.com, GlsAndAd
The number of verified domains in MSO 1 is the same as in Exchange Online 1. (OK)
Found for validated Entra ID domain "contoso.onmicrosoft.com" a GLS and AD entry (OK)

Found GLS entry for domain(s):
==============================

Property                           Value
--------                           -----
DomainName                         contoso.onmicrosoft.com
ExternalDirectoryOrganizationId    00aa00aa-bb11-cc22-dd33-44ee44ee44ee
DomainFlags                        None
DomainInUse                        True
SmtpNextHopDomain
IsValid                            True

Found no tenant GLS entry problems.
Found 1 good GLS domain entries.
Found 0 GLS domain entries assigned to a different tenant.
Found 0 missing GLS domain entries.
The diagnostic did not find any accepted domain issues in Exchange Online.
No issues found.
```

## Invoke-ProvisioningCompanyObjectDiagnostic

The **Invoke-ProvisioningCompanyObjectDiagnostic** cmdlet verifies whether your organization's core Microsoft 365 information (the Company Object) is healthy and correctly synchronized between Microsoft Entra ID and Exchange Online.

Out of sync information or corrupted values can cause issues. For example, missing service plans, licensing problems, or failures when creating or updating mailboxes.

This diagnostic automatically does the following actions:

- Validates your tenant's Company Object settings.
- Checks for missing or failed service plan provisioning.
- Fixes common synchronization issues between Microsoft Entra ID and Exchange Online.
- Resubmits or repairs failed service plan updates, when possible.

### Sample output of Invoke-ProvisioningCompanyObjectDiagnostic

The following example shows the output of the **Invoke-ProvisioningCompanyObjectDiagnostic** cmdlet when no issues are found:

```powershell
Invoke-ProvisioningCompanyObjectDiagnostic
```

```output
The diagnostic execution will be logged with RunId: a2d8b00e-9c08-4a99-8e09-1d392a01f109

Cmdlet Parameters
=================

Parameter    Value
---------    -----

Tenant Exchange Online information
==================================

Property                  Value
--------                  -----
Name                      contoso.onmicrosoft.com
OrganizationStatus        Active
ServicePlan               BPOS_S_E15_0
DirSyncServiceInstance    exchange/namprd15-015-01

The tenant "contoso.onmicrosoft.com" was successfully found in Exchange Online and Entra ID.

Property                           Value
--------                           -----
Name                               contoso.onmicrosoft.com
ExternalDirectoryOrganizationId    00aa00aa-bb11-cc22-dd33-44ee44ee44ee
DirSyncServiceInstance             exchange/namprd15-015-01
OrganizationStatus                 Active
WhenOrganizationStatusSet          1/21/2026 6:22:05 PM
IsDualWriteEnabled                 True

Delayed license removal is disabled for this tenant.
The BPOS_S mailbox plan for the tenant has the state Enabled.
An organization object update request was sent successfully.
No issues found.
```

## Invoke-ProvisioningRecipientDiagnostic

The **Invoke-ProvisioningRecipientDiagnostic** cmdlet checks for issues that prevent a mailbox, contact, group, or mail user from updating correctly in Exchange Online. Typically, these failures happen when the information stored in Microsoft Entra ID and the information stored in Exchange Online become inconsistent or incomplete.

This diagnostic does the following actions:

- Identifies recipient objects (mailboxes, groups, contacts, mail users) that failed to update or provision correctly.
- Checks for missing or invalid attributes required by Exchange Online.
- Looks for conflicts such as duplicate proxy addresses or inconsistent identity data.
- Repairs common issues by resubmitting or correcting the recipient object so Exchange Online can process it successfully.

### Sample output of Invoke-ProvisioningRecipientDiagnostic

The following example shows the output of the **Invoke-ProvisioningRecipientDiagnostic** cmdlet for a specific recipient:

```powershell
Invoke-ProvisioningRecipientDiagnostic -Recipients akink@contoso.onmicrosoft.com
```

```output
The diagnostic execution will be logged with RunId: c96be213-dce2-40ce-8961-286b51615a54

Cmdlet Parameters
=================

Parameter     Value
---------     -----
Recipients    akink@contoso.onmicrosoft.com

Tenant Exchange Online information
==================================

Property                  Value
--------                  -----
Name                      contoso.onmicrosoft.com
OrganizationStatus        Active
ServicePlan               BPOS_S_E15_0
DirSyncServiceInstance    exchange/namprd15-015-01

Diagnostic is running for the recipient akink@contoso.onmicrosoft.com.

Exchange Online Information
===========================

Property                     Value
--------                     -----
Database                     11bb11bb-cc22-dd33-ee44-55ff55ff55ff
DisplayName                  User Alias
EmailAddresses               SPO:SPO_22cc22cc-dd33-ee44-ff55-66aa66aa66aa@SPO_00aa00aa-bb11-cc22-dd33-44ee44ee44ee, SIP:akink@contoso.onmicrosoft.com, SMTP:akink@contoso.onmicrosoft.com
ExchangeGuid                 33dd33dd-ee44-ff55-aa66-77bb77bb77bb
ExternalDirectoryObjectId    44ee44ee-ff55-aa66-bb77-88cc88cc88cc
Guid                         55ff55ff-aa66-bb77-cc88-99dd99dd99dd
InPlaceHolds
IsExchangeCloudManaged       False
IsSoftDeletedByDisable       False
IsSoftDeletedByRemove        False
LitigationHoldEnabled        False
LitigationHoldOwner
Name                         44ee44ee-ff55-aa66-bb77-88cc88cc88cc
NetID                        10032005829DAF80
RecipientType                UserMailbox
RecipientTypeDetails         UserMailbox
RetentionHoldEnabled         False
SkuAssigned                  True
WhenChangedUTC               2/23/2026 7:12:00 PM
WhenCreatedUTC               1/21/2026 7:22:51 PM
WhenMailboxCreated           1/21/2026 8:49:23 PM
WhenSoftDeleted
WindowsLiveID                akink@contoso.onmicrosoft.com

The recipient object "00aa00aa-bb11-cc22-dd33-44ee44ee44ee_User_44ee44ee-ff55-aa66-bb77-88cc88cc88cc" was successfully found in Entra ID.

Entra ID Information
====================

Property                     Value
--------                     -----
AccountEnabled               True
Alias                        akink
DisplayName                  User Alias
EmailAddressCollection       SMTP:akink@contoso.onmicrosoft.com,SIP:akink@contoso.onmicrosoft.com
ExchangeGuid
ExternalObjectId             00aa00aa-bb11-cc22-dd33-44ee44ee44ee_User_44ee44ee-ff55-aa66-bb77-88cc88cc88cc
NetID                        10032005829DAF80
RecipientTypeDetailsValue
RemoteRecipientType
ServiceInstanceId            exchange/namprd15-015-01
SKUAssigned                  True
SKUCapability                BPOS_S_Enterprise
SKUCapabilityStatus          Enabled
StsRefreshTokensValidFrom    2/20/2026 7:14:25 PM
UserType                     Member
WindowsLiveID                akink@contoso.onmicrosoft.com

User object properties
======================

Property                        Value
--------                        -----
PreviousRecipientTypeDetails    None

Mailbox statistics for mailbox "00aa00aa-bb11-cc22-dd33-44ee44ee44ee\55ff55ff-aa66-bb77-cc88-99dd99dd99dd" -Database 11bb11bb-cc22-dd33-ee44-55ff55ff55ff
=========================================================================================================================================================

Property                           Value
--------                           -----
DisplayName                        User Alias
ItemCount                          84
LastLogonTime                      3/4/2026 12:17:49 AM
ExternalDirectoryOrganizationId    00aa00aa-bb11-cc22-dd33-44ee44ee44ee
LegacyDn                           /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=...

Checking Entra ID Exchange Online license and recipient type.
Licensing Status: Ok

Licensing Notes
===============
An Exchange Online license is assigned to the user object.
A UserMailbox is expected in Exchange Online, and no inconsistencies were found.
The current Exchange Online recipient type details for the recipient "55ff55ff-aa66-bb77-cc88-99dd99dd99dd" is "UserMailbox".
Reviewed Exchange Online and Entra ID proxy addresses; no Exchange Online issues found.

Diagnostic summary:
-------------------
Result SyncedMailboxLocationGuids, 66aa66aa-bb77-cc88-dd99-00ee00ee00ee
Ensured mailbox location information is current and up to date.

Result FoundMailboxStatistics, 77bb77bb-cc88-dd99-ee00-11ff11ff11ff
Found mailbox statistics information for the user mailbox.
```

## Invoke-ProvisioningVerifyRbacDiagnostic

The **Invoke-ProvisioningVerifyRbacDiagnostic** cmdlet reviews a user's permissions in Exchange Online to determine whether their role based access control (RBAC) configuration is correct. It checks all RBAC components that determine what actions the user can perform, and identifies any missing or conflicting assignments.

This diagnostic does the following actions:

- Verifies the user's assigned management roles, role assignments, and role groups.
- Compares RBAC permissions of two users.
- Confirms that permissions are valid, not duplicated, and not in a broken or inconsistent state.
- Detects common RBAC issues that can prevent a user from running specific Exchange Online cmdlets or performing admin tasks.
- Provides guidance or automated repairs if it finds configuration problems that affect the user's ability to administer Exchange Online resources.

### Sample output of Invoke-ProvisioningVerifyRbacDiagnostic

The following example shows the output of the **Invoke-ProvisioningVerifyRbacDiagnostic** cmdlet when checking whether a user can access a specific cmdlet and parameter:

```powershell
Invoke-ProvisioningVerifyRbacDiagnostic -User aking@contoso.onmicrosoft.com -CmdletName Set-Mailbox -CmdletParameters DisplayName
```

```output
The diagnostic execution will be logged with RunId: 5848930a-9300-423f-85b6-b20df01d3d2a

Cmdlet Parameters
=================

Parameter           Value
---------           -----
CmdletName          "Set-Mailbox"
User                aking@contoso.onmicrosoft.com
CmdletParameters    "DisplayName"

Tenant Exchange Online information
==================================

Property                  Value
--------                  -----
Name                      contoso.onmicrosoft.com
OrganizationStatus        Active
ServicePlan               BPOS_S_E15_0
DirSyncServiceInstance    exchange/namprd15-015-01

User RBAC permissions analysis:
===============================
The user is assigned a management role allowing access to the "Set-Mailbox" cmdlet with the "DisplayName" parameter.

Diagnostic summary:
-------------------
Result UserCanAccessCmdlet, 88cc88cc-dd99-ee00-ff11-22aa22aa22aa
The user can access the cmdlet and parameter combination.
```