---
layout: Conceptual
title: Manage mail flow using a third-party cloud service with Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/manage-mail-flow-using-third-party-cloud
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
description: A couple of different scenarios that illustrate how to configure Exchange Online mail flow through a third-party cloud service.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: d0d10ab1-08c1-4ffe-aaa5-f9dbd9a118ed
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: dc3d3a13-1d99-fa59-d1e0-6262eac0a985
document_version_independent_id: 54659913-2547-f6ce-e8df-bbecd97c61f5
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/manage-mail-flow-using-third-party-cloud.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/manage-mail-flow-using-third-party-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/manage-mail-flow-using-third-party-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 35b897a3-ca73-985b-8a0c-0fb52fd5ea88
---

# Manage mail flow using a third-party cloud service with Exchange Online | Microsoft Learn

This topic covers the following complex mail flow scenarios using Exchange Online:

Scenario 1 - MX record points to third-party spam filtering

Scenario 2 - MX record points to third-party solution without spam filtering

Note

Examples in this topic use the fictitious organization, Contoso, which owns the domain contoso.com and is a tenant in Exchange Online. This is just an example. You can adapt this example to fit your organization's domain name and third-party service IP addresses where necessary.

## Using a third-party cloud service with Microsoft 365 or Office 365

### Scenario 1 - MX record points to third-party spam filtering

Important

Microsoft strongly recommends that you enable Enhanced Filtering for Connectors or bypass filtering completely using a mail flow rule (check out point 5). Failure to follow this step inevitably results in misclassification of inbound main into your organization, and a subpar experience for Microsoft 365 email and protection features.

Microsoft also recommends that you add third-party services that modify messages in transit as [Trusted ARC sealers](/en-us/defender-office-365/email-authentication-arc-configure), if the service supports ARC sealing. Add the service as a trusted ARC sealer helps affected messages pass email authentication checks, and helps prevent legitimate messages from being delivered to the Junk Email folder, quarantined, or rejected. Third-party services that modify messages and don't support ARC sealing will invalidate the DKIM signatures of those messages. In these cases, you should review the [Spoof detections report](/en-us/defender-office-365/reports-email-security#spoof-detections-report) and [create allow entries for spoofed senders](/en-us/defender-office-365/tenant-allow-block-list-email-spoof-configure#create-allow-entries-for-spoofed-senders) to override email authentication failures for legitimate messages.

I plan to use Exchange Online to host all my organization's mailboxes. My organization uses a third-party cloud service for spam, malware, and phish filtering. All email from the internet must first be filtered by this third-party cloud service before being routed to Microsoft 365 or Office 365.

For this scenario, your organization's mail flow setup looks like the following diagram:

![Mail flow diagram showing inbound email from the internet to a third-party filtering service to Microsoft 365 or Office 365 and from outbound mail from Microsoft 365 or Office 365 to the internet.](../exchangeonline/media/a8ee0cd5-6a4c-4e57-9030-0f233def25f3v2.png)

#### Best practices for using a third-party cloud filtering service with Microsoft 365 or Office 365

