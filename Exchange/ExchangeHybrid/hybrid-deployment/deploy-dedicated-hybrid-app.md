---
layout: Conceptual
title: Deploy dedicated Exchange hybrid app | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/deploy-dedicated-hybrid-app
Manager: anaruxa
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.topic: article
author: lusassl-msft
ms.author: lusassl
description: Admins can learn about how to configure the dedicated Exchange hybrid application.
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
ms.date: 2026-04-17T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f0c3fa29-7e03-5659-283d-fd9fbc3cfa45
document_version_independent_id: 533b5944-bd54-100a-fc06-cb68baa6cb24
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/deploy-dedicated-hybrid-app.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/deploy-dedicated-hybrid-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/deploy-dedicated-hybrid-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 84feb238-0b05-aaef-47c1-f4ed35bced1f
---

# Deploy dedicated Exchange hybrid app | Microsoft Learn

## Overview

Exchange hybrid features like [Free/Busy, MailTips, and Photos](/en-us/powershell/module/exchangepowershell/set-hybridconfiguration#-features) require a dedicated application in Entra ID for secure communication between Exchange Server and Exchange Online. This article explains how to create, configure, and manage the dedicated Exchange hybrid application.

Important

As of October 31, 2025, EWS access through the shared service principal is **permanently blocked**. Rich coexistence hybrid features (Free/Busy, MailTips, and profile picture sharing) no longer work through the legacy shared service principal workflow. All Exchange servers must run a supported build and use the dedicated Exchange hybrid application for these features to function. For more information, see the [Dedicated Hybrid App: temporary enforcements, new HCW and possible hybrid functionality disruptions](https://techcommunity.microsoft.com/blog/exchange/dedicated-hybrid-app-temporary-enforcements-new-hcw-and-possible-hybrid-function/4440682) blog post.

### Background: Why this change was made

Previously, Exchange Server used a shared [Service Principal](/en-us/entra/identity-platform/app-objects-and-service-principals#service-principal-object) with Exchange Online for secure communication, and the [Hybrid Configuration wizard (HCW)](../hybrid-configuration-wizard) uploaded the current [Auth Certificate](../plan-and-deploy/integration-with-sharepoint-and-skype/maintain-oauth-certificate) to the shared Service Principal to enable this process. Because of the [retirement of Exchange Web Services in Exchange Online](https://techcommunity.microsoft.com/blog/exchange/retirement-of-exchange-web-services-in-exchange-online/3924440) and the [removal of EWS dependencies from first-party apps and services](https://techcommunity.microsoft.com/blog/exchange/security-related-updates-in-exchange-online/4303525), Exchange Server now uses a dedicated application in Entra ID for hybrid scenarios instead of the shared Service Principal.

This dedicated application is used exclusively by Exchange Server for hybrid communication and has no dependencies on the shared Service Principal. By default, it's configured with EWS API permissions. Starting with the May 2026 Hotfix Update, Graph API permissions can also be configured as a replacement for EWS API permissions in most hybrid scenarios. For details, see Configure Graph API permissions.

To learn more about this change and its implications, read the [Exchange Server Security Changes for Hybrid Deployments](https://aka.ms/ExchangeHybridSecurityChanges) blog post.

If you've already configured the dedicated Exchange hybrid app or previously had a hybrid configuration, we strongly recommend running the script in Service Principal Clean-Up Mode to remove any certificates that were uploaded to the first-party Service Principal's `keyCredentials` and not cleaned up.

## Before you begin

Before you configure the dedicated Exchange hybrid application, you must first set up either [Classic Full](../hybrid-configuration-wizard-options) or [Modern Full](../hybrid-configuration-wizard-options) hybrid by using the Hybrid Configuration wizard.

### Supported Exchange Server versions

The following Exchange Server builds support the dedicated Exchange hybrid application:

| Version | Build Number | EWS API workflow supported | Graph API workflow supported |
| --- | --- | --- | --- |
| Exchange Server SE RTM with May 2026 HU | 15.2.2562.41 | Yes | Yes |
| Exchange Server SE RTM | 15.2.2562.17 | Yes | No |
| Exchange Server 2019 CU15 with April 2025 HU | 15.2.1748.24 | Yes | No |
| Exchange Server 2019 CU14 with April 2025 HU | 15.2.1544.25 | Yes | No |
| Exchange Server 2016 CU23 with April 2025 HU | 15.1.2507.55 | Yes | No |

### Required permissions

The following table summarizes the permissions required for each task:

| Task | Least privileged roles | Higher privileged role |
| --- | --- | --- |
| Create the application in Entra ID | `Application Administrator` | `Global Administrator` |
| Configure Auth Server and enable feature in Exchange | `View-Only Configuration`**and**`Organization Client Access`**and**`Organization Configuration` | `Organization Management` |
| Clean up the shared service principal | — | `Global Administrator` |

For more details about Entra ID roles, see the [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference#all-roles) documentation. For Exchange Server roles, see the [Organization Management](../organization-management-exchange-2013-help) documentation.

Run the script on a server with the Mailbox role installed and a build that supports this feature to configure the Auth Server and create the [Setting Override](/en-us/powershell/module/exchangepowershell/new-settingoverride).

### Network connectivity requirements

The script uses the [Microsoft Graph API](/en-us/graph/use-the-api) to create and manage applications in Entra ID. The system running the script requires outbound connectivity to Graph API and Entra ID endpoints.

- In **All-in-one Configuration Mode**, the Exchange server running the script needs this outbound connectivity.
- In **Split Execution Configuration Mode**, the system used to create or manage the application in Entra ID needs this outbound connectivity (this system doesn't have to be an Exchange server).

Choose the endpoint that matches where your tenant resides, such as `Global`. For more information, see the [National Microsoft Entra ID Endpoints](/en-us/graph/deployments#app-registration-and-token-service-root-endpoints) and [National Microsoft Graph Endpoints](/en-us/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints) documentation.

To verify connectivity to the Graph and Entra ID endpoints, use the [Test-NetConnection](/en-us/powershell/module/nettcpip/test-netconnection) cmdlet. This example validates the connection using the `Global` endpoints:

```powershell
Test-NetConnection -ComputerName login.microsoftonline.com -Port 443
Test-NetConnection -ComputerName graph.microsoft.com -Port 443
```

If you plan to use the Graph API-based hybrid flow, ensure that your Exchange servers have outbound connectivity to the [Graph API endpoint](/en-us/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints).

## Configure the dedicated Exchange hybrid application

Microsoft provides the [`ConfigureExchangeHybridApplication.ps1`](https://aka.ms/ConfigureExchangeHybridApplication) script to configure the dedicated Exchange hybrid application. Detailed documentation for the script and its parameters is available in the [ConfigureExchangeHybridApplication.ps1 script documentation](https://aka.ms/ConfigureExchangeHybridApplication).

Choose the configuration path that matches your environment:

| Your scenario | Configuration path |
| --- | --- |
| Mailbox server has internet access and you have Entra ID permissions | All-in-one mode (recommended) |
| Mailbox server lacks internet access or you need to separate Entra ID and Exchange tasks | Split execution mode |
| You already used HCW to create the app | Enable the feature after using HCW. To add Graph API permissions, run the script after HCW completes. |

If your on-premises organization has hybrid relationships with [multiple tenants (1:N)](https://techcommunity.microsoft.com/blog/exchange/september-2020-hybrid-configuration-wizard-update/1687698), run the script once for each tenant using an account from that tenant. If you plan to switch to the Graph API-based workflow, prepare the dedicated Exchange hybrid application in each tenant before you enable the Graph API-based workflow via the Setting Override. Enabling the workflow before the Graph API permissions are granted and consented in each tenant causes hybrid features to stop working for tenants without the properly configured Graph API permissions.

Depending on the size of your organization, it might take up to 60 minutes for the dedicated Exchange hybrid application configuration to be recognized by the responsible Exchange Server processes. During this time, features such as Free/Busy, MailTips, and Photos might be temporarily unavailable.

The latest version of the [Hybrid Configuration wizard (HCW)](https://aka.ms/HybridWizard) also supports configuring the dedicated Exchange Hybrid application with EWS API permissions. However, HCW doesn't enable the feature automatically. If you used HCW, follow the steps in Enable the feature after using HCW to activate it. HCW also doesn't automatically clean up certificates previously uploaded to the first-party service principal's `keyCredentials`. To perform this clean-up and mitigate [CVE-2025-53786](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-53786), run the script in Service Principal Clean-Up Mode.

### All-in-one configuration mode

For most customers, the All-in-one Configuration Mode is the recommended way to configure this feature. Run the script on a Mailbox server with outbound connectivity as described in the Network connectivity requirements section. The server must run an Exchange Server build that supports this feature.

Important

The All-in-one Configuration Mode isn't compatible with Windows Server Core. If you're using Windows Server Core, follow the instructions in the Split execution configuration mode section.

Run the following command:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -FullyConfigureExchangeHybridApplication
```

By default, the script runs against the `Microsoft 365 Worldwide` cloud. If your Microsoft 365 tenant is in a different cloud, use the `AzureEnvironment` parameter. In the following example, the application is created in the `Microsoft 365 operated by 21Vianet` cloud:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -FullyConfigureExchangeHybridApplication -AzureEnvironment "ChinaCloud"
```

The script performs all the necessary steps: creating the application in Entra ID, configuring the Auth Server, and enabling the feature via Setting Override. During execution, the script asks whether you want to configure Graph API permissions in addition to the EWS API permissions. If you choose to configure Graph API permissions, the script also enables the Graph API-based hybrid flow via a Setting Override after an additional confirmation.

If you want to create the dedicated Exchange hybrid application without EWS API permissions, use the `UseGraphApiOnly` parameter:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -FullyConfigureExchangeHybridApplication -UseGraphApiOnly
```

### Split execution configuration mode

Use this mode if your Mailbox server doesn't have outbound connectivity to Microsoft Graph or Entra ID, or if the Exchange Server administrator doesn't have sufficient permissions to create and configure the application in Entra ID.

If you perform any of the steps on a non-Exchange Server, ensure that the computer is joined to the same forest where your Exchange organization resides.

#### Step 1: Export the Auth Certificate

Export the Auth Certificate (and, if available, the next Auth Certificate) with its public key. Don't export the private key of the certificate. Run the following script from an elevated Exchange Management Shell (EMS):

In this example, the certificate is exported to `C:\AuthCertExport`. To export to a different location, modify the `$exportFilePath` variable.

```powershell
# Change the path if you want to export the certificates to a different location
$exportFilePath = "C:\AuthCertExport"

$authConfig = Get-AuthConfig

New-Item -Type Directory -Path C:\AuthCertExport -Force | Out-Null

if (-not([System.String]::IsNullOrEmpty($authConfig.CurrentCertificateThumbprint))) {
    $thumbprint = $authConfig.CurrentCertificateThumbprint
    Write-Host "[+] Auth Certificate thumbprint: $thumbprint"

    try {
        $currentAuthCertificate = Get-ChildItem -Path Cert:\LocalMachine\My\$thumbprint
        Export-Certificate -Cert $currentAuthCertificate -FilePath "$exportFilePath\$thumbprint.cer" -Type CERT | Out-Null
        Write-Host "[+] Certificate was successfully exported to: $exportFilePath"
    } catch {
        Write-Host "[+] We hit the following exception: $_" -ForegroundColor Red
    }
}

if (-not([System.String]::IsNullOrEmpty($authConfig.NextCertificateThumbprint))) {
    $thumbprint = $authConfig.NextCertificateThumbprint
    Write-Host "[+] Next Auth Certificate thumbprint: $thumbprint"

    try {
        $currentAuthCertificate = Get-ChildItem -Path Cert:\LocalMachine\My\$thumbprint
        Export-Certificate -Cert $currentAuthCertificate -FilePath "$exportFilePath\$thumbprint.cer" -Type CERT | Out-Null
        Write-Host "[+] Certificate was successfully exported to: $exportFilePath"
    } catch {
        Write-Host "[+] We hit the following exception: $_" -ForegroundColor Red
    }
}
```

#### Step 2: Create the application in Entra ID

Copy the exported certificates to a machine with outbound connectivity as described in the Network connectivity requirements section. Run the script on that machine to create the application in Entra ID. The script displays your `Tenant ID` and the `appId` of the newly created application. Note both values because you need them in a later step.

```powershell
.\ConfigureExchangeHybridApplication.ps1 -CreateApplication -UpdateCertificate -CertificateMethod "File" -CertificateInformation "C:\Certificates\CurrentAuthCertificate.cer"
```

To configure the application with Graph API permissions only, use the `UseGraphApiOnly` parameter:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -CreateApplication -UseGraphApiOnly -UpdateCertificate -CertificateMethod "File" -CertificateInformation "C:\Certificates\CurrentAuthCertificate.cer"
```

If multiple Auth Certificates were exported in step 1, run the script again to upload the additional certificate. The `CreateApplication` step isn't required for the second run:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -UpdateCertificate -CertificateMethod "File" -CertificateInformation "C:\Certificates\NewNextAuthCertificate.cer"
```

#### Step 3: Configure Exchange Server

Run this step on a Mailbox server. The script configures the Auth Server, updates existing organization relationships between Exchange Server and Exchange Online, and enables the dedicated Exchange hybrid application feature. Provide the ID of your tenant, the `appId` of the newly created application in Entra ID, and the remote routing domain:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -ConfigureAuthServer -ConfigureTargetSharingEpr -EnableExchangeHybridApplicationOverride -CustomAppId "<appId>" -TenantId "<tenantId>" -RemoteRoutingDomain "<organization>.mail.onmicrosoft.com"
```

### Enable the feature after using HCW

If you used the [Hybrid Configuration wizard (HCW)](https://aka.ms/HybridWizard) to configure the dedicated Exchange Hybrid application, you must run the [New-SettingOverride](/en-us/powershell/module/exchangepowershell/new-settingoverride) cmdlet to enable the feature for your on-premises Exchange Server organization. Execute the following command from an elevated Exchange Management Shell (EMS):

```powershell
New-SettingOverride -Name "EnableExchangeHybrid3PAppFeature" -Component "Global" -Section "ExchangeOnpremAsThirdPartyAppId" -Parameters @("Enabled=true") -Reason "Enable dedicated Exchange hybrid app feature"
Get-ExchangeDiagnosticInfo -Process Microsoft.Exchange.Directory.TopologyService -Component VariantConfiguration -Argument Refresh
```

## Configure Graph API permissions

Starting with the May 2026 Hotfix Update, Exchange Server supports the Graph API-based hybrid flow for most scenarios. Microsoft has updated the [`ConfigureExchangeHybridApplication.ps1`](https://aka.ms/ConfigureExchangeHybridApplication) script to configure Graph API permissions on newly created and existing applications and to enable the Graph API-based hybrid flow via a Setting Override.

Microsoft is rolling out support for the Graph API-based hybrid flow across clouds in phases. The following table lists the current availability. This article is updated as support expands to additional clouds.

| Cloud | Graph API-based hybrid flow supported |
| --- | --- |
| Microsoft 365 Global | Yes |
| Microsoft 365 operated by 21Vianet | No |
| Microsoft 365 US Government L4 (GCC High) | No |
| Microsoft 365 US Government L5 (DOD) | No |
| Bleu | No |
| Delos Cloud | No |

Important

Don't enable the Graph API-based hybrid flow in a cloud where it isn't yet supported. Enabling it before support is available causes hybrid features such as Free/Busy, MailTips, and profile picture sharing to stop working.

### Supported scenarios

The following table shows which hybrid features each API supports:

| Feature | Supported via EWS API | Supported via Graph API |
| --- | --- | --- |
| Free/Busy | Yes | Yes |
| MailTips | Yes | Partial (Automatic Replies only) |
| Profile Pictures | Yes | Yes |
| Move to Archive(Archive Mailbox in cloud) | Yes | No |

Important

After you enabled the Graph API-based hybrid flow, Exchange Server uses EWS for hybrid features which aren't yet supported with Graph API. Don't remove the EWS API permissions from the application in Entra ID if you rely on any scenario that isn't yet supported with Graph API. If you don't use the features that aren't yet supported with Graph API, you can remove the `full_access_as_app` EWS API permission by using the script in Remove API permissions mode.

Microsoft is actively working to expand Graph API support for additional scenarios. This documentation is updated as new scenarios become supported. Exchange Server continues to use EWS for any scenario that isn't yet supported with Graph API, even if the Graph API-based hybrid flow is enabled.

### Enable Graph API-based hybrid flow

During All-in-one Configuration Mode, the script prompts you to configure Graph API permissions. If you already configured the application and want to add Graph API permissions later, rerun the script:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -FullyConfigureExchangeHybridApplication
```

For split execution mode, use the `UseGraphApiOnly` parameter as described in Split execution configuration mode.

### Remove EWS API permissions

If you don't use any features that require EWS API and want to use only Graph API permissions, run the script to remove the `full_access_as_app` EWS API permission:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -RemoveApiPermissions "EWS"
```

This command can be executed on a non-Exchange server.

## Verify the configuration

To confirm that OAuth authentication works correctly between Exchange Server and Exchange Online, use the [Test-OAuthConnectivity](/en-us/powershell/module/exchangepowershell/test-oauthconnectivity) cmdlet from Exchange Management Shell on your on-premises Exchange Server.

If the `ResultType` is `Success` and the `Detail` section includes the `appId` of your dedicated Exchange hybrid application, Exchange Server successfully acquired an OAuth token. The OAuth request is initiated by the server where the Exchange Management Shell (EMS) session is running. If the mailbox specified via the `-Mailbox` parameter resides on a different server that doesn't support the dedicated Exchange hybrid app, but the EMS host server does, the `ResultType` still shows `Success`. This behavior is by design.

Run the following command (replace the email address with an on-premises mailbox in your environment):

```powershell
$OnPremisesMailbox = "userMailboxOnprem@contoso.com"

$result = Test-OAuthConnectivity -Service EWS -TargetUri https://outlook.office365.com -Mailbox $OnPremisesMailbox
Write-Host $result.ResultType
if (($result.Detail.FullId) -match 'L:(?<guid>[0-9a-fA-F-]{36})-AS:') {
    $appid = $matches['guid']
    Write-Output "Extracted appId: $appid"
} else {
    Write-Output "appId not found"
}
```

## Manage the application

This section covers common management tasks for the dedicated Exchange hybrid application after initial configuration.

### Update the Auth Certificate

Use the following steps when the Auth Certificate expires or is replaced. These steps aren't required during initial configuration. For more information about maintaining the Auth Certificate, see the [Maintain the Exchange Server OAuth certificate](../plan-and-deploy/integration-with-sharepoint-and-skype/maintain-oauth-certificate) documentation.

If your Mailbox server has outbound connectivity as described in the Network connectivity requirements section, run:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -UpdateCertificate
```

If your Mailbox server doesn't have outbound connectivity, export the new Auth Certificate by following the steps in Step 1: Export the Auth Certificate. Copy the certificate to a machine with outbound connectivity, then run:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -UpdateCertificate -CertificateMethod "File" -CertificateInformation "C:\Certificates\NewAuthCertificate.cer"
```

Tip

Use the [MonitorExchangeAuthCertificate](https://aka.ms/MonitorExchangeAuthCertificate) script to validate your OAuth certificate. If you need to update your OAuth certificate, follow the steps in the [Maintain the Exchange Server OAuth certificate](../plan-and-deploy/integration-with-sharepoint-and-skype/maintain-oauth-certificate) documentation.

### Clean up the shared service principal

After you enable the dedicated Exchange hybrid application feature and all your Exchange servers run an Exchange build that supports this feature, clean up the certificates that were previously uploaded to the first-party Service Principal. As part of the previous Exchange hybrid design, the HCW uploaded the Auth Certificate to the first-party Service Principal. **This practice is no longer recommended and shouldn't be performed.** The Auth Certificate must now be uploaded exclusively to the dedicated Exchange hybrid application.

The commands in this section can be executed on any computer with outbound internet connectivity. Exchange servers running builds older than those listed in the Supported Exchange Server versions section can't use rich coexistence hybrid features regardless of whether certificates exist on the shared service principal, because EWS access through the shared service principal has been permanently blocked since October 31, 2025. Update these servers to a supported build and configure the dedicated Exchange hybrid application to restore hybrid functionality.

Warning

If you run the HCW after configuring the dedicated Exchange hybrid application feature and select the [Oauth, Intra Organization Connector and Organization Relationship](../hybrid-configuration-wizard-choose-configuration-feature#oauth-intra-organization-connector-and-organization-relationship) configuration option, the Auth Certificate is uploaded to the first-party Service Principal again. It's strongly recommended to repeat the steps to purge the Auth Certificate from the first-party Service Principal in this case.

To purge all `keyCredentials` of the first-party Service Principal, run:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -ResetFirstPartyServicePrincipalKeyCredentials
```

To purge a specific certificate and all expired certificates from the `keyCredentials`, provide the thumbprint of the certificate to delete:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -ResetFirstPartyServicePrincipalKeyCredentials -CertificateInformation "1234567890ABCDEF1234567890ABCDEF12345678"
```

### Remove API permissions

To remove specific API permissions from the dedicated Exchange hybrid application in Entra ID, use the `RemoveApiPermissions` parameter. This command can be executed on a non-Exchange server. Supported values for the `RemoveApiPermissions` parameter are `EWS` and `Graph`. The `EWS` value removes the `full_access_as_app` permission, while the `Graph` value removes the Graph API permissions.

To remove the `full_access_as_app` EWS API permission, run:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -RemoveApiPermissions "EWS"
```

### Delete the application

If needed, use the following command to delete the application created in Entra ID. This command can be executed on a non-Exchange server. Use this command only when rolling back the change or troubleshooting the creation of a new application. Deleting the application via the script doesn't revert the Exchange hybrid application configuration in your environment. To fully revert, follow the steps in Roll back the dedicated Exchange hybrid application configuration.

```powershell
.\ConfigureExchangeHybridApplication.ps1 -DeleteApplication
```

## Monitor and secure the application

### Audit application usage in Entra ID

After you configure the dedicated Exchange hybrid application and enable the feature, audit its usage through the Entra ID [`Sign-in logs`](/en-us/entra/identity/monitoring-health/concept-sign-ins):

1. Navigate to the Entra ID portal and sign in with your credentials.
2. Select or search for **Microsoft Entra ID**.
3. In the navigation pane, go to **Monitoring** and select **Sign-in logs**.
4. Select [**Service principal sign-ins**](/en-us/entra/identity/monitoring-health/concept-service-principal-sign-ins) to view detailed logs.

The following picture shows a successful sign-in request:

[![A screenshot that shows the Request ID, Service principal ID, Service principal name, Status, Resource and Resource ID of the dedicated Exchange hybrid application in Entra ID sign-in logs view.](../exchangehybrid/media/3p-service-principal-sign-in-1.png)](../exchangehybrid/media/3p-service-principal-sign-in-1.png#lightbox)

When you select the entry, the **Activity Details: Sign-ins** flyout opens, providing more information about the sign-in activity:

[![A screenshot that shows the advanced 'Activity Details: Sign-ins' flyout, which is opened after you click on an sign-in log entry.](../exchangehybrid/media/3p-service-principal-sign-in-2.png)](../exchangehybrid/media/3p-service-principal-sign-in-2.png#lightbox)

### Restrict access with Conditional Access

Some organizations might want to restrict access to the dedicated Exchange hybrid application service principal to a subset of public IP ranges used by Exchange Server. Use [Conditional Access for workload identities](/en-us/entra/identity/conditional-access/workload-identity) to achieve this. This feature extends Conditional Access policy support to service principals owned by the organization. Workload Identities Premium licenses are required to create or modify Conditional Access policies scoped to service principals. For more information, see [Microsoft Entra Workload ID](https://www.microsoft.com/security/business/identity-access/microsoft-entra-workload-identities#office-StandaloneSKU-k3hubfz).

## Roll back the dedicated Exchange hybrid application configuration

Warning

Since October 31, 2025, EWS access through the shared service principal is **permanently blocked**. Rolling back to the shared service principal doesn't restore rich coexistence hybrid features (Free/Busy, MailTips, and profile picture sharing). Only use these rollback steps if you need to revert the on-premises configuration changes for troubleshooting purposes or if you plan to reconfigure the dedicated Exchange hybrid application from scratch.

The following steps revert the configuration applied by the [`ConfigureExchangeHybridApplication.ps1`](https://aka.ms/ConfigureExchangeHybridApplication) script.

### Step 1: Reconfigure the first-party Service Principal

Run HCW and select the [Oauth, Intra Organization Connector and Organization Relationship](../hybrid-configuration-wizard-choose-configuration-feature#oauth-intra-organization-connector-and-organization-relationship) option to reconfigure the first-party Service Principal.

### Step 2: Remove the Setting Override

Remove the Setting Override that enables the dedicated Exchange hybrid application feature. Run the following command from an elevated Exchange Management Shell (EMS):

```powershell
Get-SettingOverride | Where-Object {$_.ComponentName -eq "Global" -and $_.SectionName -eq "ExchangeOnpremAsThirdPartyAppId"} | Remove-SettingOverride
Get-ExchangeDiagnosticInfo -Process Microsoft.Exchange.Directory.TopologyService -Component VariantConfiguration -Argument Refresh
```

### Step 3: Revert the Auth Server configuration

Run the following command from an elevated Exchange Management Shell (EMS) to revert the Auth Server change:

```powershell
# Replace this id with the id of your tenant
$tenantId = "123e4567-e89b-12d3-a456-426614174000"

(Get-AuthServer | Where-Object {$_.Name -like "*evoSTS*" -and $_.Realm -eq $tenantId}) | Set-AuthServer -ApplicationIdentifier $null -DomainName $null
```

### Step 4: Delete the application in Entra ID

Use the script to delete the application that was created in Entra ID:

```powershell
.\ConfigureExchangeHybridApplication.ps1 -DeleteApplication
```