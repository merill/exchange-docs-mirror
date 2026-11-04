---
layout: Conceptual
title: Enhanced filtering for connectors in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors
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
description: Learn how to use Enhanced Filtering for Connectors (also known as skip listing) if your organization sends mail to a non-Microsoft service or device before Microsoft 365.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.custom: msecd-doc-authoring-1015
ms.date: 2026-10-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 1bd501e4-be27-1da8-e250-7cc1ac22c8ec
document_version_independent_id: ada2e5a7-646f-3576-5834-4727151b7743
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: c8847457-b291-0a99-8d8b-ebb9837229fa
---

# Enhanced filtering for connectors in Exchange Online | Microsoft Learn

Properly configured inbound connectors are a trusted source of incoming mail to Microsoft 365. But in complex routing scenarios where email for your Microsoft 365 domain is routed somewhere else first, the source of the inbound connector is typically not the true indicator of where the message came from. Complex routing scenarios include:

- Non-Microsoft cloud filtering services.
- Managed filtering appliances.
- Hybrid environments (for example, with on-premises Exchange).

Mail routing in complex scenarios looks like this:

![Mail flow diagram for complex routing scenarios.](../../exchangeonline/media/enhanced-filtering-for-connectors-before.png)

As you can see, the message adopts the source IP of the last hop that sits in front of Microsoft 365. The message arrives in Microsoft 365 with a different source IP address. This behavior isn't a limitation of Microsoft 365; it's simply how SMTP works.

In these scenarios, you can still get the most out of [Built-in security features for all cloud mailboxes](/en-us/defender-office-365/eop-about) and [Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-about) by using Enhanced Filtering for Connectors (also known as *skip listing*).

After you enable Enhanced Filtering for Connectors, mail routing in complex routing scenarios looks like this:

![Mail flow diagram for complex routing scenarios after Enhance Filtering for Connectors is enabled.](../../exchangeonline/media/enhanced-filtering-for-connectors-after.png)

As you can see, Enhanced Filtering for connectors preserves the source IP address and sender information.

In these routing scenarios, you typically use an [ARC seal](/en-us/defender-office-365/email-authentication-arc-configure) to maintain the source information and message integrity using DKIM. However, many services that modify the message don't support ARC. To help in these situations, Enhanced Filtering for Connectors not only preserves the IP address from the previous hop but also intelligently recovers from DKIM signature failures. This behavior helps the messages pass authentication through the spoof intelligence filters.

Enhanced Filtering for Connectors has the following benefits:

- Improved accuracy for the Microsoft filtering stack and machine learning models, which include:
    - Reduced false positives in DMARC from content modification and lack of an ARC seal.
    - Heuristic clustering
    - Anti-spoofing
    - Anti-phishing
- Better post-breach capabilities in [Automated investigation and response (AIR)](/en-us/defender-office-365/air-about)
- Able to use explicit email authentication (SPF, DKIM, and DMARC) to verify the reputation of the sending domain for impersonation and spoof detection. For more information about explicit and implicit email authentication, see [Email authentication in Microsoft 365](/en-us/defender-office-365/email-authentication-about).

For more information, see the What happens when you enable Enhanced Filtering for Connectors? section later in this article.

Use the procedures in this article to enable Enhanced Filtering for Connectors on individual connectors. For more information about connectors in Exchange Online, see [Configure mail flow using connectors](use-connectors-to-configure-mail-flow).

Note

