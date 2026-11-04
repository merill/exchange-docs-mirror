---
layout: Conceptual
title: Create a hybrid deployment with the Hybrid Configuration wizard | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/deploy-hybrid
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
ms.topic: install-set-up-deploy
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Ent_O365_Hybrid
- Strat_EX_EXOBlocker
- Hybrid
- M365-email-calendar
ms.assetid: 997a25d3-7fb3-4d4e-bb28-defcbf542c99
ms.reviewer: 
description: Admins can learn how to use the Hybrid Configuration wizard (HCW) to create a hybrid deployment between and on-premises Exchange organization and an Exchange Online organization.
ms.date: 2026-10-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: eb8cb000-e64b-b90d-fa6f-09f2b50532b3
document_version_independent_id: b65f1351-a45c-37b6-f1a8-12894f203dd4
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/deploy-hybrid.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/deploy-hybrid
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/deploy-hybrid.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: da76764d-9dcb-976f-ed89-fcacc203073e
---

# Create a hybrid deployment with the Hybrid Configuration wizard | Microsoft Learn

This article describes using the Hybrid Configuration wizard to create a hybrid deployment for the following organization configuration:

- The on-premises Exchange organization is in a single Active Directory forest.
- The organization doesn't use [the Built-in security add-on for on-premises mailboxes](../standalone-eop/standalone-eop) for cloud protection of the on-premises Exchange organization.
- The on-premises Exchange organization doesn't use Edge Transport server. The Hybrid Configuration wizard supports configuring Edge Transport servers as part of a hybrid deployment, but configuring Edge Transport servers in the wizard isn't covered in this article.

A hybrid deployment extends the feature-rich experience and administrative control of your on-premises Exchange organization to the cloud. For more information about hybrid, see [Exchange Server hybrid deployments](../exchange-hybrid).

Important

You must complete all the prerequisites outlined in [Hybrid deployment prerequisites](../hybrid-deployment-prerequisites) before you use the Hybrid Configuration wizard to create and configure your hybrid deployment.

Important

Federation Trust configuration for Exchange 2010 or earlier is no longer available in HCW.

For more management tasks related to hybrid deployments, see [Hybrid Deployment procedures](hybrid-deployment).

## What do you need to know before you begin?

- Configuring the *requirements* for a hybrid deployment takes longer than the estimated time to complete the Hybrid Configuration wizard procedures outlined in this article. For example, signing up for Microsoft 365 for enterprises, configuring Active Directory synchronization, and assigning Exchange Online licenses require a larger time investment and might also include network topology changes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Hybrid deployments" entry in the [Exchange and PowerShell infrastructure permissions](../permissions/feature-permissions/infrastructure-permissions) article.
- You need to run the Hybrid Configuration wizard from one of the following locations:

    - A supported version of Exchange server:
        - Exchange 2016 Cumulative Update 8 (CU8) or later.
        - Exchange 2013 Cumulative Update 15 (CU15) or later:
- A domain-joined computer capable of establishing remote PowerShell connections to the Client Access Server or Mailbox Server chosen for hybrid configuration.
- You need to download the Hybrid Configuration wizard from a browser that supports ClickOnce technology (for example, the latest version of Microsoft Edge).
- Review [Exchange Server Hybrid Deployments](../exchange-hybrid), and make sure you understand the areas affected by configuring a hybrid deployment.
- Review and complete all hybrid deployment requirements outlined in [Hybrid deployment prerequisites](../hybrid-deployment-prerequisites).
- The Microsoft Remote Connectivity Analyzer tool checks the external connectivity of your on-premises Exchange organization and makes sure that you're ready to configure your hybrid deployment. We strongly recommend that you check your on-premises organization with the Remote Connectivity Analyzer tool before you configure your hybrid deployment. Learn more at [Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/o365).
- For information about keyboard shortcuts that might apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Hybrid forum at [Exchange | Hybrid management](/en-us/answers/tags/377/office-exchange-hybrid-management).

## Use the Exchange admin center and Hybrid Configuration wizard to create a full classic hybrid deployment

Use the following procedure to create and configure a hybrid deployment:

1. Download the latest Hybrid Configuration wizard from https://aka.ms/hybridwizard.
2. Select **Install** on the **Application Install** dialog.
3. Select **Run** to open the Hybrid Configuration wizard.
4. The Hybrid Configuration wizard opens. On the first page, select **Next**.
5. On the **On-premises Exchange Server organization** page, configure the following options:

    - **Detect the optimal Exchange server**is selected by default. If the wizard doesn't detect an eligible Exchange server, or if you want to use a different server:
        1. Select **Specify a server Exchange 2016 or 2019**.
        2. In the **Client Access server**box, enter or select the detected internal FQDN of an Exchange server:
            - An Exchange 2013 Client Access server.
            - An Exchange 2016 or 2019 Mailbox server.
    - **My Office 365 organization is hosted by** in the **Office 365 Exchange Online**section: Select one of the available values from the drop-down list. For example:
        - **Office 365 Worldwide**
        - **Office 365 China**
        - **Office 365 U.S. Government GCC High**
        - **Office 365 U.S. Government DoD**

    When you're finished on the **On-premises Exchange Server organization** page, select **Next**.
