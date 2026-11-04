---
layout: Conceptual
title: Microsoft Hybrid Agent | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/hybrid-agent
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
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: article
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Ent_O365_Hybrid
- Strat_EX_EXOBlocker
- Hybrid
- M365-email-calendar
description: The Hybrid Agent removes some of the challenges you might face when you configure an Exchange Hybrid environment.
ms.date: 2018-12-21T00:00:00.0000000Z
locale: en-us
document_id: 174147a5-effb-136b-cd43-e4da0c02a27a
document_version_independent_id: 01f56623-efbc-6e8b-766c-691b16f34a13
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/hybrid-agent.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/hybrid-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/hybrid-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 58a61a37-3354-b2d2-9c08-8d11d6a48aca
---

# Microsoft Hybrid Agent | Microsoft Learn

The Hybrid Agent removes some of the challenges you might face when you configure an Exchange Hybrid environment. The Agent, which is built on the same technology as the Microsoft Entra Application Proxy, removes some of the configuration requirements for Hybrid. For example:

- External DNS entries.
- Certificate updates.
- Inbound network connections through your firewall to enable Exchange hybrid features.

The Hybrid Agent supports Free/Busy sharing and mailbox migrations, directory synchronization, and other hybrid features.

Modern Hybrid mode is not supported in Microsoft cloud environments, including GCC, GCCH, and Gallatin. Additionally, publishing Outlook Web App (OWA) and Exchange Control Panel (ECP) through Microsoft Entra Application Proxy is unsupported.

## Agent location and requirements

Installation of the Agent and Hybrid configuration via the Hybrid Configuration wizard (HCW) is supported in either of the following locations:

