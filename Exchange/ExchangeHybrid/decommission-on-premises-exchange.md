---
layout: Conceptual
title: How and when to decommission your on-premises Exchange servers in a hybrid deployment | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/decommission-on-premises-exchange
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
ms.reviewer: 
ms.topic: install-set-up-deploy
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Strat_EX_EXOBlocker
- M365-email-calendar
ms.assetid: 4f884b7a-3b8a-4207-8843-65d3141731dc
description: Read this article if you're ready to move from an Exchange hybrid deployment to a full cloud implementation.
ms.date: 2025-10-17T00:00:00.0000000Z
locale: en-us
document_id: a6eb1f9b-27f6-4d93-5a97-ad3f8b6ed27d
document_version_independent_id: f248ffa0-1bc3-be8f-055a-1c941e3ad234
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/decommission-on-premises-exchange.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: decommission-on-premises-exchange
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/decommission-on-premises-exchange.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: ab91a833-32ad-36d4-2456-4349c629c15a
---

# How and when to decommission your on-premises Exchange servers in a hybrid deployment | Microsoft Learn

Note

Depending on your scenario, you may have more targeted guidance available:

- If you've transferred Exchange-attribute Source of Authority (SOA) to the cloud and want to **uninstall** your last Exchange Server, see [Decommission the last Exchange Server after transferring SOA to cloud](/en-us/exchange/hybrid-deployment/decommission-last-exchange-server).
- If you have an on-premises Exchange Server for recipient management only and want to **shut down** your last Exchange Server, see [Manage recipients in Exchange Hybrid environments using Management tools](/en-us/exchange/manage-hybrid-exchange-recipients-with-management-tools).

This article covers the general decommissioning of on-premises Exchange in a hybrid deployment.

[Exchange Server hybrid deployments](exchange-hybrid) describes one of the most attractive options for getting a company to Exchange Online. This method is the only option that allows you to easily onboard and offboard mailboxes. All other native options are onboard only. A hybrid configuration also has the following key options.

- **Cross-premises availability**: See user free/busy information while scheduling a meeting, regardless of where their mailbox is located.
- **Cross-premises archive**: Move only a user's archive mailbox to the cloud. This move is often the first step for customers to try Microsoft 365 and Exchange Online.
- **Cross-premises discovery searches**: With OAuth authentication, you can do eDiscovery searches in mailboxes and archives in both environments.
- **Outlook on the web URL redirection**: Users are redirected to the proper environment for Outlook on the web (formerly known as Outlook Web App or OWA).
- **No profile recreation after move**: Unlike other migration options, the mailbox GUID doesn't change. In other words, users don't need to recreate their Outlook profiles or redownload their OST files after a mailbox move.

Depending on your organization's needs, a hybrid deployment is the best option for providing the most seamless user and coexistence experience.

This article helps you understand the options for decommissioning Exchange hybrid, and when you should use those options. There are many variances in when and how to decommission Exchange hybrid servers. Taking the time to understand the implications and properly plan the full or partial decommissioning of on-premises servers is important.

## Other methods to migrate to Exchange Online

A hybrid deployment isn't for everyone. Many organizations that chose to deploy a hybrid configuration have fewer than 50 users. While the advantages of a hybrid deployment are attractive, hybrid comes with a hefty price in complexity. Many smaller organizations use a cutover, staged, or IMAP migration. A program called FastTrack can help you decide on your best migration option. Information on FastTrack is described on the [Microsoft 365 FastTrack page](https://www.microsoft.com/fasttrack/microsoft-365).

Use the following table to decide what type of migration works for your organization. For more information, see [Ways to migrate multiple email accounts to Microsoft 365 or Office 365](mailbox-migration/mailbox-migration).

