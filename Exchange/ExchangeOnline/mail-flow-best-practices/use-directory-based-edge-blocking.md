---
layout: Conceptual
title: Use Directory-Based Edge Blocking to reject messages sent to invalid recipients in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-directory-based-edge-blocking
Manager: serdars
ms.subservice: exo-mail-flow
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
ms.author: serdars
ms.topic: how-to
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: ca7b7416-92ed-40ad-abdb-695be46ea2e4
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
description: Admins can learn how to configure Directory-Based Edge Blocking (DBDB) to reject messages sent to invalid recipients in Microsoft 365 during a migration.
f1.keywords:
- NOCSH
audience: ITPro
ms.date: 2024-06-04T00:00:00.0000000Z
locale: en-us
document_id: eeb394c8-1004-a253-7806-71fdc9406478
document_version_independent_id: 1f4e3200-3025-5def-851e-3d56f815c2ff
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-directory-based-edge-blocking.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-directory-based-edge-blocking
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-directory-based-edge-blocking.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 0792ba99-17e9-be66-cfb5-3b0d83cbe8ef
---

# Use Directory-Based Edge Blocking to reject messages sent to invalid recipients in Exchange Online | Microsoft Learn

Directory-Based Edge Blocking (DBEB) lets you reject messages for invalid recipients at the service network perimeter in Microsoft 365.

If a message is sent to a valid email address in Microsoft 365 or Office 365, the message continues through the rest of the service filtering layers: anti-malware, anti-spam, and mail flow rules (also known as transport rules). If the address doesn't exist, the service blocks the message before filtering even occurs, and a non-delivery report (also known as an NDR or *bounce message*) is returned to the sender. The NDR looks like this: `550 5.4.1 Recipient address rejected: Access denied`.

**If all recipients for your domain are in Exchange Online, DBEB is already in effect, and you don't need to do anything**. If you're migrating from another email system to Exchange Online, you can use the procedure in this topic to enable DBEB for the domain before the migration.

Note

- In hybrid environments, in order for DBEB to work, the MX record for the domain must point to Microsoft 365 or Office 365 so that email for the domain is routed to Microsoft 365 or Office 365 first.
- There are additional considerations when using DBEB with on-premises mail-enabled public folders. For more information about DBEB and mail-enabled public folders, see [Office 365 Directory Based Edge Blocking support for on-premises Mail Enabled Public Folders](https://techcommunity.microsoft.com/blog/exchange/directory-based-edge-blocking-now-available-for-public-folders--dynamic-distribu/4421006).

## What do you need to know before you begin?

- Estimated time to complete: 5 to 10 minutes
- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../exchange-admin-center).
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Configure DBEB

This section describes the procedure to configure DBEB for both the New Exchange admin center (EAC) and Classic EAC.

**For New EAC**

1. Verify that your accepted domain in Exchange Online is set to **Internal relay**:

    a. Navigate to **Mail flow** &gt; **Accepted domains**. The **Accepted domains** screen appears.

    b. Select an accepted domain and click it. The accepted domain's details screen appears.

    c. Ensure that the domain type is set to **Internal relay**. If it's set to **Authoritative**, change it to **Internal relay**.

    d. Click **Save**.
2. Add users to Microsoft 365 or Office 365. For example:

    - **Directory synchronization**: Add valid users to Office 365 by synchronizing from your on-premises Active Directory environment to [Microsoft Entra ID](/en-us/azure/active-directory/) in the cloud. For more information about how to set up directory synchronization, see [Use directory synchronization to manage mail users](../recipients-in-exchange-online/manage-mail-users#use-directory-synchronization-to-manage-mail-users).
    - **Add users via PowerShell or the EAC**: For more information about how to do this task, see [Manage mail users in Exchange Online)](../recipients-in-exchange-online/manage-mail-users).
3. Set your accepted domain in Exchange Online to **Authoritative**:

    a. Navigate to **Mail flow** &gt; **Accepted domains**. The **Accepted domains** screen appears.

    b. Select an accepted domain and click it. The accepted domain's details screen appears.

    c. Ensure that the domain type is set to **Authoritative**. If it's set to **Internal relay**, change it to **Authoritative**.

    d. Click **Save**.

**For Classic EAC**

1. Verify that your accepted domain in Exchange Online is set to **Internal relay**:

    a. Navigate to **Mail flow** &gt; **Accepted domains**.

    b. Select an accepted domain and click **Edit**.

    c. Ensure that the domain type is set to **Internal relay**. If it's set to **Authoritative**, change it to **Internal relay**.

    d. Click **Save**.
2. Add users to Microsoft 365 or Office 365. For example:

    - **Directory synchronization**: Add valid users to Office 365 by synchronizing from your on-premises Active Directory environment to [Microsoft Entra ID](/en-us/azure/active-directory/) in the cloud. For more information about how to set up directory synchronization, see [Use directory synchronization to manage mail users](../recipients-in-exchange-online/manage-mail-users#use-directory-synchronization-to-manage-mail-users).
    - **Add users via PowerShell or the EAC**: For more information about how to do this task, see [Manage mail users in Exchange Online](../recipients-in-exchange-online/manage-mail-users).
3. Set your accepted domain in Exchange Online to **Authoritative**:

    a. Navigate to **Mail flow** &gt; **Accepted domains**.

    b. Select an accepted domain and click **Edit**.

    c. Set the domain type to **Authoritative**.

    d. Click **Save**.
4. Choose **Save** to save your changes, and confirm that you want to enable DBEB.

Note

- Dynamic distribution groups created in Exchange on-premises don't sync to Exchange Online and are therefore blocked by DBEB. As a workaround in hybrid environments, you can create a mail contact with the same external email address of the blocked dynamic distribution group in Exchange Online.
- Until all of your valid recipients have been added to Exchange Online and replicated through the system, you should leave the accepted domain configured as **Internal relay**. Once the domain type has been changed to **Authoritative**, DBEB is designed to allow any SMTP address that has been added to the service. There might be infrequent instances where recipient addresses that don't exist in your Microsoft 365 or Office 365 organization are allowed to relay through the service.