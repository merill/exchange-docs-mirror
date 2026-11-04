---
layout: Conceptual
title: Enable mail flow for subdomains in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/enable-mail-flow-for-subdomains
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
description: Admins can learn how to enable mail flow for subdomains in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 4033a30a-f506-481c-8ef0-fd9a0508ae38
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
f1.keywords:
- NOCSH
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 56e4d207-3c34-02c7-5a9b-3689267c866a
document_version_independent_id: c086dd8e-8fc4-fc3b-de38-ec4b13968d13
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/manage-accepted-domains/enable-mail-flow-for-subdomains.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/manage-accepted-domains/enable-mail-flow-for-subdomains
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/manage-accepted-domains/enable-mail-flow-for-subdomains.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 2c0588b0-7827-8ea6-9e38-19604913997f
---

# Enable mail flow for subdomains in Exchange Online | Microsoft Learn

If you have a hybrid environment, with mailboxes hosted both in Exchange Online and on-premises Exchange, and you have subdomains of the accepted domains that only exist in your on-premises environment, you can enable email flow to and from these on-premises subdomains. For example, if you have an accepted domain called Contoso.com, and you enable match subdomains, users can send email to, or receive email from all subdomains of Contoso.com that exist in your on-premises environment, such as marketing.contoso.com and nwregion.contoso.com. In Microsoft Forefront Online Protection for Exchange (FOPE), this feature was called *catch-all domains*.

Important

- If you have a limited number of subdomains, and know all the subdomain names, we recommend setting up each subdomain as an accepted domain in the Microsoft 365 admin center, instead of using the procedures in this topic. By setting up each subdomain separately, you can have finer control over mail flow and can include unique mail flow rules (also known transport rules) for each subdomain. For more information about adding a domain in the Microsoft 365 admin center, see [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).
- In order to enable match subdomains, an accepted domain must be set up as an internal relay domain. For information about setting the domain type to internal relay, see [Manage accepted domains in Exchange Online](manage-accepted-domains).
- In order to send email to public folders within your Exchange Online environment, you need to set the domain type to internal relay if the domain contains recipient addresses assigned to public folders. Directory-Based Edge Blocking cannot be used for public folders.
- After you enable match subdomains, in order for the service to deliver mail for all subdomains to your organization's email server (outside Microsoft 365 or Office 365), you must also change the connector that is used for transmitting messages from Office 365 to your organization's email server. For instructions, see Use the EAC to add the domain to the connector used for transmitting messages from Office 365 to your organization's email server.

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes
- You need permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Domains" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use the Exchange admin center (EAC) to set up match subdomains on a domain

### Set up match subdomains in EAC

1. Navigate to **Mail Flow** &gt; **Accepted domains**. The **Accepted domains** screen appears.

    ![The screen displaying accepted domains.](../../exchangeonline/media/accepted-domains.png)
2. Select an accepted domain and click it. The accepted domain's details screen appears.
3. Verify that **Internal Relay** is selected. If **Authoritative** is selected, change it to **Internal Relay**.

    ![The screen on which the INTERNAL RELAY option is chosen.](../../exchangeonline/media/setting-internal-relay.png)
4. Check the check box for **Accept mail for all subdomains**.

    ![The screen on which the user configures acceptance of emails from all subdomains.](../../exchangeonline/media/setting-email-acceptance-for-all-subdomains.png)
5. Click **Save**.

The accepted domain is updated successfully.

## Use the EAC to add the domain to the connector used for transmitting messages from Office 365 to your organization's email server

### Add the domain connector in EAC

1. Navigate to **Mail Flow** &gt; **Connectors**.
2. Select a connector that is used for transmitting messages from Office 365 to your organization's email server.
3. Click the connector. The connector properties screen appears.
4. In the connector properties screen that appears, under **Use of connector**, click **Edit use**.
5. In the **Use of connector** screen that appears, select **Only when email messages are sent to these domains**.

    ![The option on the New EAC screen to choose when the connector can be used.](../../exchangeonline/media/determining-timing-of-connector-new-eac.png)
6. In the text box, enter the name of the domain to which you want to apply the connector. For example, **\*.contoso.com**.
7. Click **+**.
8. Click **Next**.
9. In the **Validation email** screen that appears, In the text box, enter the email of an active mailbox on your organization's server.
10. Once the validation process is completed, click **Save**.

## Use Exchange Online PowerShell to set up match-subdomains on a domain

To add the match subdomains to a domain that is set up as an internal relay, use this syntax:

```powershell
Set-AcceptedDomain -Identity <Domain Name> -MatchSubdomains $true
```

This example sets up match subdomains for the contoso.com domain.

```powershell
Set-AcceptedDomain -Identity contoso.com -MatchSubdomains $true
```

For detailed syntax and parameter information, see [Set-AcceptedDomain](/en-us/powershell/module/exchangepowershell/set-accepteddomain).