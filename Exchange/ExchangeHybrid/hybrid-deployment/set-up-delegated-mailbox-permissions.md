---
layout: Conceptual
title: Configure Exchange to support delegated mailbox permissions in a hybrid deployment | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/set-up-delegated-mailbox-permissions
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
- Hybrid
- M365-email-calendar
ms.assetid: a2a10cb3-4557-4ff5-8191-c653522f4512
ms.reviewer: 
description: Admins can learn about the Exchange configuration settings that are required to support delegated mailbox permissions in a hybrid environment.
ms.date: 2025-03-07T00:00:00.0000000Z
locale: en-us
document_id: b1d8bb0b-6656-9565-598c-4b82018f6a1c
document_version_independent_id: fca6d1ff-0764-fcf6-d459-16473131f3a0
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/set-up-delegated-mailbox-permissions.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/set-up-delegated-mailbox-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/set-up-delegated-mailbox-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 99126201-3a74-bdd8-8f7e-bce8c6741ae7
---

# Configure Exchange to support delegated mailbox permissions in a hybrid deployment | Microsoft Learn

Delegated mailbox permissions enable someone to manage some part of another user's mailbox. A common example of this scenario is an administrative assistant who needs to manage an executive's mailbox and calendar. Hybrid deployments between an on-premises Exchange organization and Microsoft 365 or Office 365 support the **Full Access** and **Send on Behalf** delegated mailbox permissions. However, depending on the version of Exchange in your on-premises organization, you might need extra configuration to use delegated mailbox permissions in a hybrid deployment. For example:

- **Exchange 2019**: Extra configuration is required.
- **Exchange 2016**: Extra configuration is required.
- **Exchange 2013**: A supported Exchange 2013 Cumulative Update (CU) and extra configuration is required.
- **Exchange 2010**: Not supported anymore.

For more information about the specific requirements to support delegated mailbox permissions in a hybrid deployment, take a look at [Permissions in Exchange hybrid deployments](../permissions).

The following sections step you through the configuration of Exchange 2013, Exchange 2016 and Exchange 2019 on-premises deployments to enable support for delegated mailbox permissions. Before you follow these steps, you need to make sure you're on the latest Exchange 2013/2016/2019 CU. For more information, see [Hybrid deployment prerequisites](../hybrid-deployment-prerequisites).

## Exchange 2013, Exchange 2016 And Exchange 2019

The following table describes the requirements to enable support for delegated mailbox permissions based on the environment when you moved mailboxes to the cloud:

| Exchange Server version | ACLable object synchronization enabled or disabled | Action required |
| --- | --- | --- |
| Exchange 2013 CU9 or earlier | n/a | Manually configure each mailbox to support Access Control Lists (ACLs) |
| Exchange 2013 CU10 or later | Disabled | Enable ACLable object synchronization at the organization level  Manually enable ACLs on each mailbox moved to the cloud before ACLable object synchronization was enabled at the organization level.  No extra configuration is needed for mailboxes moved to the cloud after ACLable object synchronization is enabled at the organization level. |
| Exchange 2013 CU10 or later | Enabled | No extra configuration is needed. |
| Exchange 2016 | Disabled | Enable ACLable object synchronization at the organization level  Manually enable ACLs on each mailbox moved to the cloud before ACLable object synchronization was enabled at the organization level.  No extra configuration is needed for mailboxes moved to the cloud after ACLable object synchronization is enabled at the organization level. |
| Exchange 2016 | Enabled | No extra configuration is needed. |
| Exchange 2019 | Disabled | Enable ACLable object synchronization at the organization level  Manually enable ACLs on each mailbox moved to the cloud before ACLable object synchronization was enabled at the organization level.  No extra configuration is needed for mailboxes moved to the cloud after ACLable object synchronization is enabled at the organization level. |
| Exchange 2019 | Enabled | No extra configuration is needed. |

### Enable ACLable object synchronization

To enable ACLable object synchronization at the organization level, do the following.

1. Install the latest version of Microsoft Entra Connect (Microsoft Entra Connect) on all of your Microsoft Entra Connect servers. This is needed to allow Microsoft Entra Connect to synchronize the attributes needed to support hybrid permissions. You can download Microsoft Entra Connect from [Microsoft Entra Connect](https://www.microsoft.com/download/details.aspx?id=47594).
2. Open the Exchange Management Shell on an Exchange 2013 or Exchange 2016 or Exchange 2019 server running the latest available CU, or the immediately previous CU.
3. Run the following command.

    ```PowerShell
    Set-OrganizationConfig -ACLableSyncedObjectEnabled $True
    ```

After you do this step, any mailboxes that you move to the cloud will be properly configured to support delegated mailbox permissions. If mailboxes were moved to the cloud before completing these steps, you need to manually enable ACLs on those mailboxes using the steps in Enable ACLs on remote mailboxes.

Important

ACLs aren't enabled on remote mailboxes created in the cloud. If you create a remote mailbox in the cloud via on-premises Exchange, you need to use the ACLableSyncedObjectEnabled parameter when running New-RemoteMailbox or Enable-RemoteMailbox.

### Enable ACLs on remote mailboxes

To enable ACLs on mailboxes moved to the cloud before ACLable object synchronization was enabled at the organization level, do the following.

1. Open the Exchange Management Shell on an Exchange 2013 or Exchange 2016 or Exchange 2019 server running the latest available CU, or the immediately previous CU.
2. To enable ACLs on a single mailbox, run the following command:

    ```PowerShell
    Set-RemoteMailbox <UserMailbox's Identity> -ACLableSyncedObjectEnabled
    ```
3. To enable ACLs on all mailboxes moved to the cloud, run the following command:

    ```PowerShell
    Get-RemoteMailbox -ResultSize unlimited | Set-RemoteMailbox -ACLableSyncedObjectEnabled
    ```
4. To verify that the mailboxes have been successfully updated, run the following command:

    ```PowerShell
    Get-RemoteMailbox -ResultSize unlimited | Format-Table DistinguishedName,msExchRecipientDisplayType -AutoSize
    ```