| Existing organization | Number of mailboxes to migrate | Manage user accounts in your on-premises organization? | Migration type |
| --- | --- | --- | --- |
| Exchange 2003 or later | Less than 2,000 mailboxes | No | Cutover Exchange migration |
| Exchange 2007 or Exchange 2003 | Less than 2,000 mailboxes | No | Staged Exchange migration |
| Exchange 2007 or Exchange 2003 | More than 2,000 mailboxes^\*^ | Yes | Staged Exchange migration or remote move migration in an Exchange hybrid deployment |
| Exchange 2010 or later | More than 2,000 mailboxes^\*^ | Yes | Remote move migration in an Exchange hybrid deployment |
| Exchange 2000 Server or earlier versions | No maximum | Yes | IMAP migration |
| Non-Exchange on-premises messaging system | No maximum | Yes | IMAP migration |

^\*^Some organizations with fewer than 2,000 mailboxes might benefit from features and capabilities available only with a hybrid deployment. Carefully consider the benefits of a hybrid deployment with the inherent complexity. We strongly recommend consideration of cutover or staged migration for organizations with fewer than 2,000 mailboxes.

## Why you might not want to decommission on-premises Exchange servers

Many hybrid organizations eventually move all mailboxes to Exchange Online. At this point, they probably think it's time to remove their on-premises Exchange servers. But, it's not a good idea as removing on-premises Exchange servers in a hybrid deployment prevents the management of cloud mailboxes. The culprit is directory synchronization.

When directory synchronization is enabled and a user is synchronized from the on-premises environment to the cloud, you can't manage most user properties from Exchange Online; you must manage those properties in the on-premises environment. Even if you configured directory synchronization without running the Hybrid Configuration wizard (HCW), you still can't do most recipient management tasks in the cloud. For more information, see this [blog post](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/Decommissioning-your-Exchange-2010-servers-in-a-Hybrid/ba-p/597185).

## Can I use non-Microsoft tools to manage Exchange objects in a hybrid deployment?

Yes, but they aren't supported. Microsoft supports the following tools to manage Exchange recipients and objects:

- The Exchange Management Console.
- The Exchange admin center (EAC).
- The Exchange Management Shell.

Non-Microsoft tools or even ASDIEDIT aren't supported tools for managing Exchange users, and you use them at your own risk. These tools often work fine, but we don't validate these tools.

## Common hybrid to cloud only scenarios

While there are issues, creating a hybrid deployment is a relatively easy, wizard-based process that we took the time to get right. But going from hybrid to cloud only isn't as easy, and requires careful planning.

This section contains three common hybrid to cloud only scenarios along with our recommendations. Find the scenario that best fits your situation and use it to formulate a plan to keep or decommission your hybrid and/or on-premises Exchange environment.

### Scenario 1: All mailboxes and all cloud management

- **Scenario**: My organization has a hybrid configuration and now all mailboxes are in Exchange Online. We don't need to manage users in the on-premises environment and we don't need directory synchronization or password synchronization.
- **Solution**: Since all users will be managed in Microsoft 365 and there are no other directory synchronization requirements, you can safely disable directory synchronization and remove Exchange from the on-premises environment.

    ![Remove Exchange from the on-premises environment.](exchangehybrid/media/f9c2a2cb-4c16-4ca3-8244-b89c1cdf0744.jpg)

#### Disable directory synchronization and uninstall Exchange hybrid

1. Run the following command in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell) to verify the *PublicFoldersEnabled* value isn't 'Remote':

    ```powershell
    Get-OrganizationConfig | Format-List PublicFoldersEnabled
    ```

    If the *PublicFoldersEnabled* value is 'Remote' and you need to access public folders, you need to migrate them to Exchange Online. For more information, see [Use batch migration to migrate Exchange Server public folders to Exchange Online](/en-us/exchange/collaboration/public-folders/migrate-to-exchange-online).
2. Since all mailboxes are in Exchange Online, you can point your MX and Autodiscover record in DNS to Exchange Online. For more information, see [External Domain Name System records for Office 365](/en-us/microsoft-365/enterprise/external-domain-name-system-records).

    Important

    Be sure to update both internal and external DNS. Otherwise, you might have inconsistent client connectivity.
3. Use the **Set-ClientAccessServer** or **Set-ClientAccessService** cmdlet in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell) to remove the Service Connection Point (SCP) values from your Exchange servers. This step ensures no SCPs are returned, and the client instead uses the DNS method for Autodiscover.

    Exchange 2010 or 2013:

    ```powershell
    Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    ```

    Exchange 2016 or later:

    ```powershell
    Get-ClientAccessService | Set-ClientAccessService -AutoDiscoverServiceInternalUri $Null
    ```

    Note

    If you have Exchange 2007 servers, you need to run the `Get-ClientAccessServer | Set-ClientAccessServer...` command on those servers.