- On a standalone computer (designed as your "Agent server").
- On an Exchange Server:
    - Exchange 2016 or later: Mailbox role.
    - Exchange 2013: Client Access role (CAS).

        Note

        For information on installing Hybrid Agent in an environment that has Windows Extended Protection enabled for Exchange, see [Configure Windows Extended Protection in Exchange Server](../plan-and-deploy/post-installation-tasks/security-best-practices/exchange-extended-protection#configure-windows-extended-protection-in-exchange-server).

## System requirements

The Hybrid Agent has multiple methods of installation with different requirements. In all cases, the core computer requirements are the same as described in the following list:

- Windows Server 2012 R2, Windows Server 2016, Windows Server 2019 or Windows Server 2022

    - .NET Framework 4.7.2 or later.
    - TLS 1.2 enabled.
    - [Application Proxy in Microsoft Entra ID](/en-us/entra/identity/app-proxy/application-proxy-add-on-premises-application)
    - Capable of establishing outbound HTTPS connections to the internet.
    - Capable of establishing HTTPS connections to the Exchange Server chosen for hybrid configuration.

The HCW can download and install the Agent MSI automatically, as long as the following requirements are met:

- The computer is a member of an Active Directory domain.
- The computer is capable of establishing remote PowerShell connections to the Exchange Server that's chosen for hybrid configuration.
- The computer uses a browser that supports ClickOnce technology (for example, Microsoft Edge).
- The on-premises Active Directory account you're using must meet the following requirements:

    - Membership in the Organization Management role group in your on-premises Exchange organization.
    - Membership in the local Administrators group on the computer where you're installing the Hybrid Agent.

Having the HCW download and install the Agent MSI automatically is ideal if you're installing the Agent directly on a CAS server.

## Port and protocol requirements

- Outbound ports HTTPS (TCP) 443 and 80 must be open between the computer where the Hybrid Agent installed and the internet as shown [here](/en-us/entra/identity/app-proxy/application-proxy-add-on-premises-application).
- Ports TCP ports 443, 80, 5985, and 5986 must be open between the computer where the Hybrid Agent is installed and the CAS that's selected in the Hybrid Configuration wizard.

Important

Free/busy requests from on-premises users to Exchange Online users don't traverse the Hybrid Agent. All Exchange Mailbox Servers (including Exchange 2013 Mailbox Servers) must be able to communicate with the Microsoft 365 or Office 365 endpoints via HTTPS (TCP port 443). The required URLs, IP addresses, and ports are described [here](/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges).

### Proxy server considerations

If your network environment uses outbound proxy servers, you need to do some extra configuration as described in this section. This list might not be exhaustive.

#### Agent

The Agent supports outbound unauthenticated proxy servers, but you need to do more configurations after the installation. Run the `ConfigureOutBoundProxy.ps1` script located in `\Program Files\Microsoft Hybrid Service\` on the computer where the Agent is installed. For example:

```PowerShell
PS C:\Program Files\Microsoft Hybrid Service\>.\ConfigureOutBoundProxy.ps1 -ProxyAddress http://proxyserver:8080
```

By running the script, the following section is added to the `Microsoft.Online.EME.Hybrid.Agent.Service.exe.config` file located in the same folder:

```xml
  <system.net>
    <defaultProxy>
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True" />
    </defaultProxy>
  </system.net>
```

Important

A proxy server that prevents registration causes the following items to fail:

- Connector installation.
- **Test-Connectivity** after installation.

We recommend that you allow the connectors to bypass the proxy until you can make app config changes.

#### Exchange Server

The HCW establishes connections from your Exchange Server to domains.live.com to exchange metadata and establish trusts. Because connections originate from your CAS server, the proxy settings on that server (from `Get-ExchangeServer | Format-List internetWebProxy`) must be set correctly, or outbound free/busy can fail. In addition to connection failures, the HCW can't configure delegated authentication if the proxy setting is incorrect.

## Free/Busy requirements

The hybrid wizard automatically handles the free/busy information that's required in on-premises Exchange and Exchange Online.

If you need to configure free/busy sharing with a third-party, go to the **Organization** tab in the Exchange admin center and configure individual or organization sharing between the two systems (Exchange Online and Exchange on-premises or Exchange on-premises and Exchange on-premises).

If you encounter problems, see [How to troubleshoot free/busy issues in a hybrid deployment](https://support.microsoft.com/help/2555008/how-to-troubleshoot-free-busy-issues-in-a-hybrid-deployment-of-on-prem).

## Constraints

Keep the following issues in mind before you install the Hybrid Agent:

- [Hybrid Modern Authentication](/en-us/office365/enterprise/hybrid-modern-auth-overview) isn't supported with the Hybrid Agent. You need to use the Classic Exchange Hybrid Topology and publish AutoDiscover, EWS, ActiveSync, MAPI and OAB endpoints for hybrid Modern Authentication to function with various Outlook clients.
- For Teams calendaring features that require access to on-premises mailboxes, we recommended the full Classic Exchange Hybrid Topology. For more information, see [How Exchange and Microsoft Teams interact](/en-us/microsoftteams/exchange-teams-interact).
- Message tracking and multi-mailbox search do not traverse the Hybrid Agent. These Hybrid features require the classic connectivity model where Exchange Web Services (EWS) and Autodiscover are published on-premises and are externally available to Exchange Online.
- The Hybrid Agent registers the internal FQDN of the CAS server that was selected when you ran the Hybrid Configuration wizard in the Entra Hybrid proxy infrastructure. If the registered CAS server is offline, free/busy look-ups from Exchange Online to on-premises and mailbox migration to and from Exchange Online won't work. If the selected CAS is permanently offline, you must register a new CAS server by running the Hybrid Configuration wizard again.
- The Hybrid Agent supports a single migration endpoint with the service default limits. Multiple migration endpoints using custom endpoints or URLs isn't supported.
- The Hybrid Agent supports a single Exchange organization. Multiple Exchange organizations aren't supported.

Note

SMTP doesn't traverse the Hybrid Agent and still requires a public certificate for mail flow between Exchange Online and your on-premises organization. SMTP traffic is out of scope for the Hybrid Agent.

## Running setup

You must run the HCW on the computer where you want to install the Agent. After the Agent is installed and configured, the HCW will locate a preferred server to connect to and run the standard hybrid configuration steps. You don't need to run the HCW from the Exchange server directly. But, the computer where you run the HCW must be able to connect to the Exchange Server on the ports specified in the Ports and protocols section.

### Installation Prerequisites

1. Optional: Verify connectivity.

    1. On the server where you are running the Hybrid Configuration wizard (Hybrid Agent install and subsequent hybrid configuration steps), download the following sample script and save it to any directory: https://aka.ms/hybridconnectivity.
    2. Open the Exchange Management Shell and change directory to the location of the script.
    3. Import the cmdlets by running the following command:

        ```PowerShell
        Import-Module .\HybridManagement.psm1
        ```
    4. Run the following command to verify the computer where you're installing can reach out to all required endpoints for the Hybrid Agent installation and Hybrid Configuration wizard setup.

        ```PowerShell
        Test-HybridConnectivity -TestO365Endpoints
        ```

        The output of the command looks like this:

        ![Sample output of Test-HybridConnectivity.](../exchangehybrid/media/test-hybridconnectivity-results.png)
2. To allow installation of the Hybrid Agent and perform mailbox migrations to and from your Microsoft 365 or Office 365 organization, enable the Mailbox Replication service (MRS) proxy on the EWS virtual directory by running the following command:

    ```PowerShell
    Set-WebServicesVirtualDirectory -Identity "EWS (Default Web Site)" -MRSProxyEnabled $true
    ```

    Note

    If you don't complete this step before you run the HCW, the HCW enables MRS proxy. However, we recommend that you complete this step before you run the HCW to ensure the IIS cache has time to clear before HCW validates the endpoint.
3. Go to **Programs and Features** in Control Panel and verify that a previous version of the Hybrid Configuration wizard isn't already installed. If it is, uninstall it.
4. Install .NET Framework version 4.6.2 on the computer where the HCW is being run. You might need to install a later version of .NET Framework depending on the version of Exchange you have installed. Alternatively, if this version isn't installed, the HCW prompts you to install it or upgrade the version already installed on your computer.

### Installation steps

1. Log into your on-premises Exchange admin center (EAC), navigate to the **Hybrid** node, and then click **Configure**.
2. Select the Exchange server where you want to run traditional hybrid setup. Either select the default server provided by the HCW or specify a specific server in the second radio button. Select **Next**.
3. Enter your on-premises Exchange credentials and your Microsoft 365 or Office 365 Global Administrator credentials. Click **Next**.
4. Wait while the HCW gathers information and configuration about your environments. When it's completed, click **Next**.
5. Select either **Minimal** or **Full Hybrid Configuration**. You can also choose **Organization Configuration Transfer**. For more information, see [Hybrid Organization Configuration Transfer V2](https://techcommunity.microsoft.com/t5/exchange-team-blog/released-hybrid-organization-configuration-transfer-v2/ba-p/608762). Click **Next**.
6. Follow the steps to enable federation. Click **Next**.
7. Select **Use Exchange Modern Hybrid Topology**

    ![Hybrid Topology page in the Hybrid Configuration wizard.](../exchangehybrid/media/08b9b1933233cf4348506a629d1a6f22.png)

    Click **Next**.
8. The HCW installs the Hybrid Agent. There are four basic phases:

    1. Download the Agent install package.
    2. Installation of the Agent on the local computer (note: this prompts for your Microsoft 365 or Office 365 Global Administrator credentials again).
    3. Registration of the Agent in Entra, including creation of the URL used to proxy requests. The URL has the format: `uniqueGUID.resource.mailboxmigration.his.msappproxy.net`.
    4. Testing migration viability from your Microsoft 365 or Office 365 organization to your on-premises Exchange organization via the Agent.

    Note

    The Hybrid Agent installation process could take up to 10 minutes to complete.

    The remaining HCW inputs and actions are the same as a Classic Hybrid deployment.

During the update phase, the HCW creates a migration endpoint with the custom URL created in step 8.3 above. It also sets the `TargetSharingEPR` value on the Organization Relationship and/or the IntraOrganization Connector object on the Microsoft 365 or Office 365 side to this value. The new URL is used to send requests from your Microsoft 365 or Office 365 organization to your on-premises Exchange organization for free/busy and migrations.

You can view the specific values by running **Get-MigrationEndpoint** and **Get-OrganizationRelationship** from an [Exchange Online PowerShell connection](/en-us/powershell/exchange/connect-to-exchange-online-powershell) to your Microsoft 365 or Office 365 organization.

The following example shows the output that you might see when you run the **Get-MigrationEndpoint** and **Get-OrganizationRelationship** cmdlets:

```PowerShell
Get-MigrationEndpoint | Format-List Identity,RemoteServer

Identity : Hybrid Migration Endpoint - EWS (Default Web Site)
RemoteServer : 123e4567-e89b-12d3-a456-426614174000.resource.mailboxmigration.his.msappproxy.net
```

```PowerShell
Get-OrganizationRelationship | Format-List Name,TargetSharingEpr

Name : O365 to On-premises - <GUID>
TargetSharingEpr : https://123e4567-e89b-12d3-a456-426614174000.resource.mailboxmigration.his.msappproxy.net/EWS/Exchange.asmx
```

## Hybrid Agent PowerShell module

The Hybrid Management PowerShell module is installed by the Hybrid Configuration wizard at \**\Program Files\Microsoft Hybrid Service\** on the computer where the Hybrid Agent is installed. This module provides the following cmdlets that can now be used with or without a multifactor authentication-enabled administrator account.

| Cmdlets | Purpose |
| --- | --- |
| Get-HybridAgent | To view Hybrid Agents installed. |
| Update-HybridApplication | To edit parameters like the target URI of Hybrid Application. |
| Get-HybridApplication | To view all Hybrid Applications in the organization. |
| Remove-HybridApplication | To remove a specific Hybrid Application. |

### How to use Hybrid Agent cmdlets with or without multifactor authentication-enabled accounts

To use these cmdlets, you would need to import the latest HybridManagement.psm1 available at \*\*\Program Files\Microsoft Hybrid Service\*\*. It can also be downloaded directly from https://aka.ms/HybridAgentPSM.

To import the Hybrid Management module, run the following command from a Windows PowerShell prompt as an administrator:

```PowerShell
Import-module .\HybridManagement.psm1
```

To execute these cmdlets with multifactor authentication-enabled admin credentials, you need to provide a *userPrincipalName* parameter. If your account isn't a multifactor authentication-enabled admin account, you can also use the *Credential* parameter in lieu of the *userPrincipalName* parameter, which results in the usage of basic authentication.

The following table shows how the usage differs in these two modes:

| - | Admin with a multifactor authentication-enabled account | Admin with basic authentication |
| --- | --- | --- |
| 1 | Get-HybridAgent -UserPrincipalName &lt;tenant admin UPN&gt; | Get-HybridAgent -Credential (Get-Credential) |
| 2 | Get-HybridApplication -UserPrincipalName &lt;tenant admin UPN&gt; -AppId &lt;GUID&gt; | Get-HybridApplication -Credential (Get-Credential) -AppId &lt;GUID&gt; |
| 3 | Remove-HybridApplication -UserPrincipalName &lt;tenant admin UPN&gt; -AppId &lt;GUID&gt; | Remove-HybridApplication -Credential (Get-Credential) -AppId &lt;GUID&gt; |
| 4 | New-HybridApplication -UserPrincipalName &lt;tenant admin UPN&gt; -TargetUri "Server FQDN" | New-HybridApplication -Credential (Get-Credential) -TargetUri "Server FQDN" |
| 5 | Update-HybridApplication -AppId &lt;GUID&gt; -TargetUri "Server FQDN" -UserPrincipalName &lt;tenant admin UPN&gt; | Update-HybridApplication -AppId &lt;GUID&gt; -TargetUri "Server FQDN" -Credential (Get-Credential) |

## Multi Agent Deployment

### Option 1: Use the Hybrid Configuration wizard to install additional Agents

Additional Hybrid Agents can be installed for redundancy. Simply download the latest version of the HCW and open the application on the computer where you would like to install another Hybrid Agent.

1. Like previous HCW installations, start the application, select **Next**.
2. Select a desired server to execute against, select **Next**.
3. Provide credentials to sign in to your Microsoft 365 or Office 365 organization, and then select **Next**.
4. The HCW gathers configuration information, select **Next** when complete.
5. Select the default option provided for either **Full** or **Minimal**, select **Next**.
6. Select Exchange **Modern Hybrid Topology, Next**.
7. A page is shown that provides you with the status of your existing or previously installed Agents. Make sure the status of the existing Agent is accurate before proceeding to the next step. Select **Install an additional agent**, and then click **Next**.

    Example:

    ![Sample of registered Hybrid Agents in the HCW.](../exchangehybrid/media/hcw-registered-hybrid-agents.png)

The HCW installs the additional Hybrid Agent. When the installation is complete, you can open the Microsoft Windows Services console from the computer and verify the service or Agent is installed and running (look for **Microsoft Hybrid Service - mshybridsvc**). At that point, you can either re-run HCW if you wish to make further changes to your hybrid config, or simply cancel the wizard.

You can repeat this step on each computer where you would like an additional Hybrid Agent installed.

### Option 2: Manually download and install additional Agents

A second option for installing additional Agents is outside the HCW itself and is done by downloading and manually installing the Agent on the desired computer.

1. Go to https://aka.ms/hybridagentinstaller.
2. Save the MSHybridService.msi to a location on your computer.
3. From that computer, open a Windows Command console as Administrator and run the following command to install the Hybrid Agent:

    ```PowerShell
    Msiexec /i MSHybridService.msi
    ```

    You'll be prompted for your tenant Global Admin credentials.
4. After the installation is complete, you can open the Microsoft Windows Services console from the computer and verify the service or Agent is installed and running.

You can repeat this step on each computer where you would like an additional Hybrid Agent installed.

## Checking the Status of Your Hybrid Agents

### Option 1: Get status via the Hybrid Configuration wizard

1. Start the HCW application and select **Next**.
2. Select a server in your Exchange organization and select **Next**.
3. Provide credentials to sign in to your Microsoft 365 or Office 365 organization, and then select **Next**.
4. The HCW will gather configuration information. Select **Next** when it's complete.
5. Select default option provided for either **Full** or **Minimal** and select **Next**.
6. Select **Exchange Modern Hybrid Topology** and select **Next**.

    A page will be shown that will provide you with the status of your existing installed Agents.

    ![Agent status in the HCW.](../exchangehybrid/media/hcw-agent-status.png)
7. Click **Cancel** when you're finished.

### Option 2: Get status via the Hybrid Management PowerShell Module

With each installation of the Hybrid Agent, the HCW installs the Hybrid Management PowerShell module in \Program Files\Microsoft Hybrid Service\ on the computer where the Agent is installed. By default, this module isn't imported and so you will need to import it before you can use it. This module also requires the Azure module for PowerShell if not already installed. First install [the PackageManagement modules](https://www.powershellgallery.com/packages/PackageManagement/) and then see [this topic](/en-us/powershell/azure/servicemanagement/install-azure-ps) for the Azure PowerShell module installation instruction.

To import the Hybrid Management module, run the following command from a Windows PowerShell prompt as Administrator:

```PowerShell
Import-module .\HybridManagement.psm1
```

After that you can run the following command to view Agent status:

```PowerShell
Get-HybridAgent -Credential (Get-Credential)
```

The output of the command looks like this:

![Get-HybridAgent results.](../exchangehybrid/media/get-hybridagent-output.png)

Note

The **id** value in the results is the Agent identity and not your unique tenant guid assigned to the route.

## Direct your Hybrid Agent(s) to the load balancer instead of a specific server

You can use the Hybrid Management PowerShell module to configure your Hybrid Agent(s) to direct requests to your load balancer instead of a specific Exchange Server. The Hybrid Agent supports routing requests to the load balancer for Exchange Server 2013 Client Access Servers and Exchange Server 2016 servers or later.

1. Follow the steps from the previous section to import the Hybrid Management module for PowerShell.
2. Use the *targetUri* parameter on the **Update-HybridApplication** cmdlet to change the value of the internalURL from a specific server to your load balancer endpoint.
3. Use the unique endpoint GUID value for your tenant for the *appId* parameter (for example, 123e4567-e89b-12d3-a456-426614174000). **Note that this GUID value isn't the Agent ID**. To find the endpoint GUID value, use either of the following procedures:

    - From the `TargetSharingEPR` value:

        ```PowerShell
        Get-OrganizationRelationship ((Get-OnPremisesOrganization).OrganizationRelationship) | Select-Object TargetSharingEpr
        ```

        The output looks like this:

        ```powershell
        TargetSharingEpr
        ----------------
        https://123e4567-e89b-12d3-a456-426614174000.resource.mailboxmigration.his.msappproxy.net/EWS/Exchange.asmx
        ```
    - From the MRS configuration:

        ```PowerShell
        Get-MigrationEndpoint "Hybrid Migration Endpoint - EWS (Default Web Site)" | Select-Object RemoteServer
        ```

        The output looks like this:

        ```powershell
        RemoteServer
        ------------
        123e4567-e89b-12d3-a456-426614174000.resource.mailboxmigration.his.msappproxy.net
        ```
4. After you have the endpoint GUID value for your tenant, run the following command:

    - *targetUri*: `https://myloadbalancer.contoso.com` in this example (your value will be different).
    - *appId*: 123e4567-e89b-12d3-a456-426614174000 in this example (your value will be different).

    ```PowerShell
    Update-HybridApplication -targetUri "https://myloadbalancer.contoso.com" -appId 123e4567-e89b-12d3-a456-426614174000 -Credential (Get-Credential)
    ```

    Example:

    ![Update-HybridConfiguration command output.](../exchangehybrid/media/update-hybridconfiguration-output.png)

## Additional Information

You can view installation details of the Hybrid Agent in the following locations on the server where it's installed.

- In the Services console:

    ![The Microsoft Hybrid Service in the list of Windows Services.](../exchangehybrid/media/183c42b7f780c0f11399ad84d5b794ca.png)
- In the registry at `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Hybrid Service`:

    ![HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Hybrid Service.](../exchangehybrid/media/3d0ea73be12c78a759c3e6947dbfcea6.png)
- On the hard drive:

    ![Location of the Microsoft Hybrid Service on the hard drive.](../exchangehybrid/media/cc0348c42c337d0dd313272aed0bfd89.png)
- In **Programs and Features** in Control Panel:

    ![The Microsoft Hybrid Service in Programs and Features.](../exchangehybrid/media/f06cc90d380e6f23cedc43d38a7fc075.png)

## Testing and validation of the Hybrid Agent

After a successful deployment of the Hybrid Agent and hybrid configuration, you can use the following steps to validate free/busy and mailbox migration flow via the Agent.

1. On the server where the Hybrid Agent is installed, open **Performance Monitor**.
2. Add the object **Microsoft AD App Proxy Connector** and the **# requests** counter to your view.

    ![The Hybrid Agent in Performance Monitor.](../exchangehybrid/media/d67d36919447785a56ab2b3759e12e74.png)

### Migration

1. Open an [Exchange Online PowerShell connection](/en-us/powershell/exchange/connect-to-exchange-online-powershell) to your Microsoft 365 or Office 365 organization.
2. Replace &lt;your customguid&gt; with the unique endpoint GUID value as described in Direct your Hybrid Agent(s) to the load balancer instead of a specific server and run the following command:

    ```PowerShell
    Test-MigrationServerAvailability -ExchangeRemoteMove:$true -RemoteServer '<your customguid>.resource.mailboxmigration.his.msappproxy.net' -Credentials (Get-Credential)
    ```
3. Enter your on-premises credentials in the dialog that appears.

After the test returns the success result, switch back to **Performance Monitor** and confirm that the number of requests has increased.

Performing a test mailbox move from your on-premises Exchange organization to your Microsoft 365 or Office 365 organization is also an option.

Note

If this test fails try running Update-HybridApplication and point it to a single Exchange Server instead of a load balancer.

### Free/Busy

To perform the same validation for free/busy information, log in to a Microsoft 365 or Office 365 mailbox in your tenant, create a test meeting invite, and send it to an on-premises mailbox.

## Uninstall the Hybrid Agent

To uninstall the Hybrid Agent, re-run Hybrid Configuration wizard from the same computer you ran the installation on and select **Classic Connectivity**. Selecting classic connectivity uninstalls and unregisters the Hybrid Agent from the computer and Entra. After you unregister the Hybrid Agent, you can resume setup and configure hybrid in classic mode.

## Switching modes from Classic to Modern

You can switch to Modern Hybrid (Hybrid Agent) after successfully configuring Classic Hybrid (publishing the EWS namespace and allowing inbound). But, we only recommend switching if you're blocked from migrating mailboxes to the cloud after this setup is complete. If you chose to revert to Modern Hybrid, see the previous Constraints section, because not all hybrid features or experiences are supported with the Hybrid Agent.

If you have weighed the pros and cons of switching from Classic to Modern, you proceed by deleting your existing migration batches and migration endpoint in Exchange Online and re-running the Hybrid Configuration wizard and selecting **Modern Hybrid**.