1. Add your custom domains in Microsoft 365 or Office 365. To prove that you own the domains, follow the instructions in [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).
2. [Create user mailboxes in Exchange Online](../recipients-in-exchange-online/create-user-mailboxes) or [move all users' mailboxes to Microsoft 365 or Office 365](../mailbox-migration/mailbox-migration).
3. Update the DNS records for the domains that you added in step 1. (Not sure how to do this? Follow the instructions on [this page](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).) The following DNS records control mail flow:

    - **MX record**: Your domain's MX record must point to your third-party service provider. Follow their guidelines for how to configure your MX record.
    - **SPF record**: All mail sent from your domain to the internet originates in Microsoft 365 or Office 365, so your SPF record requires the standard value for Microsoft 365 or Office 365:

        ```text
        v=spf1 include:spf.protection.outlook.com -all
        ```

        You would only need to include the third-party service in your SPF record if your organization sends **outbound** internet email through the service (where the third-party service would be a source for email from your domain).

    When you're configuring this scenario, the "host" that you need to configure to receive email from the third-party service is specified in the **MX Record**. For example:

    ![Example host name value.](../exchangeonline/media/thirdpartyhostconfig.png)

    In this example, the host name for the Microsoft 365 or Office 365 host should be **hubstream-mx.mail.protection.outlook.com**. This value can vary from domain to domain, so check your value at **Configuration** &gt; **Domain** &gt; &lt;select domain&gt; to confirm your actual value.
4. Lock down your Exchange Online organization to only accept mail from your third-party service.

    Create and configure a **Partner** inbound connector using either *TlsSenderCertificateName* (preferred) or *SenderIpAddresses* parameters, then set the corresponding *RestrictDomainsToCertificate* or *RestrictDomainsToIPAddresses* parameters to $True. Any messages that are smart-host routed directly to Exchange Online will be rejected (because they didn't arrive over a connection using specified certificate or from the specified IP addresses).

    For example:

    ```powershell
    New-InboundConnector -Name "Reject mail not routed through MX (third-party service name)" -ConnectorType Partner -SenderDomains * -RestrictDomainsToCertificate $true -TlsSenderCertificateName *.contoso.com -RequireTls $true
    ```

    or

    ```powershell
    New-InboundConnector -Name "Reject mail not routed through MX (third-party service name)" -ConnectorType Partner -SenderDomains * -RestrictDomainsToIPAddresses $true -SenderIpAddresses <#static list of on-premises IPs or IP ranges of the third-party service>
    ```

    Note

    If you already have an **OnPremises** inbound connector for the same certificate or sender IP addresses, you still need to create the **Partner** inbound connector (the *RestrictDomainsToCertificate* and *RestrictDomainsToIPAddresses* parameters are only applied to **Partner** connectors). The two connectors can coexist without problems.
5. There are two options for this step:

    - **Use Enhanced Filtering for Connectors (highly recommended)**: Use [Enhanced Filtering for Connectors](use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors) (also known as skip listing) on the Partner inbound connector that receives messages from the third-party application. This allows cloud email protection scanning on the messages.

        Note

        For hybrid scenarios where third-party applications rely on an on-premises Exchange server to send to Exchange Online, you also need to enable Enhanced Filtering for Connectors on the **OnPremises** inbound connector in Exchange Online.
    - **Bypass spam filtering**: Use a mail flow rule (also known as a transport rule) to bypass spam filtering. This option prevents most cloud email protection controls and therefore prevents double anti-spam checks.

        ![Mail flow rule to prevent double-scanning.](../exchangeonline/media/transportrulefor3rdparty.png)

        Important

        Instead of bypassing spam filtering using a mail flow rule, we highly recommend that you enable [Enhanced Filtering for Connector (also known as Skip Listing)](use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors). Most third-party cloud anti-spam providers share IP addresses among many customers. Bypassing scanning on these IPs might allow spoofed and phishing messages from these IP addresses.

### Scenario 2 - MX record points to third-party solution without spam filtering

I plan to use Exchange Online to host all my organization's mailboxes. All email that's sent to my domain from the internet must first flow through a third-party archiving or auditing service before arriving in Exchange Online. All outbound email that's sent from my Exchange Online organization to the internet must also flow through the service. However, the service doesn't provide a spam filtering solution.

This scenario requires you to use [Enhanced Filtering for Connectors](use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors). Otherwise, mail from all internet senders appears to originate from the third-party service, not from the true sources on the internet.

![Mail flow diagram showing inbound mail from the internet to a third-party solution to Office 365 or Microsoft 365, and showing outbound mail from Microsoft 365 or Office 365 to the third-party solution and then to the internet.](../exchangeonline/media/05300b2e-1223-4eb2-87df-b3370fac9f91_2.png)

#### Best practices for using a third-party cloud service with Microsoft 365 or Office 365

We strongly recommend that you use the archiving and auditing solutions that are provided by Microsoft 365 and Office 365.

Important

There is a 3rd scenario where MX record points to Microsoft 365, however, the third-party service operates after Microsoft 365. In this setup, emails leave the Microsoft 365 environment and are routed to the third-party service for spam, malware, and phishing filtering. Once filtered, the messages return to Microsoft 365. For more details on this setup, including its challenges and complexities, refer to the article [Integration via in-and-out mail routing](/en-us/defender-office-365/mdo-integrate-security-service#integration-via-in-and-out-mail-routing)