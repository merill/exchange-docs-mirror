---
layout: Conceptual
title: Configure external calendar sharing in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/configure-external-calendar-share
Manager: dcscontentpm
ms.subservice: sharing
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how to choose Cross-Tenant Access Policy or federation-based configuration and troubleshoot calendar sharing between Exchange organizations.
author: Cloud-Writer
ms.author: meerak
audience: ITPro
ms.reviewer: shanefe
ms.localizationpriority: medium
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
ms.service: exchange-online
ms.topic: how-to
ms.date: 2026-10-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b92cac02-dd0e-0e37-fbdc-4f064711d468
document_version_independent_id: 2cb675d0-b2bd-1a59-2aa7-2aa924575bf6
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/configure-external-calendar-share.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/configure-external-calendar-share
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/configure-external-calendar-share.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 1f9d647f-195a-3218-45dd-d46510f0e082
---

# Configure external calendar sharing in Exchange Online | Microsoft Learn

External calendar sharing lets users share calendar information between separate Exchange organizations. The organization that owns the calendar controls the permitted access and level of detail. The required configuration depends on where the mailboxes are hosted and whether Microsoft 365 Cross-Tenant Access Policy (XTAP) is available.

This model is different from anonymous calendar publishing. For recipients who don't use an applicable cross-tenant or federated sharing configuration, see [Publish and subscribe to calendars](publish-subscribe-calendars).

## Required configuration

Choose the configuration for your scenario:

- **Between Microsoft 365 tenants:** Use Microsoft 365 Cross-Tenant Access Policy when it's available for your tenants. XTAP replaces organization relationships and sharing policies for free/busy, shared-calendar, and MailTips access between organizations hosted in Microsoft 365.
- **With on-premises Exchange organizations, including hybrid scenarios:** Keep the required federation, organization relationships, and sharing policies. XTAP doesn't replace the configuration needed for access to on-premises mailboxes.

Important

XTAP is rolling out and might not yet be available in your tenant. Check the Microsoft 365 Message center and follow [Migrate to Microsoft 365 Cross-Tenant Access Policy](migrate-to-m365-xtap) to inventory, configure, test, and migrate your existing settings. Keep sharing policies that are still needed for on-premises or hybrid organizations.

XTAP controls inbound access. For bidirectional sharing, both organizations must configure complementary policies. Follow the migration guide's testing and cleanup sequence: organization relationships take precedence for free/busy, while an applicable XTAP calendar-sharing capability takes precedence over sharing policies. An `Anonymous` sharing-policy entry with a higher access level can still apply, so follow the guide's instructions to configure the Anonymous capability before testing.

The federation-based configuration described in the following sections depends on these components:

- **Federation trust:** Establishes trust with the Microsoft identity service so Exchange organizations can exchange protected sharing information.
- **Organization relationship:** Identifies the external domains and controls organization-level calendar availability sharing.
- **Sharing policy:** Controls which external domains users can share with and the maximum calendar detail they can expose.

Tenant administrators manage these settings. Users can't override the limits established by the applicable configuration. If you're configuring or troubleshooting XTAP, use the [migration guide](migrate-to-m365-xtap) instead of applying the federation-based steps below.

## Review federation information

Use Exchange PowerShell to review the local federation configuration and retrieve federation information for the external domain:

```powershell
Get-FederatedOrganizationIdentifier
Get-FederationInformation -DomainName fourthcoffee.com
Get-FederationTrust
```

For command details, see [Get-FederatedOrganizationIdentifier](/en-us/powershell/module/exchangepowershell/get-federatedorganizationidentifier), [Get-FederationInformation](/en-us/powershell/module/exchangepowershell/get-federationinformation), and [Get-FederationTrust](/en-us/powershell/module/exchangepowershell/get-federationtrust).

For Microsoft 365 organizations, the federation information for the external domain should identify Microsoft Online as the token issuer and provide the expected target application URI.

Hybrid organizations can require separate relationships for cloud and on-premises mailboxes. Verify the location of the mailboxes in both organizations before changing the configuration.

## Configure an organization relationship

An organization relationship can be created in the Exchange admin center or with Exchange Online PowerShell. It should include the external organization's domains and the calendar access settings that your organization intends to expose.