4. Do the following steps to delete the inbound and outbound connectors created by the Hybrid Configuration wizard:

    1. Open the Exchange admin center at https://admin.exchange.microsoft.com as an [Exchange Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#exchange-administrator) and go to **Mail Flow** &gt; **Connectors**. Or to go directly to the **Connectors** page, use https://admin.exchange.microsoft.com/#/connectors.
    2. On the **Connectors**page, disable or delete the inbound and outbound connectors created by the Hybrid Configuration wizard:
        - **Inbound from &lt;unique identifier&gt;**
        - **Outbound from &lt;unique identifier&gt;**
5. Remove the organization relationship created by the Hybrid Configuration wizard:

    1. Open the Exchange admin center at https://admin.exchange.microsoft.com at https://admin.exchange.microsoft.com as an [Exchange Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#exchange-administrator) and go to **Organization** &gt; **Sharing**. Or, to go directly to the **Sharing** page, use https://admin.exchange.microsoft.com/#/organizationsharing.
    2. On the **Sharing** page, remove the **O365 to On-Premises - &lt;unique identifier&gt;** relationship created by the Hybrid Configuration wizard.
6. Disable the OAuth configuration from the on-premises environment and Microsoft 365:

    - **On-premises Exchange**: Run the following command in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell):

        ```powershell
        Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
        ```
    - **Exchange Online**: Run the following command in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell):

        ```powershell
        Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        ```

    Note

    The *Identity* parameter value assumes you used the Hybrid Configuration wizard to configure OAuth. If not, you might need to use a different *Identity* value.
7. Disable directory synchronization. For instructions, see [Turn off directory synchronization for Microsoft 365 or Office 365](/en-us/microsoft-365/enterprise/turn-off-directory-synchronization).

    When you complete this step, you do all user management tasks in Microsoft 365. You no longer use the Exchange Management Console or Exchange admin center in on-premises Exchange.
8. You can now safely uninstall Exchange from the on-premises servers.

### Scenario 2: All cloud mailboxes with AD FS

- **Scenario**: My organization has a hybrid configuration and now all mailboxes are in Exchange Online. We plan to keep Active Directory Federation Services (AD FS) for user authentication of Exchange Online mailboxes.

    Important

    This scenario applies to hybrid organizations that plan to keep directory synchronization and use the Exchange admin center in on-premises Exchange to manage recipients. If you don't require the on-premises EAC to manage recipients, you can remove the last on-premises Exchange server and still keep directory synchronization. For more information, see [Manage hybrid exchange recipients with management tools](manage-hybrid-exchange-recipients-with-management-tools).
- **Solution**:

    - Since you're keeping AD FS, you also need to keep directory synchronization as a prerequisite.
    - Even though you have no on-premises mailboxes, you can't fully remove all Exchange servers from the on-premises environment. But you can remove most of them. You need to leave one or more on-premises Exchange servers (which can be virtual machines) for user management, because the source of authority is still in on-premises Exchange.

    ![State before decommissioning Exchange servers.](exchangehybrid/media/c692f0af-6536-4bc9-950d-58a1e486525f.jpg)

Tip

If you choose to remove AD FS from your infrastructure, cloud sync or Microsoft Entra Connect synchronizes your on-premises credentials with the cloud. Each service authenticates users independently:

- **Microsoft 365 identity services** manages online authentication requests.
- **Active directory** manages the internal authentication.

#### Keep AD FS and decommission most Exchange servers

1. Run the following command in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell) to verify the *PublicFoldersEnabled* value isn't 'Remote':

    ```powershell
    Get-OrganizationConfig | Format-List PublicFoldersEnabled
    ```

    If the *PublicFoldersEnabled* value is 'Remote' and you need to access public folders, you need to migrate them to Exchange Online. For more information, see [Use batch migration to migrate Exchange Server public folders to Exchange Online](/en-us/exchange/collaboration/public-folders/migrate-to-exchange-online).

    If you need to keep public folders and migrating them to Exchange Online isn't an option, go to Scenario 3: All cloud mailboxes with some on-premises email services.