- Enhanced Filtering for Connectors is intended for scenarios where the MX record for the domain doesn't point to Microsoft 365. For example:
    - Hybrid environments where internet mail is routed through the on-premises Exchange environment before being delivered to Microsoft 365. Microsoft 365 doesn't scan mail sent to on-premises recipients.
    - Internet mail is routed through a non-Microsoft service or device before delivery to Microsoft 365 recipients as described in [MX record points to non-Microsoft spam filtering](/en-us/exchange/mail-flow-best-practices/manage-mail-flow-using-third-party-cloud#scenario-1---mx-record-points-to-third-party-spam-filtering).
- Enhanced Filtering for Connectors isn't intended for non-Microsoft services or devices that scan mail *after* Microsoft 365. Once Microsoft 365 scans a message, be careful not to break the chain of trust by routing mail through any non-Exchange server that isn't part of your cloud or on-premises organization. When the message eventually arrives at the destination mailbox, the headers from the first scanning verdict might no longer be accurate.
- In *non-linear inbound routing* scenarios in [Centralized Mail Transport](../../transport-options), adding on-premises hybrid servers to Enhanced Filtering for Connectors isn't supported. This configuration can cause Microsoft 365 to scan mail that returns from the on-premises environment. This behavior adds a `compauth` header value to the messages, which might result in the [messages being identified as spam](/en-us/defender-office-365/message-headers-eop-mdo). In *linear inbound routing*scenarios in Centralized Mail Transport, adding on-premises hybrid servers to Enhanced Filtering for Connectors is supported.
    - Examples of *non-linear inbound routing*(adding on-premises hybrid servers to Enhanced Filtering for Connectors isn't supported):
        - Internet &gt; Microsoft 365 &gt; On-premises &gt; Microsoft 365
        - Internet &gt; non-Microsoft service &gt; Microsoft 365 &gt; On-premises &gt; Microsoft 365
    - Examples of *linear inbound routing*(adding on-premises hybrid servers to Enhanced Filtering for Connectors is supported):
        - Internet &gt; On-premises &gt; Microsoft 365
        - Internet &gt; non-Microsoft service &gt; On-premises &gt; Microsoft 365

## Configure Enhanced Filtering for Connectors

Note

Currently, IPv6 addresses are supported only in PowerShell. To use PowerShell to configure Enhanced Filtering for Connectors, see the Use PowerShell to configure Enhanced Filtering for Connectors on an inbound connector section later in this article.

### What do you need to know before you begin?

- Include all of the trusted IP addresses associated with the on-premises hosts or the non-Microsoft filters that send email into your Microsoft 365 organization, including any intermediate hops with public IP addresses. To get these IP addresses, consult the documentation or support provided with the service.
- After you enable Enhanced Filtering for Connectors, [disable](../../security-and-compliance/mail-flow-rules/manage-mail-flow-rules#enable-or-disable-a-mail-flow-rule) any [mail flow rules (transport rules) that request a spam filtering bypass](../../security-and-compliance/mail-flow-rules/use-rules-to-set-scl) (spam confidence level or SCL -1) for messages that flow through the connector. SCL -1 is an input to filtering, not a final decision, and the SCL value stamped on the message might differ. The following scenarios might require you to maintain the SCL = -1 mail flow rule:

    - You're using [Microsoft Defender for Office 365 Evaluation Mode](/en-us/defender-office-365/trial-user-guide-defender-for-office-365).
    - You're phasing in a [Defense in Depth](/en-us/defender-office-365/step-by-step-guides/defense-in-depth-guide) configuration.
- To open the Microsoft Defender portal, go to https://security.microsoft.com. To go directly to the **Enhanced Filtering for Connectors** page, use https://security.microsoft.com/skiplisting.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Exchange Online permissions](../../permissions-exo/permissions-exo#role-groups-in-exchange-online): Membership in the **Organization Management** role group.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^ or **Exchange Administrator** roles.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

### Use the Microsoft Defender portal to configure Enhanced Filtering for Connectors on an inbound connector

1. In the Microsoft Defender portal, go to **Email & Collaboration** &gt; **Policies & Rules** &gt; **Threat policies** page &gt; **Rules** section &gt; **Enhanced filtering**.
2. On the **Enhanced Filtering for Connectors** page, select the inbound connector that you want to configure by clicking on the name.
3. In the connector details flyout that appears, configure the following settings:

    - **IP addresses to skip**: Choose one of the following values:

        - **Disable Enhanced Filtering for Connectors**: Turn off Enhanced Filtering for Connectors on the connector.
        - **Automatically detect and skip the last IP address**: We recommend this value if you have to skip only the last message source.
        - **Skip these IP addresses that are associated with the connector**: Select this value to configure a list of IP addresses to skip. Enter a single IP (for example, 192.168.1.1), IP range (for example, 192.168.0.1-192.168.0.254), or CIDR IP (for example, 192.168.0.1/25) in the box and press **Enter**. The entry is added as a separate item (displayed as a gray box with an **X** icon). After confirming that the entry appears, proceed to the following steps.

            Important

            - Microsoft 365 IP addresses aren't supported. Don't use this feature to compensate for issues introduced by unsupported email routing paths. Use caution and limit the IP ranges to only the email systems that handle your own organization's messages before Microsoft 365 or Office 365.
            - The loopback address (127.0.0.0/8) or private IP address defined by RFC 1918 (10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16) aren't supported. Enhanced Filtering automatically detects and skips loopback addresses and private IP addresses. You should configure any network address translation (NAT) devices to assign public IP addresses to email servers involved in email delivery to Microsoft 365.
            - Currently, IPv6 addresses are supported only in PowerShell.
    - If you selected **Automatically detect and skip the last IP address** or **Skip these IP addresses that are associated with the connector**, the **Apply to these users** section appears:

        - **Apply to entire organization**: We recommend this value after you test the feature on a few recipients first.
        - **Apply to a small set of users**: Select this value to configure a list of recipient email addresses that Enhanced Filtering for Connectors applies to. We recommend this value as an initial test of the feature.

            Note

            - This value is effective only on the actual email addresses that you specify. For example, if a user has five email addresses associated with their mailbox (also known as *proxy addresses*), you need to specify all five of their email addresses here. Otherwise, messages sent to the four other email addresses go through normal filtering.
            - Similarly, if you add a group SMTP address, skiplisting applies only to messages addressed to that group. Skiplisting doesn't apply to messages sent directly to individual group members unless those individual addresses are also specified.
            - In hybrid environments where inbound mail flows through on-premises Exchange, you must specify the *TargetAddress* of the *MailUser* object. For example, `michelle@contoso.mail.onmicrosoft.com`.
            - This value is effective only on messages where **all** recipients are specified here. If a message contains **any** recipients that aren't specified here, normal filtering is applied to **all** recipients of the message.
4. When you're finished, select **Save**.

'

### Use PowerShell to configure Enhanced Filtering for Connectors on an inbound connector

To configure Enhanced Filtering for Connectors on an inbound connector, [connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) and use the following syntax:

```powershell
Set-InboundConnector -Identity <ConnectorIdentity> [-EFSkipLastIP <$true | $false>] [-EFSkipIPs <IPAddresses>] [-EFUsers "emailaddress1","emailaddress2",..."emailaddressN"]
```

- *EFSkipLastIP*: Valid values are:

    - `$true`: Only the last message source is skipped.
    - `$false`: Skip the IP addresses specified by the *EFSkipIPs* parameter. If no IP addresses are specified there, Enhanced Filtering for Connectors is disabled on the inbound connector. The default value is `$false`.
- *EFSkipIPs*: The specific IPv4 or IPv6 addresses to skip when the *EFSkipLastIP* parameter value is `$false`. Valid values are:

    - **A single IP address**: For example, `192.168.1.1`.
    - **An IP address range**: For example, `192.168.1.0-192.168.1.31`.
    - **Classless Inter-Domain Routing (CIDR) IP**: For example, `192.168.1.0/25`.

    See the **Skip these IP addresses that are associated with the connector** description in the previous section for limitations on IP addresses.
- *EFUsers*: The comma-separated email address of recipient email addresses that you want to apply Enhanced Filtering for Connectors to. See the **Apply to a small set of users** description in the previous section for limitations on individual recipients. The default value is blank (`$null`), which means Enhanced Filtering for Connectors is applied to all recipients.

This example configures the inbound connector named From Anti-Spam Service with the following settings:

- Enhanced Filtering for Connectors is enabled on the connector, and the IP address of the last message source is skipped.
- Enhanced Filtering for Connectors only applies to the recipient email addresses `michelle@contoso.com`, `laura@contoso.com`, and `julia@contoso.com`.

```powershell
Set-InboundConnector -Identity "From Anti-Spam Service" -EFSkipLastIP $true -EFUsers "michelle@contoso.com","laura@contoso.com","julia@contoso.com"
```

To disable Enhanced Filtering for Connectors, use the value `$false` for the *EFSkipLastIP* parameter.

For detailed syntax and parameter information, see [Set-InboundConnector](/en-us/powershell/module/exchangepowershell/set-inboundconnector).

## What happens when you enable Enhanced Filtering for Connectors?

The following table describes what connections look like before and after you enable Enhanced Filtering for Connectors:

| Feature | Before Enhanced Filtering is enabled | After Enhanced Filtering is enabled |
| --- | --- | --- |
| **Email domain authentication** | [Implicit](/en-us/defender-office-365/email-authentication-about#composite-authentication) using anti-spoof protection technology. | Explicit, based on the source domain's SPF, DKIM, and DMARC records in DNS. |
| **X-MS-Exchange-ExternalOriginalInternetSender** | Not available | This header is stamped if skip listing was successful, enabled on the connector, and recipient match happens. The value of this field contains information about the true source address. |
| **X-MS-Exchange-SkipListedInternetSender** | Not available | This header is stamped if skip listing was enabled on the connector, irrespective of recipient matches. The value of this field contains information about the true source address. This header is used primarily for reporting purposes and to help understand WhatIf scenarios. |

You can view the improvements in filtering and reporting by using the Threat protection status report in the Microsoft Defender portal. For more information, see [Threat protection status report](/en-us/defender-office-365/reports-email-security#threat-protection-status-report).