---
layout: Conceptual
title: Manage recipients in Exchange Hybrid environments using Management tools | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/manage-hybrid-exchange-recipients-with-management-tools
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
ms.custom:
- has-azure-ad-ps-ref
- azure-ad-ref-level-one-done
description: Manage on-premises recipients in Exchange Server Hybrid Environments using Exchange Server Management tools.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms.reviewer: 
ms.collection:
- Strat_EX_Admin
- exchange-server
f1.keywords:
- NOCSH
audience: ITPro
ms.service: exchange-server-it-pro
ms.date: 2025-10-16T00:00:00.0000000Z
locale: en-us
document_id: 2dee5b3e-6d8d-ca7e-a0c3-96d01c9a95f1
document_version_independent_id: f160f2ac-f965-c218-eba3-59909c4336bb
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/manage-hybrid-exchange-recipients-with-management-tools.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-hybrid-exchange-recipients-with-management-tools
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/manage-hybrid-exchange-recipients-with-management-tools.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 7e990e7a-a9d5-3468-c21e-70790dc2885d
---

# Manage recipients in Exchange Hybrid environments using Management tools | Microsoft Learn

If you maintain an on-premises Exchange Server only for recipient management in a hybrid environment—even after moving all recipients to Exchange Online - you might be able to decommission your last Exchange Server and manage recipients using Windows PowerShell.

Previously, even after migrating all mailboxes to Exchange Online, you still needed an on-premises Exchange Server to manage cloud recipient attributes. These attributes were edited in your on-premises Active Directory and synchronized to Microsoft Entra ID through directory synchronization. This method is still supported, and shutting down the Exchange Server remains optional.

If you no longer require Exchange Server on-premises but want to keep directory synchronization, there are several options for managing recipients:

- **Install Exchange Server management tools** and use PowerShell to manage recipients. You can clean up Active Directory using the provided script. This article describes the process.
- **Transfer the Source of Authority (SOA)** for mailboxes and other objects to Exchange Online, and then manage them from the cloud. For more information, see [Cloud-based management of Exchange attributes for Remote Mailboxes in hybrid environments](hybrid-deployment/enable-exchange-attributes-cloud-management).

## Will this new method work for me?

An updated version of the Exchange Management Tools can eliminate the need for running an on-premises Exchange server if all of the following statements are true:

- You migrated all mailboxes and public folders to Exchange Online (no on-premises Exchange recipients).
- You use AD for recipient management and cloud sync or Microsoft Entra Connect for synchronization.
- You don't use or require the on-premises Exchange admin center or Exchange role-based access control (RBAC).
- You're comfortable using Windows PowerShell only for recipient management.
- You don't require auditing or logging of recipient management activity.
- You're running only one on-premises Exchange server and only for recipient management.
- You want to manage recipients without running any Exchange servers.

Use Exchange Setup in Exchange 2019 Cumulative Update 12 or later to install the latest Management tools on any domain-joined computer (client or server). For instructions, see [Install the Exchange Management tools](/en-us/exchange/plan-and-deploy/post-installation-tasks/install-management-tools).

Warning

**DO NOT** uninstall the last server. You can choose to shut down the server, and use the script to clean up, but DO NOT uninstall. Uninstalling the server removes critical information from Active Directory that breaks the ability of the management tool package to manage Exchange attributes. Learn more here: Important: Be Aware

With the updated Exchange Management Tools, domain admins and members of the Recipient Management EMT group (created through step 6 below) can use Windows PowerShell to run the following cmdlets without a running Exchange server:

- Set-MailUser, Get-MailUser, New-MailUser, Remove-MailUser, Disable-MailUser, and Enable-MailUser.
- Set-MailContact, Get-MailContact, New-MailContact, Remove-MailContact, Disable-MailContact, and Enable-MailContact.
- Set-RemoteMailbox, Get-RemoteMailbox, New-RemoteMailbox, Remove-RemoteMailbox, Disable-RemoteMailbox, and Enable-RemoteMailbox.
- Set-DistributionGroup, Get-DistributionGroup, New-DistributionGroup, Remove-DistributionGroup, Disable-DistributionGroup, and Enable-DistributionGroup (excluding Upgrade-DistributionGroup).
- Get-DistributionGroupMember, Add-DistributionGroupMember, Remove-DistributionGroupMember, and Update-DistributionGroupMember.
- Set-EmailAddressPolicy, Get-EmailAddressPolicy, New-EmailAddressPolicy, Remove-EmailAddressPolicy, and Update-EmailAddressPolicy.
- Set-User and Get-User.