6. On the page that opens, configure the following options:

    - **On-premises Exchange account**section: Do one of the following steps:
        - Do nothing to use current account to access your on-premises Active Directory and Exchange servers.
        - Select **Change** to select a different account. In the dialog that opens, uncheck **Use current Windows identity**, enter a different account in **Domain\username** syntax, and then select **OK**.
    - **Microsoft 365 Exchange Online Account** section: Select **Sign in** and enter the username and password of a Microsoft 365 account with Global Administrator permissions. Select **Next**.

    Verify the **On-premises Exchange account** and **Microsoft 365 Exchange Online account** values are correct, and then select **Next**.
7. On the **Gathering configuration information** page, the wizard connects to your on-premises organization and your Microsoft 365 organization using the credentials from the previous page. The wizard examines the configuration of both organizations as indicated by individual progress bars.

    When the process is complete, select **Next**.
8. On the **Hybrid Features** page, configure the following options:

    - Select **Full Hybrid Configuration**.
    - **Other options** section: Select **Organization Configuration Transfer** to do a one-time transfer of on-premises organization objects to Exchange Online. For more information, see [Hybrid Organization Configuration Transfer V2](https://techcommunity.microsoft.com/t5/exchange-team-blog/released-hybrid-organization-configuration-transfer-v2/ba-p/608762).

    When you're finished on the **Hybrid Features** page, select **Next**.
9. The **Hybrid Domains** page appears if you have more than one on-premises accepted domain added to your Microsoft 365 organization.

    The **Hybrid Domains** page doesn't appear in the following scenarios:

    - You have only one on-premises accepted domain added to your Microsoft 365 organization. Because this domain is the only domain available for hybrid deployment configuration, the domain is automatically selected and the wizard skips this step.
    - You have no on-premises accepted domains added to your Microsoft 365 organization. You need to add at least one domain to your Microsoft 365 organization before you can continue.

    On the **Hybrid Domains** page, select the domains to include in your hybrid deployment. In most deployments, you can leave **Auto Discover** set to **False** for each domain. Only select **True** for a domain if you need to force the wizard to use the Autodiscover information from a specific domain for all selected hybrid domains.

    When you're finished on the **Hybrid Domains** page, select **Next**.
10. On the **Hybrid Topology** page, select **Use Exchange Classic Hybrid Topology** to keep on-premises mailboxes, and then select **Next**.
11. On the **Transport Certificate** page, configure the following options:

    - **Select a reference server**: Select the Exchange server that hosts the certificate you configured earlier in the wizard.
    - **Select a certificate**: Select the certificate to use for secure mail transport. The list displays the digital certificates issued by a commercial certification authority (CA) installed on the Mailbox server you selected in the previous step.

    When you're finished on the **Transport Certificate** page, select **Next**.
12. On the **Organization FQDN** page, enter the externally accessible FQDN for your internet-facing Exchange server. Microsoft 365 uses this FQDN to configure the service connectors for secure mail transport between your on-premises and cloud Exchange organizations. For example, enter "mail.contoso.com."

    When you're finished on the **Organization FQDN** page, select **Next**.
13. The hybrid deployment configuration selections are updated.

    You're now ready to start the Exchange services changes and the hybrid deployment configuration. Select **Update** to start the configuration process.

    While the hybrid configuration process is running, the wizard displays the feature and service areas as they're configured for the hybrid deployment.
14. When finished, the wizard displays a completion message. Select **Close** to complete the hybrid deployment configuration process and to close the wizard.

Tip

For more information on the different Hybrid Configuration wizard options, see the following articles:

- [Use Minimal Hybrid to quickly migrate Exchange mailboxes to Microsoft 365](../mailbox-migration/use-minimal-hybrid-to-quickly-migrate)
- [Microsoft Hybrid Agent](hybrid-agent)
- [Hybrid Configuration wizard options](../hybrid-configuration-wizard-options).

## Configure OAuth authentication between Exchange and Exchange Online organizations

HCW configures OAuth authentication and organization relationships for the selected hybrid features.

For detailed configuration steps, see [Configure OAuth Authentication Between Exchange and Exchange Online Organizations](../configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help)

For more information about Exchange security and compliance features that use OAuth authentication, see the following articles:

- [Using OAuth authentication to support Archiving in an Exchange hybrid deployment](../using-oauth-authentication-to-support-archiving-in-an-exchange-hybrid-deployment-exchange-2013-help)
- [Using Oauth Authentication to Support eDiscovery in an Exchange Hybrid Deployment](../using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help)

## Federation Trust

Federation Trust configuration is no longer available in HCW.

## How do you know you successfully created a hybrid deployment?

Your first indication the hybrid configuration steps worked as expected is the successful completion of the Hybrid Configuration wizard.

To further verify you successfully created and configured your hybrid deployment, do one or more of the following steps:

- Run the following command in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell) in the on-premises organization:

    ```powershell
    Get-HybridConfiguration
    ```

The command displays the hybrid deployment configuration values and settings, hybrid features, and transport endpoints. Verify these values are correct.

- Verify the Hybrid Configuration wizard completed all configuration steps by reviewing the hybrid configuration log. By default, the log is located at `%ExchangeInstallPath%Logging\Update-HybridConfiguration` on the on-premises Exchange Mailbox server.
- Take one of the following actions:

    - Test the mailbox move feature by moving an existing on-premises mailbox to the Exchange Online organization.
    - Test free/busy calendar sharing between the on-premises and cloud organizations by creating a new user mailbox in the Exchange Online organization.

    Either action also allows you to test and confirm the following features:

    - Message delivery between the on-premises and Exchange Online organizations is functioning correctly with existing mailboxes.
    - Message delivery is secure and messages between the on-premises and cloud organizations are treated as internal.