2. Since all mailboxes are in Exchange Online, you can point your MX and Autodiscover record in DNS to Exchange Online. For more information, see [External Domain Name System records for Office 365](/en-us/microsoft-365/enterprise/external-domain-name-system-records).

    Important

    Be sure to update both internal and external DNS. Otherwise, you might have inconsistent client connectivity.
3. Use the **Set-ClientAccessServer** or **Set-ClientAccessService** cmdlet in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell) to remove the Service Connection Point (SCP) values from your Exchange servers. This step ensures no SCPs are returned, and the client instead uses the DNS method for Autodiscover.

    Exchange 2010 or 2013:

    ```powershell
    Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    ```

    Exchange 2016 or later:

    ```powershell
    Get-ClientAccessService | Set-ClientAccessService -AutoDiscoverServiceInternalUri $Null
    ```

    Note

    If you have Exchange 2007 servers, you need to run the `Get-ClientAccessServer | Set-ClientAccessServer...` command on those servers.
4. To prevent hybrid configuration objects from being recreated in the future, run the following command in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell):

    ```powershell
    Remove-HybridConfiguration
    ```
5. Remove all on-premises Exchange servers except for one (OK) or two (better) for user management.

    Tip

    You don't need a Database Availability Group (DAG) or other high availability options for the remaining Exchange servers.
6. Disable the OAuth configuration from the on-premises environment and Microsoft 365:

    - **On-premises Exchange**: Run the following command in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell):

        ```powershell
        Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
        ```
    - **Exchange Online**: Run the following command in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell):

        ```powershell
        Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        ```

    Note

    The *Identity* parameter value assumes you used the Hybrid Configuration wizard to configure OAuth. If not, you might need to use a different *Identity* value.
7. Do the following steps to delete the inbound and outbound connectors created by the Hybrid Configuration wizard:

    1. Open the Exchange admin center at https://admin.exchange.microsoft.com as an [Exchange Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#exchange-administrator) and go to **Mail Flow** &gt; **Connectors**. Or to go directly to the **Connectors** page, use https://admin.exchange.microsoft.com/#/connectors.
    2. On the **Connectors**page, disable or delete the inbound and outbound connectors created by the Hybrid Configuration wizard:
        - **Inbound from &lt;unique identifier&gt;**
        - **Outbound from &lt;unique identifier&gt;**
8. Remove the organization relationship created by the Hybrid Configuration wizard:

    1. Open the Exchange admin center at https://admin.exchange.microsoft.com at https://admin.exchange.microsoft.com as an [Exchange Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#exchange-administrator) and go to **Organization** &gt; **Sharing**. Or, to go directly to the **Sharing** page, use https://admin.exchange.microsoft.com/#/organizationsharing.
    2. On the **Sharing** page, remove the **O365 to On-Premises - &lt;unique identifier&gt;** relationship created by the Hybrid Configuration wizard.

Note

We recommended leaving the Exchange Hybrid Deployment feature enabled in cloud sync or Microsoft Entra Connect.

### Scenario 3: All cloud mailboxes with some on-premises email services

- **Scenario**: My organization has a hybrid configuration and now all mailboxes are in Exchange Online. I want to remove our on-premises Exchange servers, but we use Exchange for the following services:

    - SMTP relay for on-premises applications.
    - Access to public folders in on-premises Exchange.
- **Solution**: We recommend against removing Exchange and the hybrid configuration in this scenario.

    Pointing your Autodiscover DNS records to Exchange Online breaks features like hybrid public folder access.

    You can point your MX record to Microsoft 365 and reduce the number of on-premises Exchange servers. However, you need to keep enough on-premises Exchange servers to handle the remaining hybrid functions. And you need to maintain or migrate Exchange-only services and features (for example, public folders).

    If you plan to keep identity synchronization from Active Directory, you need to maintain one (OK) or two (better) on-premises Exchange servers for user management.