Note

You can't modify on-premises recipients directly in Microsoft Entra ID or Exchange Online.

## Verify that Management Tools can run without Exchange Server

If your environment includes a single Exchange server running solely for cloud recipient management, use the steps in this section to test the Management Tools update.

### Prepare the Exchange Environment

1. Verify that all mailboxes are in the cloud by running the following commands in the Exchange Management Shell:

    ```powershell
    Set-AdServerSettings -ViewEntireForest $true
    Get-Mailbox
    ```

    Note

    By default, built-in admin mailboxes aren't synced to the cloud by cloud sync or Microsoft Entra Connect. Before you proceed, you should disable these mailboxes using Disable-Mailbox.
2. Verify that the Exchange Online tenant coexistence domain (usually something like `<domain>.mail.onmicrosoft.com`) is configured as target delivery domain by running the following command:

    ```powershell
    Get-RemoteDomain Hybrid* | Format-List DomainName,TargetDeliveryDomain
    ```

    If the coexistence domain isn't added as a remote domain, you can add it using New-RemoteDomain. For example:

    ```powershell
    New-RemoteDomain -Name 'Hybrid Domain - <domain>.mail.onmicrosoft.com' -DomainName '<domain>.mail.onmicrosoft.com'
    ```

    If it isn't set as the Target Delivery Domain, you can set it using *Set-RemoteDomain*. For example:

    ```powershell
    Set-RemoteDomain -TargetDeliveryDomain: $true -Identity 'Hybrid Domain - <domain>.mail.onmicrosoft.com'
    ```

    Note

    If you already removed the last Exchange server or never had one, you can access the Set-RemoteDomain and New-RemoteDomain cmdlets via the Exchange snap-in. Install the Exchange Management Tools from the last Cumulative Update for Exchange Server 2019 on any domain-joined machine and run the following command in Windows PowerShell:

    ```PowerShell
    Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    ```

    This method of manually enabling the Exchange snap-in is only supported for this specific case.

    Installing the Exchange Management Tools in an environment that never had an Exchange Server creates a new Exchange organization, and prepares Active Directory for Exchange. If you have a large AD deployment, or if a separate team manages AD, use the steps here: [Prepare Active Directory and domains for Exchange Server](/en-us/Exchange/plan-and-deploy/prepare-ad-and-domains) to prepare AD.
3. [Install the Exchange Management Tools](/en-us/exchange/plan-and-deploy/post-installation-tasks/install-management-tools) role using the Exchange Server 2019 April 2022 Cumulative Update or a later version of Setup. The updated tools can be installed on any domain-joined computer in an Exchange 2013 or later Exchange organization.

    Note

    Installing the updated Exchange Management Tools in an environment with only Exchange 2013 and/or Exchange 2016 will upgrade the Exchange organization to Exchange Server 2019, and performs an AD schema update. If you have a large AD deployment, or if a separate team manages AD, use the steps here: [Prepare Active Directory and domains for Exchange Server](/en-us/Exchange/plan-and-deploy/prepare-ad-and-domains) to perform the schema update.
