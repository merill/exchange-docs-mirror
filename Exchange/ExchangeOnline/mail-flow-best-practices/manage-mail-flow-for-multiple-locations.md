---
layout: Conceptual
title: Manage mail flow with mailboxes in multiple locations | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/manage-mail-flow-for-multiple-locations
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
ms.author: serdars
ms.topic: how-to
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: e1da5f2f-c732-4010-85c9-878b2cef3fb3
ms.collection:
- exchange-online
- M365-email-calendar
description: Learn how to manage mail flow in an Exchange hybrid environment - some mailboxes are on-premises and some are in Exchange Online.
f1.keywords:
- NOCSH
ms.reviewer: 
audience: ITPro
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 8b6130dd-6f13-b63d-2733-9bf91fd4a6e0
document_version_independent_id: 58835922-47d9-79df-0239-b38b53506193
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/manage-mail-flow-for-multiple-locations.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/manage-mail-flow-for-multiple-locations
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/manage-mail-flow-for-multiple-locations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: e229fb14-41b3-e359-f19c-7ac4c5d315c8
---

# Manage mail flow with mailboxes in multiple locations | Microsoft Learn

## Overview

This documentation provides detailed guidance on handling complex mail flow scenarios in environments that leverage Microsoft 365 or Office 365.

The examples described in this documentation use the fictitious organization, `Contoso`, which owns the domain `contoso.com`. The IP address of the Contoso email server is `172.17.17.231`, and its third-party provider uses `10.10.10.1` for their IP address. These are just examples. You can adapt these examples to fit your organization's domain name and public-facing IP address where necessary.

This documentation covers the following complex mail flow scenarios:

- Manage mail flow with mailboxes in multiple locations (Exchange Online and on-premises Exchange)
    - Overview
        - Important information
        - Scenario 1: MX record points to Microsoft 365 or Office 365 and Microsoft 365 or Office 365 filters all messages
            - Best practices
        - Scenario 2: MX record points to Microsoft 365 or Office 365 and mail is filtered on-premises
            - Best practices
        - Scenario 3: MX record points to my on-premises servers
            - Best practices
        - Scenario 4: MX record points to my on-premises server, which filters and provides compliance solutions for your messages. Your on-premises server needs to relay messages to the internet through Microsoft 365 or Office 365.
            - Best practices
    - See also

### Important information