Review the documented procedure in [Create an organization relationship in Exchange Online](/en-us/exchange/sharing/organization-relationships/create-an-organization-relationship).

To inspect an existing relationship, use [Get-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/get-organizationrelationship):

```powershell
Get-OrganizationRelationship |
    Format-List Name,DomainNames,Enabled,FreeBusyAccessEnabled,FreeBusyAccessLevel,TargetApplicationUri
```

Confirm that:

- The relationship is enabled.
- `DomainNames` includes the recipient's domain.
- Calendar availability access is enabled at the intended level.
- The target application URI is appropriate for the external organization.

## Configure the sharing policy

The sharing policy assigned to a mailbox determines which external domains the user can share with and the maximum detail level.

Use [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox) to identify the assigned policy and [Get-SharingPolicy](/en-us/powershell/module/exchangepowershell/get-sharingpolicy) to review its domain entries:

```powershell
Get-Mailbox user@contoso.com | Format-List SharingPolicy
Get-SharingPolicy "Default Sharing Policy" | Format-List Domains
```

A policy can contain entries for specific federated domains and a wildcard entry for other federated domains. The most specific applicable entry determines the permitted detail level.

For supported domain-entry values and syntax, see [Set-SharingPolicy](/en-us/powershell/module/exchangepowershell/set-sharingpolicy#-domains).

Do not configure consumer email domains as federated domain entries unless they are part of an Exchange organization with the required federation configuration. For recipients who don't use an applicable cross-tenant or federated sharing configuration, use [anonymous publishing](publish-subscribe-calendars).

## Troubleshoot external sharing

### The recipient cannot view availability

First, identify the configuration that applies. For Microsoft 365 tenants using XTAP, verify the inbound policy in the organization that owns the calendar and follow the testing steps in [Migrate to Microsoft 365 Cross-Tenant Access Policy](migrate-to-m365-xtap). Existing organization relationships take precedence for free/busy, so follow the guide before disabling or removing them.

For federation-based sharing:

1. Confirm that the sender and recipient addresses use the expected domains.
2. Confirm that the organization relationship is enabled and includes the external domain.
3. Confirm that calendar availability access is enabled at the required level.
4. Confirm that federation information can be retrieved for the external domain.
5. In hybrid deployments, confirm that the relationship targets the environment that hosts the mailbox.

### A sharing invitation cannot be accepted

Sharing invitations contain protected data. Mail flow rules, disclaimers, routing services, or third-party message-processing products can invalidate an invitation if they change its content or message class.

1. Send a new sharing invitation and accept it promptly.
2. Review mail flow rules that add disclaimers or otherwise modify external messages.
3. Review connectors and third-party mail-processing services in the sender's and recipient's mail paths.
4. Confirm that the invitation arrives as a calendar-sharing message rather than a normal email message.
5. After correcting the mail path, send a new invitation instead of reusing the modified invitation.

### The available detail level is lower than expected

For XTAP calendar sharing, review the applicable inbound calendar-sharing capability in the organization that owns the calendar. When a capability applies, it takes precedence over the sharing policy, except that an `Anonymous` sharing-policy entry with a higher access level can still apply. See [Migrate to Microsoft 365 Cross-Tenant Access Policy](migrate-to-m365-xtap).

For federation-based sharing:

1. Identify the sharing policy assigned to the sender's mailbox.
2. Review the domain-specific and wildcard entries in that policy.
3. Review the organization relationship's free/busy access level.
4. Adjust only the setting that is intended to permit the additional information, and keep the exposure no broader than required.

## Related calendar-sharing articles

- [Calendar sharing overview](/en-us/exchange/sharing/calendar-share-overview)
- [Migrate to Microsoft 365 Cross-Tenant Access Policy](/en-us/exchange/sharing/migrate-to-m365-xtap)
- [Publishing and subscribing](/en-us/exchange/sharing/publish-subscribe-calendars)
- [Resolve issues with calendar sharing in classic Outlook for Windows](/en-us/troubleshoot/exchange/calendars/sharing/resolve-legacy-calendar-share-issues)
- [Resolve issues with modern calendar sharing](/en-us/troubleshoot/exchange/calendars/sharing/resolve-modern-calendar-share-issues)
- [Delegate access and calendar sharing via REST](/en-us/exchange/sharing/manage-calendar-delegate-access)