4. Install the Windows Remote Server Administration Tools using the steps in this article: [Install, uninstall and turn off/on RSAT tools](/en-us/windows-server/remote/remote-server-administration-tools#install-uninstall-and-turn-offon-rsat-tools).
5. If you have the Scripting Agent enabled, copy **ScriptingAgentConfig.xml** from *$env:ExchangeInstallPath\Bin\CmdletExtensionAgents* on the Exchange Server, to the *$env:ExchangeInstallPath\Bin\CmdletExtensionAgents* folder on the computer with the Management Tools update installed.
6. Run the provided script to create the Recipient Management EMT security group that grants users without Domain admin rights to manage recipients.

    1. Sign-in to the computer with the Management Tools update as a Domain Admin and open Windows PowerShell.
    2. Load the Recipient Management snap-in by running the following command:

        ```PowerShell
        Add-PSSnapin *RecipientManagement
        ```
    3. Run Add-PermissionForEMT.ps1 from the $env:ExchangeInstallPath\Scripts folder. The script creates a security group called Recipient Management EMT. Members of this group have recipient management permissions. All admins without domain admin rights need to perform recipient management should be added to this security group.
7. Sign in to the computer with the Management Tools update with the appropriate permissions (domain admin or member of Recipient Management EMT) and load the Recipient Management snap-in by running:

    ```powershell
    Add-PSSnapin *RecipientManagement
    ```

    You need to do this step every time you manage recipients.
8. Test all recipient management cmdlets and verify that you see the expected results.

    Note

    Cmdlets when accessed via PowerShell Snap-in like `RecipientManagement` have a difference in the output data types compared to when run using `New-PSSession`. This is expected and any scripts that rely on the cmdlets' data types should be modified accordingly. For instance, (`Get-Mailbox User).EmailAddresses.GetType()` when used through `RecipientManagement SnapIn` yields data type as `ProxyAddressCollection`, whereas the same cmdlet when run in a PSSession yields data type as `ArrayList`.
9. Shut down your last Exchange server and verify that all recipient management cmdlets still work as expected.

    Note

    When you shut down your final Exchange server and test the create and update commands like `New-` or `Set-RemoteMailbox`, you'll observe significant increase in latency. This is because the Admin Audit Log initializer attempts to connect to the powered-down Exchange server, causing a timeout delay of approximately 40 seconds. After cleaning up the server in Active Directory using the `CleanupActiveDirectoryEMT.ps1` script mentioned in the Active Directory clean up section, this delay is no longer present.

## Permanently shutting down your last Exchange Server

If you intend to permanently shut down your last Exchange Server, we recommend that you use the following steps to clean up and improve the security posture of your environment.

Important

If you use your last Exchange server for any purpose other than recipient management (for example, SMTP relay), then don't shut it down.

1. Turn on your last Exchange server.
2. Clean up your hybrid configuration by performing [Steps 1 to 8](/en-us/exchange/decommission-on-premises-exchange#to-keep-ad-fs-and-directory-synchronization-and-decommission-most-of-the-exchange-servers) for Scenario 2 in [How and when to decommission your on-premises Exchange servers in a hybrid deployment](/en-us/exchange/decommission-on-premises-exchange#scenario-two).
3. Remove the Federation Trust by running the following command in the Exchange Management Shell:

    ```powershell
    Remove-FederationTrust "Microsoft Federation Gateway"
    ```
4. Remove the Federation Certificate: To find the certificate thumbprint, run:

    ```powershell
    $fedThumbprint = (Get-ExchangeCertificate | Where-Object {$_.Subject -eq "CN=Federation"}).Thumbprint
    ```

    To remove the certificate thumbprint, run:

    ```powershell
    Remove-ExchangeCertificate -Thumbprint $fedThumbprint
    ```
5. Remove the Service Principal credentials created for OAuth. To complete this action you can use the [ConfigureExchangeHybridApplication.ps1](https://aka.ms/ConfigureExchangeHybridApplication) script.

    Use this syntax to clean up the keyCredentials of the first-party Service Principal:

    ```powershell
    .\ConfigureExchangeHybridApplication.ps1 -ResetFirstPartyServicePrincipalKeyCredentials
    ```
6. Uninstall the Hybrid agent. If your environment has a Modern Hybrid configuration, follow the steps below to remove it.

    1. In the computer where Hybrid Agent is installed, open the Exchange Management Shell and change directory to the location of the script **C:\Program Files\Microsoft Hybrid Service\HybridManagement.psm1** and then import the Hybrid Agent PowerShell Module.

        ```PowerShell
        Import-Module .\HybridManagement.psm1
        ```
    2. To remove the App, an AppId is required. Use any of the following cmdlets in Exchange Online PowerShell to find the AppId.

        ```powershell
        Get-OrganizationRelationship ((Get-OnPremisesOrganization).OrganizationRelationship) | Select-Object TargetSharingEpr
        ```

        The output looks like this:

        ```powershell
        TargetSharingEpr
        ----------------
        https://123e4567-e89b-12d3-a456-426614174000.resource.mailboxmigration.his.msappproxy.net/EWS/Exchange.asmx
        ----------------
        https://123e4567-e89b-12d3-a456-426614174000.resource.mailboxmigration.his.msappproxy.net/EWS/Exchange.asmx
        ```

        Or, run:

        ```powershell
        Get-MigrationEndpoint "Hybrid Migration Endpoint - EWS (Default Web Site)" | Select-Object RemoteServer
        ```

        The output looks like this:

        ```powershell
        RemoteServer
        ------------
        123e4567-e89b-12d3-a456-426614174000.resource.mailboxmigration.his.msappproxy.net
        ```

        In this example, 123e4567-e89b-12d3-a456-426614174000 is the AppId to be used in the next step.
    3. Remove the App by running:

        ```powershell
        Remove-HybridApplication -appId 123e4567-e89b-12d3-a456-426614174000 -Credential (Get-Credential)
        ```

        Note

        The AppId is 123e4567-e89b-12d3-a456-426614174000 only for this example; your value is different.
    4. Uninstall the Hybrid agent using the steps here: [Uninstall the hybrid agent](/en-us/exchange/hybrid-deployment/hybrid-agent#uninstall-the-hybrid-agent).
7. If you haven't already, point your MX and Autodiscover DNS records to Exchange Online. This step is important to ensure mail flow isn't affected. For more information, see [External Domain Name System records for Office 365](/en-us/microsoft-365/enterprise/external-domain-name-system-records).
8. Shut down your last Exchange server.

## Active Directory clean up

If you plan to never run an on-premises Exchange server again, we recommend that you clean up your Active Directory by removing unnecessary Exchange objects.

Warning

This step can't be undone. Proceed only if you **never** want to run Exchange Server again.

AD cleanup can be done by running the CleanupActiveDirectoryEMT script shipped with Management tools. The script removes system mailboxes, unnecessary Exchange containers, permissions for Exchange Security Groups on the domain and configuration partitions, and the Exchange Security Groups. You need to run this script with domain admin credentials.

This script is available at: `$env:ExchangeInstallPath\Scripts\CleanupActiveDirectoryEMT.ps1`

### Important: Be Aware

Warning

**Once you shut down the last Exchange server, Exchange RBAC will no longer function**. Users who were a part of Exchange Recipient groups or had custom Exchange roles allowing for recipient management will no longer have permission. Only domain admins and users who are assigned permission using `Add-PermissionForEMT.ps1` script will be able to perform recipient management.

Once you shut down your last Exchange server and perform the Exchange hybrid and Active Directory cleanup steps as previously described, you should **erase and reformat your last Exchange server**. **Do Not Uninstall the Exchange Server**.

## Update the Exchange Server management tools only role (with no running Exchange Server) to a newer Cumulative or Security update

You have followed steps from [this article](/en-us/Exchange/manage-hybrid-exchange-recipients-with-management-tools) to remove the last Exchange Server and are using management tools only role for management of hybrid objects.

### Upgrade management tools to a newer Cumulative Update (CU)

In such environments, if you upgrade the Management tools only role server to newer CU, it may fail with the following error:

[![Screenshot of the upgrade management tools to newer Cumulative Update.](exchangehybrid/media/upgrade-management-tools-only-role-server-to-newer-cu-error.png)](exchangehybrid/media/upgrade-management-tools-only-role-server-to-newer-cu-error.png#lightbox)

Active Directory must be prepared with 'Setup /PrepareAD' before Exchange Server management tools can be updated to a newer CU.

To update the management tools to a newer CU, perform the following steps:

1. Use the following command to perform PrepareAD:

    `.\Setup.EXE /PrepareAD /IAcceptExchangeServerLicenseTerms_DiagnosticDataON`
2. Use the following command to upgrade the Management tools only role:

    `.\Setup.EXE /m:Upgrade /IAcceptExchangeServerLicenseTerms_DiagnosticDataON`
3. If you had previously executed `.\CleanupActiveDirectoryEMT.ps1` in the environment as per [Manage recipients in Exchange Hybrid environments using Management tools](/en-us/Exchange/manage-hybrid-exchange-recipients-with-management-tools), run the `.\CleanupActiveDirectoryEMT.ps1` script again (because /PrepareAD re-created some objects that the `CleanupActiveDirectoryEMT.ps1` removes).

    Warning

    Ensure that you're running `CleanupActiveDirectoryEMT.ps1` script ONLY in the environment where you have already followed [Manage recipients in Exchange Hybrid environments using Management tools](/en-us/Exchange/manage-hybrid-exchange-recipients-with-management-tools#active-directory-clean-up) and the script was already run before (and there are no running Exchange Servers). This action can't be undone.

### Upgrade management tools to a newer Security Update (SU)

Download the security update package and run it to update management tools role to a newer SU.