In certain hybrid mail flow scenarios, customers may encounter situations in which outbound emails, originating from or relayed through their on-premises Exchange server or email gateway, are first routed through their Office 365 tenant. This occurs when the email gateway or on-premises Exchange server uses a specific certificate (for example, `gateway.contoso.com` or `exchange.contoso.com`), and the inbound connector created by the Hybrid Configuration Wizard (HCW) uses a default wildcard certificate configuration (`*.contoso.com`). Consequently, emails sent by the on-premises server or gateway are attributed to the Office 365 tenant before reaching recipients with MX records pointing to Exchange Online. Although unintended, this is the standard email attribution process for the matching Office 365 tenant. To understand how message attribution works in Microsoft 365, please read [Office 365 Message Attribution](https://techcommunity.microsoft.com/t5/exchange-team-blog/office-365-message-attribution/ba-p/749143).

Therefore, include `spf.protection.outlook.com` in your domain's SPF record, even if emails are sent directly from your on-premises server or gateway to the internet. If your tenant is not hosted in `Microsoft 365 Global` environment, the domain to include is different. You can find the correct entry for the respective environment in the [Set up SPF to identify valid email sources for your Microsoft 365 domain](/en-us/defender-office-365/email-authentication-spf-configure#spf-txt-records-for-custom-domains-in-microsoft-365) documentation.

If you want to change the routing behavior in this scenario, you can follow the steps outlined in the [FAQ #6(b) section of the "Office 365 Message Attribution"](https://techcommunity.microsoft.com/t5/exchange-team-blog/office-365-message-attribution/ba-p/749143) blog post.

### Scenario 1: MX record points to Microsoft 365 or Office 365 and Microsoft 365 or Office 365 filters all messages

- I'm migrating my mailboxes to Exchange Online, and I want to keep some mailboxes on my organization's email server (on-premises server). I want to use Microsoft 365 or Office 365 as my spam filtering solution and want to send my messages from my on-premises server to the internet by using Microsoft 365 or Office 365. Microsoft 365 or Office 365 sends and receives all messages.

Most customers who need a hybrid mail flow setup should allow Microsoft 365 or Office 365 to perform all their filtering and routing. We recommend that you point your MX record to Microsoft 365 or Office 365 because this setting provides for the most accurate spam filtering. For this scenario, your organization's mail flow setup looks like the following diagram.

![Mail flow diagram showing the scenario where your MX record points to Microsoft 365 or Office 365 and mail from the internet goes to Microsoft 365 or Office 365 and then to your on-premises servers. Mail traveling from your on-premises servers goes to Microsoft 365 or Office 365 and then to the internet.](../exchangeonline/media/38bcffa1-3f75-42de-9c06-85b0938a8d6e.png)

#### Best practices

1. Add your custom domains in Microsoft 365 or Office 365. To prove that you own the domains, follow the instructions in [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).
2. [Create user mailboxes in Exchange Online](../recipients-in-exchange-online/create-user-mailboxes) or [move all users' mailboxes to Microsoft 365 or Office 365](../mailbox-migration/mailbox-migration).
3. Update the DNS records for the domains that you added in step 1. (Not sure how to do this task? Follow the instructions on [this page](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).) The following DNS records control mail flow:

    - **MX record**: Point your MX record to Microsoft 365 or Office 365 in the following format: &lt;domainKey&gt;-com.mail.protection.outlook.com

        For example, if your domain is contoso.com, the MX record should be: contoso-com.mail.protection.outlook.com.
    - **SPF record**: This record should include the following senders:

        - Microsoft 365 or Office 365.
        - Your on-premises email servers that connect to Microsoft 365 or Office 365.
        - Non-Microsoft services that send email on behalf of your organization.

        For example, if the internet-facing IP address of on-premises email server is 172.17.17.231, the SPF record for contoso.com should be:

        ```text
        v=spf1 ip4:172.17.17.231 include:spf.protection.outlook.com -all
        ```

        Alternatively, depending on the non-Microsoft service requirements, you might need to include the domain from the non-Microsoft service. For example:

        ```text
        v=spf1 include:spf.protection.outlook.com include:non-microsoft_cloud_service.com -all
        ```
4. In the Exchange admin center (EAC), use the connector wizard to [Configure mail flow using connectors in Microsoft 365 or Office 365](use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow) for the following scenarios:

    - Sending messages from Microsoft 365 or Office 365 to your organization's email servers
    - Sending messages from your on-premises servers to Microsoft 365 or Office 365

        If either of the following scenarios apply to your organization, you must create a connector to support sending mail from your on-premises servers to Microsoft 365 or Office 365.
    - Your organization is authorized to send messages on behalf of your client, but your organization doesn't own the domain. For example, contoso.com is authorized to send email through fabrikam.com, which doesn't belong to contoso.com.
    - Your organization relays non-delivery reports (also known as NDRs or bounce messages) to the internet through Microsoft 365 or Office 365.

        To create the connector, choose the first option in the connector creation wizard on the **How should Office 365 identify email for your email server** screen, as shown in the below two screenshots, for New EAC and Classic EAC, respectively.

![The screen on which a connector is created to manage mail flow in multiple locations.](../exchangeonline/media/connector-to-manage-mfml.png)

![Screenshot showing the New Connector screen of the Hybrid Connection Wizard for Exchange.](../exchangeonline/media/0b3ced5f-3f0e-4cc3-aff4-f95e651189e0.png)

This configuration enables Microsoft 365 or Office 365 to identify your email server by using the certificate. In this scenario, the certificate CN or Subject Alternative Name (SAN) contains the domain that belongs to your organization. For more information, see [Identifying email from your email server](/en-us/previous-versions/exchange-server/exchange-150/dn910993%28v=exchg.150%29). For connector configuration details see, [Part 2: Configure mail to flow from your email server to Microsoft 365 or Office 365](use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail#part-2-configure-mail-to-flow-from-your-email-server-to-microsoft-365-or-office-365).

1. You don't need connectors in the following scenarios unless one of your partners has a special requirement, such as enforcing TLS with a bank.

    - Sending mail from Microsoft 365 or Office 365 to a partner organization
    - Sending mail from a partner organization to Microsoft 365 or Office 365

Note

If your organization's uses Exchange 2010 or later, we recommend that you use the [Hybrid Configuration Wizard](../hybrid-configuration-wizard) to configure connectors in Microsoft 365 or Office 365 as well as on your on-premises Exchange servers. For this scenario, your domain's MX record can't point to your organization's email server.

### Scenario 2: MX record points to Microsoft 365 or Office 365 and mail is filtered on-premises

- I'm migrating my mailboxes to Exchange Online and I want to keep some mailboxes on my organization's email server (on-premises server). I want to use the filtering and compliance solutions that are already in my on-premises environment. All messages that come from the internet to my cloud mailboxes, or messages sent to the internet from my cloud mailboxes, must route through my on-premises servers.

If you have business or regulatory reasons for filtering mail in your on-premises environment, we recommend pointing your domain's MX record to Microsoft 365 or Office 365 and enabling centralized mail transport. This setup provides optimal spam filtering and protects your organization's IP addresses. For this scenario, your organization's mail flow setup looks like the following diagram.

![Mail flow diagram showing the scenario where your MX record points to Microsoft 365 or Office 365 and filtering happens on your on-premises servers. Mail from the internet goes to Microsoft 365 or Office 365 and then to your servers for compliance filtering and then back to Microsoft 365 or Office 365.](../exchangeonline/media/61f59e52-2718-4da0-a196-c3691bd75763.png)

#### Best practices

1. Add your custom domains in Microsoft 365 or Office 365. To prove that you own the domains, follow the instructions in [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).
2. [Create user mailboxes in Exchange Online](../recipients-in-exchange-online/create-user-mailboxes) or [move all users' mailboxes to Microsoft 365 or Office 365](../mailbox-migration/mailbox-migration).
3. Update the DNS records for the domains that you added in step 1. (Not sure how to do this task? Follow the instructions on [this page](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).) The following DNS records control mail flow:

    - **MX record**: Point your MX record to Microsoft 365 or Office 365 in the following format: &lt;domainKey&gt;-com.mail.protection.outlook.com

    For example, if your domain is contoso.com, the MX record should be: contoso-com.mail.protection.outlook.com.

    - **SPF record**: This record should include the following senders:

        - Microsoft 365 or Office 365.
        - Your on-premises email servers that connect to Microsoft 365 or Office 365.
        - Non-Microsoft services that send email on behalf of your organization.

        For example, if the internet-facing IP address of on-premises email server is 172.17.17.231, the SPF record for contoso.com should be:

        ```text
        v=spf1 ip4:172.17.17.231 include:spf.protection.outlook.com -all
        ```
4. Use Centralized Mail Transport (CMT) for on-premises compliance solutions.

    - Mail that comes from the internet to a mailbox in Exchange Online first gets sent to your on-premises server and then comes back to Exchange Online to be delivered to the mailbox. Line 1 represents this path in the scenario 2 diagram.
    - Mail that comes from Exchange Online and is destined for the internet is first sent to your on-premises servers, then comes back to Exchange Online, and is then delivered to the internet. Line 4 represents this path in the scenario 2 diagram.
    - To achieve this configuration, create connectors via the [Hybrid Configuration Wizard](../hybrid-configuration-wizard) or via cmdlets, and enable CMT. For details about CMT, see [Transport Options in Exchange Hybrid Deployments](../transport-options).

You don't need connectors in the following scenarios unless one of your partners has special requirements, such as enforcing TLS with a bank.

- Sending mail from Microsoft 365 or Office 365 to a partner organization
- Sending mail from a partner organization to Microsoft 365 or Office 365

### Scenario 3: MX record points to my on-premises servers

- I'm migrating my mailboxes to Exchange Online, and I want to keep some mailboxes on my organization's email server (on-premises server). I want to use the filtering and compliance solutions that are already in my on-premises email environment. All messages that come from the internet to my cloud mailboxes, or messages sent to the internet from cloud mailboxes, must route through my on-premises servers. I need to point my domain's MX record to my on-premises server.

As an alternative to Scenario 2, you can point your domain's MX record to your organization's email server instead of to Microsoft 365 or Office 365. Some organizations have a business or regulatory need for this setup, but filtering typically works better if you use Scenario 2.

For this scenario, your organization's mail flow setup looks like the following diagram.

![Diagram showing mail flow when your MX record points to your on-premises servers instead of Microsoft 365 or Office 365. Mail goes from the internet to your organization's servers and then to Microsoft 365 or Office 365. Mail goes from Microsoft 365 or Office 365 to your on-premises servers to internet.](../exchangeonline/media/500e199e-ad94-42e7-ac04-d4f46b59fee2.png)

#### Best practices

If the MX record for your domain needs to point to your on-premises IP address, use the following best practices:

1. Add your custom domains in Microsoft 365 or Office 365. To prove that you own the domains, follow the instructions in [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).
2. [Create user mailboxes in Exchange Online](../recipients-in-exchange-online/create-user-mailboxes) or [move all users' mailboxes to Microsoft 365 or Office 365](../mailbox-migration/mailbox-migration).
3. Update the DNS records for the domains that you added in step 1. (Not sure how to do this task? Follow the instructions on [this page](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).) The following DNS records control mail flow:

    - **SPF record**: This record should include the following senders:

        - Microsoft 365 or Office 365.
        - Your on-premises email servers that connect to Microsoft 365 or Office 365.
        - Non-Microsoft services that send email on behalf of your organization.

        For example, if the internet-facing IP address of on-premises email server is 172.17.17.231, the SPF record for contoso.com should be:

        ```text
        v=spf1 ip4:172.17.17.231 include:spf.protection.outlook.com -all
        ```
4. Because you're not relaying messages from your on-premises servers to the internet through Microsoft 365 or Office 365, you don't technically need to create connectors for the following scenarios. But if at some point you change your MX record to point to Microsoft 365 or Office 365, you'll need to create connectors; therefore, it's best to do it up front. In the Exchange admin center, use the connector wizard to [Part 2: Configure mail to flow from your email server to Microsoft 365 or Office 365](use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail#part-2-configure-mail-to-flow-from-your-email-server-to-microsoft-365-or-office-365) for the following scenarios, or use the [Hybrid Configuration Wizard](../hybrid-configuration-wizard) to create connectors:

    - Sending mail from Microsoft 365 or Office 365 to your organization's email servers
    - Sending mail from your on-premises servers to Microsoft 365 or Office 365
5. To make sure that messages are sent to your organization's on-premises servers through MX, go to [Example security restrictions you can apply to email sent from a partner organization](use-connectors-to-configure-mail-flow/set-up-connectors-for-secure-mail-flow-with-a-partner#examplesecurityrestrict), and follow "Example 3: Require that all email from your partner organization domain ContosoBank.com is sent from a specific IP address range."

### Scenario 4: MX record points to my on-premises server, which filters and provides compliance solutions for your messages. Your on-premises server needs to relay messages to the internet through Microsoft 365 or Office 365

- I'm migrating my mailboxes to Exchange Online, and I want to keep some mailboxes on my organization's email server (on-premises server). I want to use the filtering and compliance solutions that are already in my on-premises email environment. All messages sent from my on-premises servers must relay through Microsoft 365 or Office 365 to the internet. I need to point my domain's MX record to my on-premises server.

For this scenario, your organization's mail flow setup looks like the following diagram.

![Mail flow diagram with arrows showing mail from the internet to on-premises servers and then to Microsoft 365 or Office 365. Also shows email travelling from on-premises servers to Microsoft 365 or Office 365 to the internet.](../exchangeonline/media/60d0655c-eff8-441f-9911-7f8b4cc06fe5.png)

#### Best practices

If the MX record for your domain needs to point to your on-premises IP address, use the following best practices:

1. Add your custom domains in Microsoft 365 or Office 365. To prove that you own the domains, follow the instructions in [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).
2. [Create user mailboxes in Exchange Online](../recipients-in-exchange-online/create-user-mailboxes) or [move all users' mailboxes to Microsoft 365 or Office 365](../mailbox-migration/mailbox-migration).
3. Update the DNS records for the domains that you added in step 1. (Not sure how to do this task? Follow the instructions on [this page](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).) The following DNS records control mail flow:

    - **MX record**: Point your MX record to your on-premises server in the following format: mail.&lt;domainKey&gt;.com

        For example, if your domain is contoso.com, the MX record should be: .mail.contoso.com.
    - **SPF record**: This record should include the following senders:

        - Microsoft 365 or Office 365.
        - Your on-premises email servers that connect to Microsoft 365 or Office 365.
        - Non-Microsoft services that send email on behalf of your organization.

        For example, if the internet-facing IP address of on-premises email server is 172.17.17.231, the SPF record for contoso.com should be:

        ```text
        v=spf1 ip4:172.17.17.231 include:spf.protection.outlook.com -all
        ```
4. In the EAC, use the connector wizard to [Configure mail flow using connectors in Microsoft 365 or Office 365](use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow) for the following scenarios:

    - Sending mail from Microsoft 365 or Office 365 to your organization's email servers
    - Sending mail from your on-premises servers to Microsoft 365 or Office 365

        Create a connector to support the scenario "Sending mail from your on-premises servers to Microsoft 365 or Office 365" if any of the following scenarios apply to your organization:
    - Your organization is authorized to send mail on behalf of your client, but your organization doesn't own the domain. For example, contoso.com is authorized to send email through fabrikam.com, which doesn't belong to contoso.com.
    - Your organization relays non-delivery reports (NDRs) to the internet through Microsoft 365 or Office 365.
    - The MX record for your domain, contoso.com, points to your on-premises server, and users in your organization automatically forward messages to email addresses outside your organization. For example, `kate@contoso.com` has forwarding enabled, and all messages go to `kate@tailspintoys.com`. If `john@fabrikam.com` sends a message to `kate@contoso.com`, by the time the message arrives at Microsoft 365 or Office 365, the sender domain is fabrikam.com and the recipient domain is tailspin.com. The sender domain and recipient domain don't belong to your organization.

        To create the connector, choose the first option in the connector creation wizard on the **How should Microsoft 365 or Office 365 identify email for your email server** screen, as shown in the below two screenshots, for New EAC and Classic EAC, respectively.

![The screen on which a connector is created to manage mail flow in multiple locations.](../exchangeonline/media/connector-to-manage-mfml.png)

![Screenshot showing the New Connector screen of the Hybrid Connection Wizard for Exchange.](../exchangeonline/media/0b3ced5f-3f0e-4cc3-aff4-f95e651189e0.png)

This option allows Microsoft 365 or Office 365 to identify your email server by using the certificate. In this scenario, the certificate CN or Subject Alternative Name (SAN) contains the domain that belongs to your organization. For more information, see [Identifying email from your email server](/en-us/previous-versions/exchange-server/exchange-150/dn910993%28v=exchg.150%29). For connector configuration details see, [Part 2: Configure mail to flow from your email server to Microsoft 365 or Office 365](use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail#part-2-configure-mail-to-flow-from-your-email-server-to-microsoft-365-or-office-365).

1. [Set up connectors for secure mail flow with a partner organization](use-connectors-to-configure-mail-flow/set-up-connectors-for-secure-mail-flow-with-a-partner) to make sure that messages are sent to your organization's on-premises servers via MX.