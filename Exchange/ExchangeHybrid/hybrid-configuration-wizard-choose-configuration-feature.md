---
layout: Conceptual
title: HCW Choose Exchange Hybrid Configuration feature | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-configuration-wizard-choose-configuration-feature
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.topic: how-to
author: lusassl-msft
ms.author: lusassl
description: Admins can learn about how to use the new Exchange Hybrid Configuration 'Choose Exchange Hybrid Configuration' feature.
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
ms.date: 2025-07-24T00:00:00.0000000Z
locale: en-us
document_id: 9905d135-7960-ab11-1220-8fa9607e7afd
document_version_independent_id: ddc8a682-7a8f-d587-0c84-8868ceecca0a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-configuration-wizard-choose-configuration-feature.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-configuration-wizard-choose-configuration-feature
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-configuration-wizard-choose-configuration-feature.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 252d3240-efed-c3f1-db7f-ad94fc64079f
---

# HCW Choose Exchange Hybrid Configuration feature | Microsoft Learn

## Overview

With the new release of the Hybrid Configuration wizard (HCW), administrators can explicitly select the hybrid configurations that should be done during an HCW run. This helps administrators to preserve their customized configurations and prevent HCW from resetting them by selecting and deselecting configurations.

We revised the permissions that are required to run the HCW. The permissions that are required to run the HCW can be found in the [Hybrid Configuration wizard](hybrid-configuration-wizard#account-permissions-requirements) documentation.

## What is the benefit of the new "Choose Exchange Hybrid Configuration" feature

During a rerun of the HCW, administrators don't require many first-time configurations that HCW does. HCW doesn't allow skipping of any configurations, which resets many custom configurations done after previous HCW run. This behavior sometimes leads to a bad Exchange Server hybrid configuration state. You can skip many of the steps, which are not needed for existing hybrid configurations by using the newly introduced `Choose Exchange Hybrid Configuration` feature.

Administrators sometimes need to do HCW reruns for `Organization Configuration Transfer` (OCT) or to perform a TLS certificate update, which isn't available through any other tool. If an HCW rerun is done in addition to OCT and TLS certificate update, HCW resets all hybrid configurations (for example, modification in connectors, migration endpoints etc.) which may not be desired. These changes cause extra configuration overhead as administrators have to adjust the configuration again afterwards. You can avoid this behavior now by using the newly introduced `Choose Exchange Hybrid Configuration` feature.

## Granular configuration options

This section explains the configuration options available when using the `Choose Exchange Hybrid Configuration` feature. You can choose from these options to configure your hybrid deployment according to your needs. We have covered some scenarios of when which option can be used in the FAQ section of this article.

Regardless of the selected option, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-OnPremisesOrganization or Set-OnPremisesOrganization
    [-Name '<guid>']
    [-HybridDomains <AcceptedTrustedDomains>]
    [-InboundConnector 'Inbound from <guid>']
    [-OutboundConnector 'Outbound to <guid>']
    [-OrganizationRelationship 'O365 to On-premises - <guid>']
    [-OrganizationName '<NameOfTheOrganization>']
    [-OrganizationGuid '<guid>']
    [-Comment '<ConfigurationHash>']
```

```powershell
New-HybridConfiguration or Set-HybridConfiguration
    [-ClientAccessServers $null]
    [-ExternalIPAddresses $null]
    [-Domains <AcceptedTrustedDomains>]
    [-OnPremisesSmartHost <OnPremisesEntryPointDomain>]
    [-TLSCertificateName '<I>X.500Issuer<S>X.500Subject']
    [-SendingTransportServers <TransportServers>]
    [-ReceivingTransportServers <TransportServers>]
    [-EdgeTransportServers <EdgeTransportServers> or $null]
    [-Features FreeBusy,MoveMailbox,Mailtips,MessageTracking,OwaRedirection,OnlineArchive,SecureMail,Photos]
```

### Configure Hybrid Features

The `Configure Hybrid Features` section contains settings that can be used to configure hybrid features in general, such as free/busy, MailTips, or migration endpoints. Additionally, this section includes the `Organization Configuration Transfer` feature.

#### Oauth, Intra Organization Connector and Organization Relationship

Selecting this option configures (or re-configures) `Intra-Organization Connectors`, `Organization Relationships` and creates the `OAuth trust` between Exchange Server on-premises and Exchange Online. These configurations are needed for free/busy sharing, MailTips, Online Archiving and more.

Important

Make sure that the OAuth certificate, which is used by Exchange Server on-premises, is valid before running this configuration. You can find more information about the required steps in the [Maintain the Exchange Server OAuth certificate](plan-and-deploy/integration-with-sharepoint-and-skype/maintain-oauth-certificate) documentation.

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-OrganizationRelationship
    [-Name 'On-premises to O365 - <guid>']
    [-TargetApplicationUri $null]
    [-TargetAutodiscoverEpr $null]
    [-Enabled $true]
    [-DomainNames <domain>.mail.onmicrosoft.com]
```

```powershell
New-OrganizationRelationship
    [-Name 'O365 to On-premises - <guid>']
    [-TargetApplicationUri $null]
    [-TargetAutodiscoverEpr $null]
    [-Enabled $true]
    [-DomainNames <OnPremisesEntryPointDomain>]
```

```powershell
Set-OrganizationRelationship
    [-Identity 'On-premises to O365 - <guid>']
    [-MailboxMoveEnabled $true]
    [-FreeBusyAccessEnabled $true]
    [-FreeBusyAccessLevel LimitedDetails]
    [-ArchiveAccessEnabled $true]
    [-MailTipsAccessEnabled $true]
    [-MailTipsAccessLevel All]
    [-DeliveryReportEnabled $true]
    [-PhotosEnabled $true]
    [-TargetOwaURL 'https://outlook.office.com/mail']
```

```powershell
Set-OrganizationRelationship
    [-Identity 'O365 to On-premises - <guid>']
    [-FreeBusyAccessEnabled $true]
    [-FreeBusyAccessLevel LimitedDetails]
    [-TargetSharingEpr $null]    
    [-MailTipsAccessEnabled $true]
    [-MailTipsAccessLevel All]
    [-DeliveryReportEnabled $true]
    [-PhotosEnabled $true]
    [-TargetOwaURL $null]
```

```powershell
New-IntraOrganizationConnector or Set-IntraOrganizationConnector
    [-Name 'HybridIOC - <guid>']
    [-DiscoveryEndpoint 'https://autodiscover-s.outlook.com/autodiscover/autodiscover.svc']
    [-TargetAddressDomains <domain>.mail.onmicrosoft.com]
    [-Enabled $true]
```

```powershell
New-IntraOrganizationConnector or Set-IntraOrganizationConnector
    [-Name 'HybridIOC - <guid>']
    [-DiscoveryEndpoint 'https://<OnPremisesEntryPointDomain>/autodiscover/autodiscover.svc']
    [-TargetAddressDomains <OnPremisesEntryPointDomain>]
    [-Enabled $true]
```

```powershell
Set-PartnerApplication
    [-Identity 'Exchange Online']
    [-Enabled $true]
```

```powershell
New-AuthServer or Set-AuthServer
    [-Name 'ACS - <guid>']
    [-AuthMetadataUrl 'https://accounts.accesscontrol.windows.net/<guid>/metadata/json/1']
    [-DomainName '<AcceptedDomains>','<domain>.mail.onmicrosoft.com']
```

```powershell
New-AuthServer or Set-AuthServer
    [-Name 'EvoSts - <guid>']
    [-AuthMetadataUrl 'https://login.windows.net/<domain>.onmicrosoft.com/federationmetadata/2007-06/federationmetadata.xml']
    [-Type AzureAD]
```

```powershell
Add-AvailabilityAddressSpace
    [-ForestName <domain>.mail.onmicrosoft.com]
    [-AccessMethod InternalProxy]
    [-UseServiceAccount $true]
    [-ProxyUrl <OnPremisesEwsUrl>]
```

#### Deploy dedicated Exchange hybrid app

Selecting this option registers a [dedicated Exchange Hybrid application](hybrid-deployment/deploy-dedicated-hybrid-app) in Microsoft Entra ID. This application replaces the legacy shared (first-party) service principal previously used for hybrid communication between on-premises Exchange and Exchange Online. When selected, the Hybrid Configuration wizard (HCW) creates a tenant-specific enterprise application in Microsoft Entra ID and configures OAuth-based trust to enable hybrid features such as:

- Free/Busy lookups
- MailTips
- Profile photo sharing

By selecting this option, the following actions are performed using Microsoft Graph API:

- Register a new application in Entra ID named `ExchangeServerApp-{Guid of the organization}`
- Add the `full_access_as_app` EWS API permission (to be replaced with a Graph API permission in the future)
- Grant tenant-wide admin consent
    - Requires confirmation during HCW runtime
- Upload the current Auth Certificate to the application
- Upload the next Auth Certificate (if available)
- Remove any expired certificates from the application

Caution

The Hybrid Configuration wizard requires tenant-wide admin consent. This consent is essential for the feature to function properly. If you don't grant or later revoke this consent, hybrid features such as Free/Busy, MailTips, and profile photo sharing stop working.

Once configured, the Hybrid Configuration wizard doesn't automatically enable the feature for your on-premises Exchange Server organization. HCW only creates the application in Microsoft Entra ID and prepares the Exchange Server configuration. To enable the feature, run the [New-SettingOverride](/en-us/powershell/module/exchangepowershell/new-settingoverride) cmdlet. Before doing so, ensure all Exchange servers are running a [version that supports this feature](hybrid-deployment/deploy-dedicated-hybrid-app#before-you-begin). Run the following command from an elevated Exchange Management Shell (EMS):

```powershell
New-SettingOverride -Name "EnableExchangeHybrid3PAppFeature" -Component "Global" -Section "ExchangeOnpremAsThirdPartyAppId" -Parameters @("Enabled=true") -Reason "Enable dedicated Exchange hybrid app feature"
Get-ExchangeDiagnosticInfo -Process Microsoft.Exchange.Directory.TopologyService -Component VariantConfiguration -Argument Refresh
```

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-AuthServer or Set-AuthServer
    [-Name 'EvoSts - <guid>']
    [-AuthMetadataUrl 'https://login.windows.net/<domain>.onmicrosoft.com/federationmetadata/2007-06/federationmetadata.xml']
    [-Type AzureAD]
    [-DomainName <Default Accepted Domain>, <domain>.mail.onmicrosoft.com]
    [-ApplicationIdentifier <dedicated Exchange hybrid app ID>]
```

#### Update Coexistence Domain in Exchange Server Accepted domain and Email Address Policy

Selecting this option adds Exchange Online co-existence domain (`<domain>.mail.onmicrosoft.com`) as accepted domain to Exchange Server on-premises for hybrid mail flow and AutoDiscover requests. The coexistence domain is used for secondary email addresses (also known as proxy addresses) in any email address policies that contain the domains you specified in the Hybrid Configuration wizard.

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-RemoteDomain or Set-RemoteDomain
    [-Name 'Hybrid Domain - <domain>.mail.onmicrosoft.com']
    [-DomainName <domain>.mail.onmicrosoft.com]
    [-TargetDeliveryDomain $true]
```

```powershell
New-RemoteDomain or Set-RemoteDomain
    [-Name 'Hybrid Domain - <domain>.onmicrosoft.com']
    [-DomainName <domain>.onmicrosoft.com]
    [-TrustedMailInboundEnabled $true]
```

```powershell
New-AcceptedDomain or Set-AcceptedDomain
    [-Name <domain>.mail.onmicrosoft.com]
    [-DomainName <domain>.mail.onmicrosoft.com]
```

```powershell
Set-EmailAddressPolicy
    [-Identity 'Default Policy']
    [-ForceUpgrade $true]
    [-EnabledEmailAddressTemplates 'smtp:@<domain>.onmicrosoft.com','smtp:@<AdditionalAcceptedDomains>','SMTP:@<DefaultAcceptedDomain>','smtp:%m@<domain>.mail.onmicrosoft.com']
```

#### Migration Endpoint

Selecting this option creates a migration endpoint in the Exchange Online tenant. The migration endpoint is needed to move (migrate) mailboxes from Exchange Server on-premises to Exchange Online.

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-MigrationEndpoint or Set-MigrationEndpoint
    [-Name 'Hybrid Migration Endpoint - EWS (Default Web Site)']
    [-ExchangeRemoteMove $true]
    [-RemoteServer <OnPremisesEntryPointDomain>]
    [-Credentials (Get-Credential -UserName <ADDomain>\<Username>)]
```

#### Organization Configuration Transfer

Selecting this option copies the organization policy objects and values from Exchange Server on-premises to Exchange Online.

See [Organization configuration transfer attributes](org-config-transfer-attributes/org-config-transfer-attributes) for a list of attributes that are copied from an on-premises Exchange organization to Exchange Online.

### Configure Mail Flow

The `Configure Mail Flow` section provides settings that can be used to configure hybrid mail flow related features, such as connectors in Microsoft 365 and Exchange Server on-premises, and Centralized Mail Transport. It also includes a configuration action that can be used to replace the certificate used to secure the email flow between Exchange Server on-premises and Exchange Online.

#### Outbound Connector in M365 Organization

Selecting this option configures either a new or modifies an existing `Outbound Connector` in Microsoft 365 organization.

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-OutboundConnector or Set-OutboundConnector
    [-Name 'Outbound to <guid>']
    [-RecipientDomains <RecipientDomains>]
    [-SmartHosts <OnPremisesSmartHost>]
    [-ConnectorSource HybridWizard]
    [-ConnectorType OnPremises]
    [-TLSSettings DomainValidation]
    [-TLSDomain <TLSCertificateDomain>]
    [-CloudServicesMailEnabled $true]
    [-RouteAllMessagesViaOnPremises $false]
    [-UseMxRecord $false]
    [-IsTransportRuleScoped $false]
```

#### Inbound Connector in M365 Organization

Selecting this option configures either a new or modifies an existing `Inbound Connector` within the Microsoft 365 organization.

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-InboundConnector or Set-InboundConnector
    [-Name 'Inbound from <guid>']
    [-CloudServicesMailEnabled $true]
    [-ConnectorSource HybridWizard]
    [-ConnectorType OnPremises]
    [-RequireTLS $true]
    [-SenderDomains '']
    [-SenderIPAddresses $null]
    [-RestrictDomainsToIPAddresses $false]
    [-TLSSenderCertificateName <TLSCertificateDomain>]
    [-AssociatedAcceptedDomains $null]
```

#### Receive Connector on Exchange Hybrid Server

Selecting this option configures either a new and or modifies an existing `Receive Connector` in Exchange Server on-premises organization.

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-ReceiveConnector or Set-ReceiveConnector
    [-Identity '<ServerName>\Default Frontend <ServerName>']
    [-AuthMechanism 'Tls, Integrated, BasicAuth, BasicAuthRequireTLS, ExchangeServer']
    [-Bindings '[::]:25','0.0.0.0:25']
    [-Fqdn <ServerFqdn>]
    [-PermissionGroups 'AnonymousUsers, ExchangeServers, ExchangeLegacyServers']
    [-RemoteIPRanges '::-ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff','0.0.0.0-255.255.255.255']
    [-RequireTLS $false]
    [-TLSDomainCapabilities mail.protection.outlook.com:AcceptCloudServicesMail]
    [-TLSCertificateName '<I>X.500Issuer<S>X.500Subject']
    [-TransportRole FrontendTransport]
```

#### Send Connector on Exchange Hybrid Server

Selecting this option configures either a new or modifies an existing `Send Connector` in Exchange Server on-premises organization.

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-SendConnector or Set-SendConnector
    [-Name 'Outbound to Office 365 - <guid>']
    [-AddressSpaces 'smtp:<domain>.mail.onmicrosoft.com;1']
    [-DNSRoutingEnabled $true]
    [-ErrorPolicies Default]
    [-Fqdn <OnPremisesEntryPointDomain>]
    [-RequireTLS $true]
    [-IgnoreSTARTTLS $false]
    [-SourceTransportServers <TransportServers>]
    [-SmartHosts $null]
    [-TLSAuthLevel DomainValidation]
    [-DomainSecureEnabled $false]
    [-TLSDomain mail.protection.outlook.com]
    [-CloudServicesMailEnabled $true]
    [-TLSCertificateName '<I>X.500Issuer<S>X.500Subject']
```

#### Enable Centralized Mail Transport

Selecting this option routes outbound messages, sent from your Exchange Online organization through your Exchange Server on-premises organization. In Centralized Mail Transport (CMT) configurations, actual changes are done in Inbound and Outbound Connectors. Hence whenever CMT is selected, the Inbound and Outbound Connectors are automatically selected. Deselecting an Inbound or Outbound Connector does automatically deselect the `Enable Centralized Mail Transport` option.

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
New-InboundConnector or Set-InboundConnector
    [-Name 'Inbound from <guid>']
    [-CloudServicesMailEnabled $true]
    [-ConnectorSource HybridWizard]
    [-ConnectorType OnPremises]
    [-RequireTLS $true]
    [-SenderDomains '']
    [-SenderIPAddresses $null]
    [-RestrictDomainsToIPAddresses $false]
    [-TLSSenderCertificateName <TLSCertificateDomain>]
    [-AssociatedAcceptedDomains $null]
```

```powershell
New-OutboundConnector or Set-OutboundConnector
    [-Name 'Outbound to <guid>']
    [-RecipientDomains '*']
    [-SmartHosts <OnPremisesSmartHost>]
    [-ConnectorSource HybridWizard]
    [-ConnectorType OnPremises]
    [-TLSSettings DomainValidation]
    [-TLSDomain <TLSCertificateDomain>]
    [-CloudServicesMailEnabled $true]
    [-RouteAllMessagesViaOnPremises $true]
    [-UseMxRecord $false]
    [-IsTransportRuleScoped $false]
```

#### Update Secure Mail Certificate for connectors

Tip

The `Update Secure Mail Certificate for connectors` configuration is a new option, which was introduced to simplify the recurring transport certificate renewal process in hybrid scenarios.

If you only need to update the TLS certificate used by all four connectors while keeping other connector configurations the same, select this option.

When selecting this option, you don't need to select any other connector configuration, if you want to preserve the existing connector configuration. If any other connector configuration option was also selected, along with the TLS certificate update, other configuration changes occur for the connector.

If this option is selected, HCW executes the specified cmdlets and parameters:

Show cmdlets

```powershell
Set-InboundConnector
    [-Name 'Inbound from <guid>']
    [-TLSSenderCertificateName <TLSCertificateDomain>]
```

```powershell
Set-OutboundConnector
    [-Name 'Outbound to <guid>']
    [-TLSDomain <TLSCertificateDomain>]
```

```powershell
Set-ReceiveConnector
    [-Identity '<ServerName>\Default Frontend <ServerName>']
    [-TLSCertificateName '<I>X.500Issuer<S>X.500Subject']
```

```powershell
Set-SendConnector
    [-Name 'Outbound to Office 365 - <guid>']
    [-TLSCertificateName '<I>X.500Issuer<S>X.500Subject']
```

## How to use the new "Choose Exchange Hybrid Configuration" feature

In the latest version of HCW, administrators can use the `Choose Exchange Hybrid Configuration` feature as follows:

1. On the `Hybrid Topology` page, based on the topology that you want to configure, you can select between `Classic Hybrid` and `Modern Hybrid`. This page is also the point at which you can decide whether you want to use the new `Choose Exchange Hybrid Configuration` feature or not. If you want to update only specific hybrid configurations without altering any other configurations, select `Choose Exchange Hybrid Configuration` and click `Next`.

[![A screenshot that shows the first page of the Hybrid Configuration wizard with the new 'Choose Exchange Hybrid Configuration' option](exchangehybrid/media/hcw-custom-config-1.png)](exchangehybrid/media/hcw-custom-config-1.png#lightbox)
2. If `Choose Exchange Hybrid Configuration` was selected, a new `Choose what HCW configures` section is shown on which administrators can select from the following hybrid configurations. You can find a description of each configuration in the Granular configuration options section of this article.

[![A screenshot that shows the new 'Choose Exchange Hybrid Configuration' selection.](exchangehybrid/media/hcw-custom-config-2.png)](exchangehybrid/media/hcw-custom-config-2.png#lightbox)

    Note

    If you've selected `Minimal Hybrid Configuration` on the previous page, the `Choose what HCW configures` section isn't shown. This is because `Choose Exchange Hybrid Configuration` is not supported in this scenario.

    Based on your selection, the required configuration sections will be shown after clicking on `Next`. If, for example, only `Organization Configuration Transfer` was selected, HCW will only show the OCT configuration page in the next step.

    Administrators shouldn't change the default hybrid configuration by deselecting existing configuration, unless it's an HCW rerun and the intention is, to preserve existing hybrid configurations, which would have been modified after last run. If, by mistake, some options were selected or deselected, click on the `Reset Choices` button to revert the selection back to the preselected default.

    You can always come back to the `Choose what HCW configures` overview and make adjustments to the selection. That is possible until you clicked on `Update` on the last page.
3. Click on `Next` and continue with the configuration as usual (for example, selecting the transport certificate).
4. If you select the `Deploy dedicated Exchange hybrid app` option, HCW will prompt you with the `Exchange Server Application Configuration` dialog. To proceed successfully, ensure the `Grant Administrator Consent` checkbox is selected - this step is required to configure the dedicated Exchange Hybrid application.

[![A screenshot that shows the new 'Exchange Server Application Configuration' dialog for a new dedicated Exchange hybrid app.](exchangehybrid/media/hcw-custom-config-8.png)](exchangehybrid/media/hcw-custom-config-8.png#lightbox)

    If HCW detects an existing dedicated Exchange Hybrid application, it displays the application's name and ID. The dialog also shows the current administrator consent status for the `full_access_as_app` EWS API permission. If consent has already been granted (checkbox is selected) and you deselect it, the consent will be revoked - potentially breaking your existing configuration and impacting hybrid features such as Free/Busy, MailTips, and profile photo sharing.

[![A screenshot that shows the new 'Exchange Server Application Configuration' dialog for an existing dedicated Exchange hybrid app.](exchangehybrid/media/hcw-custom-config-9.png)](exchangehybrid/media/hcw-custom-config-9.png#lightbox)
5. Once you've click on `Update`, HCW performs the selected actions. On the final page, it shows you all the hybrid configurations that were excluded via `Choose Exchange Hybrid Configuration` feature.

[![A screenshot that shows final page that is shown after HCW has processed the changes. It shows the excluded hybrid configuration steps.](exchangehybrid/media/hcw-custom-config-7.png)](exchangehybrid/media/hcw-custom-config-7.png#lightbox)

## Other changes made to the HCW

With the introduction of the `Deploy dedicated Exchange hybrid app` feature, the default configuration behavior has changed. Unless the `Choose Exchange Hybrid Configuration` option is selected and the Deploy dedicated Exchange hybrid app checkbox is explicitly cleared, the Hybrid Configuration wizard configures the [dedicated Exchange hybrid app](hybrid-deployment/deploy-dedicated-hybrid-app) by default.

[![A screenshot that shows the new 'Exchange Server Application Configuration' dialog for a new dedicated Exchange hybrid app.](exchangehybrid/media/hcw-custom-config-8.png)](exchangehybrid/media/hcw-custom-config-8.png#lightbox)

With the introduction of the `Choose Exchange Hybrid Configuration` feature, we made several other adjustments to the Hybrid Configuration wizard to comply with the new feature.

Centralized Mail Transport (CMT) configuration is moved to the `Choose what HCW configures` page:

**Old experience:**

[![A screenshot that shows the old Centralized Mail Transport configuration option.](exchangehybrid/media/hcw-custom-config-3.png)](exchangehybrid/media/hcw-custom-config-3.png#lightbox)

**New experience:**

[![A screenshot that shows the new Centralized Mail Transport configuration experience.](exchangehybrid/media/hcw-custom-config-4.png)](exchangehybrid/media/hcw-custom-config-4.png#lightbox)

On the `Hybrid Features` page, the option to select `Organization Config Transfer` was removed for `Full Hybrid Configuration`. This option can now be accessed via the `Choose what HCW configures` page:

**Old experience:**

[![A screenshot that shows the old Organization Config Transfer configuration option.](exchangehybrid/media/hcw-custom-config-5.png)](exchangehybrid/media/hcw-custom-config-5.png#lightbox)

**New experience:**

[![A screenshot that shows the new Organization Config Transfer configuration experience.](exchangehybrid/media/hcw-custom-config-6.png)](exchangehybrid/media/hcw-custom-config-6.png#lightbox)

## Frequently Asked Questions

This section discusses various questions that can come up while using this new feature.

**❓ Should I use the `Choose Exchange Hybrid Configuration` feature if I'm setting up Exchange Server Hybrid for the first time?**
That isn't needed unless you also want to perform `Organization Configuration Transfer` (OCT). If OCT is needed by you in your first HCW run, then select `Choose Exchange Hybrid Configuration`, and on the `Choose what HCW configures` page select `Organization Configuration Transfer` additionally to all the preselected configurations. 

**❓ We run HCW to configure Exchange Hybrid once already. We used the `Choose Exchange Hybrid Configuration` feature but forgot to select `Migration Endpoint` to be configured. What should we do now?**
It's no problem. You can rerun the HCW, deselect everything except `Migration Endpoint` and finish the run. HCW configures the migration endpoint for you without updating anything else. 

**❓ We run HCW to configure Exchange Hybrid once already. Today, we only need to update TLS certificate for all connectors. How should we do that?**
Rerun the HCW, select `Choose Exchange Hybrid Configuration` and on the `Choose what HCW configures` page deselect everything except `Update Secure Mail Certificate for connectors`. 

**❓ We run HCW to configure Exchange Hybrid once already. Today, we only need to perform an `Organization Configuration Transfer`. How should we do that?**
Rerun the HCW, select `Choose Exchange Hybrid Configuration` and on the `Choose what HCW configures` page deselect everything except `Organization Configuration Transfer`. 

**❓ We're currently using `Modern Hybrid` but want to switch to `Classic Hybrid`. We don't want to change anything related to mail flow, which is working properly. How can we do that?**
Rerun the HCW and select `Classic Hybrid Topology`. On the `Choose Exchange Hybrid Configuration` page, at least select, `Oauth, Intra Organization Connector and Organization Relationship` and `Migration Endpoint` configuration. 

**❓ We run HCW to configure Exchange Hybrid once already. After Exchange Server hybrid setup, we made many changes on either of the four connectors. We want to rerun HCW and update some other hybrid configurations but don't want to change anything related to mail flow, which is working properly. How can we do that?**
Rerun the HCW, select `Choose Exchange Hybrid Configuration` and on the `Choose what HCW configures` page don't select the following four configurations: `Outbound Connector`, `Inbound Connector`, `Receive Connector` and `Send Connector`. 

**❓ We have many accepted domains in our organization and during a HCW rerun, HCW tries to create Service Principal Name (SPN) sets for each of the Accepted Domain. We hit a limit in Entra ID but are unsure what the limit is. The HCW log file contains the following exception: `[Directory_ResourceSizeExceeded] The size of the object has exceeded its limit. Please reduce the number of values and retry your request.` What is the limit and how can we avoid it?**
We don't have a specified limit for the number of SPNs that can be added, as it depends on how these values are stored. However, there is a limitation on the total number of entries an attribute can contain. This limit is considered a practical limit, meaning the size of each individual entry affects the overall limit. Our tests indicate that it's likely to reach this limit if more than 800 SPNs are added. Keep in mind that this is a practical limit, so you might reach it with fewer or more than 800 SPNs.To workaround this, rerun the HCW, select `Choose Exchange Hybrid Configuration` and on the `Choose what HCW configures` page don't select the following configurations: `Oauth, Intra Organization Connector and Organization Relationship`. Deselecting this option prevents HCW from creating SPNs for all accepted domains.