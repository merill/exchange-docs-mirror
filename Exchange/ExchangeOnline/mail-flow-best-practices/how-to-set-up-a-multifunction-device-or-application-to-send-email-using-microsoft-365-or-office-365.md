---
layout: Conceptual
title: How to set up a multifunction device or application to send email using Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.topic: install-set-up-deploy
author: ArindamT
ms.author: arindamt
ms.reviewer: arindamt
description: Learn how to set up printers, scanners, LOB applications to send email using Microsoft 365 or Office 365.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- BCS160
- MOE150
- MET150
audience: Admin
f1.keywords:
- CSH
ms.custom: MiniMaven
ms.service: exchange-online
ms.localizationpriority: high
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: f1e4e3f0-bb9c-cca0-9343-49926262caba
document_version_independent_id: 75645bf5-f9a5-b5b9-d9e6-856e32ffc97f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: e44dae4d-c132-7eb5-9f34-b0fb3ea2d089
---

# How to set up a multifunction device or application to send email using Microsoft 365 or Office 365 | Microsoft Learn

This article explains how you can send email from devices and business applications when all of your mailboxes are in Microsoft 365 or Office 365. These devices and applications *create* email messages, but are incapable of *sending* those messages without help, because they aren't email servers. For example:

- Network-connected scanners that send scanned documents as attachments in email messages.
- Line-of-business (LOB) applications that need to send email messages. For example, an appointment application that sends email reminders to participants.

The following methods are available to send email from these devices or applications using Microsoft 365 or Office 365:

- **Client SMTP submission (also known as authenticated SMTP submission or SMTP AUTH)**: Send authenticated email using the credentials of a cloud mailbox. POP3 or IMAP4 clients use this method to send email.
- **SMTP relay**: Send email as an email server through Microsoft 365 or Office 365. The connection is authenticated using an inbound connector.
- **Direct Send**: Send unauthenticated email as an external email server directly to Microsoft 365 or Office 365.
- **High Volume Email**: Send large volumes of email to internal recipients. Requires the use of an HVE account, which can be authenticated either through Basic Authentication (username/password) or Modern Authentication (OAuth).

Here's a comparison of each method and the features they support:

| - | Client SMTP submission | SMTP relay | Direct Send | High Volume Email |
| --- | --- | --- | --- | --- |
| **Features** |  |  |  |  |
| Send to recipients in your domain or domains | Yes | Yes | Yes | Yes |
| Relay to the internet via Microsoft 365 or Office 365 | Yes | Yes | No | No |
| Bypass anti-spam | Yes, if the email is destined for one of your Microsoft 365 or Office 365 mailboxes. | No. Suspicious email might be filtered. We recommend an SPF record entry. | No. Suspicious email might be filtered. We recommend an SPF record entry. | Yes, if the mail is destined for one of your Microsoft 365 or Office 365 mailboxes. |
| Supports mail sent from applications hosted by a third party | Yes | No | Yes. We recommend updating your SPF record to allow the third party to send as your domain. | Yes |
| Saves to Sent Items folder | Yes | No | No | No |
| **Requirements** |  |  |  |  |
| Open TCP port | 587 or 25 | 25 | 25 | 587 |
| Device or application server must support TLS | Required | Optional | Optional | Required |
| Requires authentication | Microsoft 365 or Office 365 username and password required | One or more static IP addresses. Your printer or app host requires a static IP address that's visible to Microsoft 365 or Office 365 for authentication. | None | Yes, HVE account credentials or OAuth token are required. |

Here are the limitations of each method:

| Limitations | Client SMTP submission | SMTP relay | Direct Send | High Volume Email |
| --- | --- | --- | --- | --- |
| Throttling limits | 10,000 recipients per day. 30 messages per minute. | Reasonable limits are imposed. The service can't be used to send spam or bulk mail. For more information about reasonable limits, see [High-risk delivery pool for outbound messages](/en-us/defender-office-365/outbound-spam-high-risk-delivery-pool-about#relay-pool). | Standard throttling for anonymous email sent from the internet to Microsoft 365 or Office 365. | No recipient or message rate limits. For more information on HVE limits see [Manage High Volume Email (HVE) for Microsoft 365](high-volume-mails-m365) |

The rest of this article describes each method in detail.

## Client SMTP submission: Authenticate mail sent from your device or application through a cloud mailbox

Note

Client SMTP submission using Basic authentication in Exchange Online is scheduled for deprecation, see [timeline information](https://techcommunity.microsoft.com/blog/exchange/exchange-online-to-retire-basic-auth-for-client-submission-smtp-auth/4114750). We strongly recommend using one of the following alternative methods instead:

- **Send email to internal recipients only**: Use High Volume Email for Microsoft 365. For instructions, see [Manage High Volume Email for Microsoft 365](high-volume-mails-m365).
- **Send email to internal and external recipients**: Use Azure Communication Services Email. For more information, see [Email SMTP support in Azure Communication Services](/en-us/azure/communication-services/concepts/email/email-smtp-overview).
- If you have one or more on-premises email servers (Exchange Server or any other SMTP server), you can use one of the following methods:
    - Use Basic authentication to authenticate with the on-premises email server.
    - Configure the on-premises email server for anonymous relay (not open relay). For instructions in Exchange, see [Allow anonymous relay on Exchange servers](/en-us/exchange/mail-flow/connectors/allow-anonymous-relay).

Client SMTP submission using Basic authentication isn't compatible with [Security defaults in Microsoft Entra ID](/en-us/entra/fundamentals/security-defaults). We recommend using Modern authentication (OAuth) to connect to our service. For more information about OAuth, see [Authenticate an IMAP, POP, or SMTP connection using OAuth](/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth).

Client SMTP submission supports the following scenarios:

- Send email from a third-party hosted application, service, or device.
- Send email to people inside and outside your organization.

The device or application must be able to authenticate with Microsoft 365 or Office 365. The email address of the mailbox appears as the message sender.

Tip

Verify SMTP AUTH is enabled for the designated mailbox. SMTP AUTH is disabled for organizations created after January 2020 but you can enable it per-mailbox. For more information, see [Enable or disable authenticated client SMTP submission (SMTP AUTH) in Exchange Online](../clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission).

- **Features of client SMTP submission**:

    - Send email to people inside and outside your organization.
    - Bypass most spam checks for email sent to people in your organization. This bypass can help prevent your company IP addresses from being added to a spam blocklist.
    - Send email from any location or IP address, including your on-premises network, or a third-party cloud-hosting service like Microsoft Azure.
- **Requirements for client SMTP submission**:

    - **Authentication**: We recommend using Modern authentication in the form of OAuth. For more information about OAuth, see [Authenticate an IMAP, POP, or SMTP connection using OAuth](/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth). If SMTP AUTH is intentionally disabled in the organization or on the designated mailbox, use a different method.
    - **Mailbox**: You need a licensed Microsoft 365 or Office 365 mailbox that the device uses to send email from.
    - **Transport Layer Security (TLS)**: Your device or application must support TLS 1.3 or TLS 1.2. If your device or application doesn't support TLS 1.2 or later, you can't use client SMTP submission with Microsoft 365 or Office 365.

        Instead, you can use an on-premises email server (Exchange Server or any other SMTP server) to relay mail. For more information about configuring your own Exchange server to send mail to Microsoft 365 or Office 365, see [Set up connectors to route mail between Microsoft 365 or Office 365 and your own email servers](use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail).

        Tip

        For information about TLS, see [How Exchange Online uses TLS to secure email connections](/en-us/purview/exchange-online-uses-tls-to-secure-email-connections). For detailed technical information about how Exchange Online uses TLS with cipher suite ordering, see [TLS cipher suites supported by Office 365](/en-us/purview/technical-reference-details-about-encryption#tls-cipher-suites-supported-by-microsoft-365).
    - **TCP Port**: Port 587 (recommended) or port 25 is required and must be unblocked on your network. Some network firewalls or ISPs block port 25 because that port is used by email servers to send messages.

        Tip

        If your device or application recommends or defaults to TCP port 465, it doesn't support the required versions of TLS for client SMTP submission in Microsoft 365 or Office 365.
    - **DNS**: Use the DNS name `smtp.office365.com`. Don't use an IP address for the Microsoft 365 or Office 365 server.
- **Limitations of client SMTP submission**:

    - If the device or application needs to send email from an account (mailbox) that's different from the account that's used to authenticate, the sign-in account needs **Send As** permission in the mailbox. Otherwise, messages are returned in a nondelivery report (also known as an NDR or bounce message):

        **An example of a failure:**

        5.7.60 SMTP; Client doesn't have permissions to send as this sender.

        For instructions to add **Send As** permission to the mailbox, see [Manage permissions for recipients in Exchange Online](../recipients-in-exchange-online/manage-permissions-for-recipients).
    - Microsoft 365 or Office 365 imposes sending limits for the volume and rate of email messages from mailboxes. For more information, see [Exchange Online limits - Receiving and sending limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#receiving-and-sending-limits).

### Set up client SMTP submission

Configure your device or application using the settings described in the following table:

| Device or Application setting | Value |
| --- | --- |
| Server/smart host | `smtp.office365.com`. Don't use an IP address for the Microsoft 365 or Office 365 server. |
| TCP port | 587 (recommended) or 25 |
| TLS/StartTLS | Enabled (TLS 1.3 or TLS 1.2) |
| Username/email address and password | Enter the sign-in credentials of the designated mailbox. |

Tip

If you're using a third-party device or application, be aware that this device or application might use different names for the settings; so, check their documentation for instructions.

## SMTP relay: Configure a connector to relay email from your device or application through Microsoft 365 or Office 365

This method supports the following scenarios:

- When the following methods don't work for you:
    - [Client SMTP submission using Modern authentication](/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth).
    - [High Volume Email for Microsoft 365](high-volume-mails-m365)
    - [Azure Communication Services Email](/en-us/azure/communication-services/concepts/email/email-smtp-overview)
    - Basic authentication or anonymous relay through an on-premises email server.
- When the device or application needs to send more email than a mailbox allows.

An inbound connector in Microsoft 365 or Office 365 authenticates your device or application using a TLS certificate (recommended) or public IP address. Authentication helps to identify messages as belonging to your organization so they aren't identified as spam or spoofing.

Your device or application can send email using any address (including email addresses that can't receive email), as long as the address is in an [accepted domain](manage-accepted-domains/manage-accepted-domains). The email address doesn't need to be associated with a mailbox. For example, if your Microsoft 365 domain is contoso.com, the device or application could send mail using an address like `do_not_reply@contoso.com`.

You can't use SMTP relay to send email from a third-party hosted service (for example, Microsoft Azure) through Microsoft 365 or Office 365. For more information, see [Troubleshoot outbound SMTP connectivity issues in Azure](/en-us/azure/virtual-network/troubleshoot-outbound-smtp-connectivity).

- **Features of SMTP relay**:

    - Doesn't require a licensed Microsoft 365 or Office 365 mailbox to send email.
    - Higher sending limits than client SMTP submission. Senders aren't subject to the limits of client SMTP submission.
- **Requirements for SMTP relay**:

    - **A certificate or static public IP address**: If the device or application can't use a certificate for authentication, use a static IP address that isn't shared with another organization.
    - **Connector**: Set up an inbound connector in Microsoft 365 or Office 365 as described in this section.
    - **TCP Port**: Port 25 is required. Verify this port isn't blocked on your network or by your ISP.
- **Limitations of SMTP relay**:

    - Mail can be disrupted if your IP addresses are added to a spam blocklist.
    - Reasonable limits are imposed for sending email messages. For more information, see [High-risk delivery pool for outbound messages](/en-us/defender-office-365/outbound-spam-high-risk-delivery-pool-about#relay-pool).
    - Requires static unshared IP addresses (unless a certificate is used).
    - The device or application is expected to retry failed connection within a reasonable amount of time. Microsoft recommends using SMTP logs on the device or application to help investigate these types of failures.

    Tip

    Per the [SMTP RFC suggestion](https://datatracker.ietf.org/doc/html/rfc5321#section-4-5-4:%7E:text=SMTP%20clients%20that,rather%20than%20SMTP), client SMTP submission might work better for a device or application that isn't a full-featured email server (MTA).

### Configure a TLS certificate-based connector for SMTP relay

Before you start, you need a certificate where the Subject or Subject Alternate Name (SAN) fields contain an [accepted domain](manage-accepted-domains/manage-accepted-domains) in Microsoft 365 or Office 365.

1. Configure your device or application using the settings described in the following table:

    | Device or application setting | Value |
    | --- | --- |
    | Server/smart host | Your MX endpoint. For example, `contoso-com.mail.protection.outlook.com`. To find this value, see Appendix: Find the MX record for the chosen accepted domain in Microsoft 365 or Office 365. |
    | TCP port | 25 |
    | TLS/StartTLS | Enabled (TLS 1.3 or TLS 1.2) |
    | TLS Certificate | The Subject or SAN fields of the certificate contain a verified [accepted domain](manage-accepted-domains/manage-accepted-domains) in Microsoft 365 or Office 365. |
    | Email address | Any email address in the accepted domain. |

    Tip

    If you're using a third-party device or application, be aware that this device or application might use different names for the settings; so, check their documentation for instructions.
2. Create a certificate-based inbound connector in Microsoft 365.

    If you already have an inbound connector configured to deliver messages from your on-premises organization to Microsoft 365 or Office 365 (for example, a hybrid environment), you probably don't need to create a dedicated connector for SMTP relay.

    Existing hybrid customers who used the Hybrid Configuration Wizard to configure their connectors should check their existing connector to ensure that it uses \*.contoso.com instead of mail.contoso.com or hostname.contoso.com. This domain verification is because mail.contoso.com and hostname.contoso.com might not be registered domains in Microsoft 365.

    To create a certificate-based connector, do the following steps:

    1. In the Exchange admin center (EAC) at https://admin.cloud.microsoft/exchange#/, go to **Mail flow** &gt; **Connectors**. Or, to go directly to the **Connectors** page, use https://admin.cloud.microsoft/exchange#/connectors.
    2. On the **Connectors** page, select ![](../exchangeonline/media/itpro_eac_addicon.png)**Add a connector**.
    3. The new connector wizard opens. On the **New connector** page, configure the following options:

        - **Connection from**: Select **Your organization's email server**.
        - **Connection to**: The value **Office 365** is automatically selected and you can't change it.

        [![Screenshot that shows the New connector page with Connection from: Your organization's email server selected.](../exchangeonline/media/choosing-an-option-from-new-connector-page.png)](../exchangeonline/media/choosing-an-option-from-new-connector-page.png#lightbox)

        When you're finished on the **New connector** page, select **Next**.
    4. On the **Connector name** page, configure the following options:

        - **Name**: Enter a unique, descriptive name for the connector.
        - **Description**: Enter an optional description.
        - **What do you want to do after connector is saved?**:
            - Verify **Turn it on** is selected.
            - Verify **Retain internal Exchange email headers** isn't selected.

        When you're finished on the **Connector name** page, select **Next**.
    5. On the **Authenticating sent email** page, verify **By verifying that the subject name on the certificate that the sending server uses to authenticate with Office 365 matches the domain entered in the text box below (recommended)** is selected.

        In the box, enter an [accepted domain](manage-accepted-domains/manage-accepted-domains) in Microsoft 365 or Office 365 that matches the Subject or SAN field in the certificate used by your server, device, or application.

        For example, contoso.com in an accepted domain in your Microsoft 365 organization, and contoso.com is included in the Subject or SAN field in the certificate that's used on the device or application.

        Tip

        If multiple hosts are identified in the certificate (one in the Subject field and one or more in the SAN field), we recommend using the value \*.contoso.com in this box.

        [![Screenshot of the Authenticating sent email page of the new connector wizard in the Exchange admin center with By verifying the subject name on the certificate... selected.](../exchangeonline/media/authenticating-sent-email.png)](../exchangeonline/media/authenticating-sent-email.png#lightbox)

        When you're finished on the **Authenticating sent email** page, select **Next**.
    6. On the **Review connector** page, verify the configuration of the connector. Use the links on the page or select **Back** to make changes.

        When you're finished on the **Review connector** page, select **Create connector**.
3. To avoid flagging these messages as spam and delivery to recipient Junk Email folders, you need to add an SPF record for your domain in the DNS settings at your domain registrar. For more information, see [Set up SPF to identify valid email sources for your Microsoft 365 domain](/en-us/defender-office-365/email-authentication-spf-configure).
4. To test the configuration, send a test email from your device or application, and confirm the recipient receives it.

### Configure an IP address-based connector for SMTP relay

If you can't configure a certificate-based connector, configure an IP address-based connector to relay email through Microsoft 365 or Office 365.

Before you start, get the public IP address used by the device or application. This IP address is visible to Microsoft 365 or Office 365 as the source of email from the device or application.

Note

Dynamic IP addresses aren't supported or allowed.

Don't share the IP address with anyone outside of your organization (the IP address is used for authentication on the connector).

1. Configure your device or application using the settings described in the following table:

    | Device or application setting | Value |
    | --- | --- |
    | Server/smart host | Your MX endpoint. For example, `contoso-com.mail.protection.outlook.com`. To find this value, see Appendix: Find the MX record for the chosen accepted domain in Microsoft 365 or Office 365. |
    | TCP port | 25 |
    | TLS/StartTLS | Enabled (TLS 1.3 or TLS 1.2) |
    | Email address | Any email address in the verified [accepted domain](manage-accepted-domains/manage-accepted-domains) in Microsoft 365 or Office 365. The email address doesn't need a mailbox. |
2. Create an IP address-based inbound connector in Microsoft 365.

    If you already have an inbound connector configured to deliver messages from your on-premises organization to Microsoft 365 or Office 365 (for example, a hybrid environment), you probably don't need to create a dedicated connector for SMTP relay.

    1. In the Exchange admin center (EAC) at https://admin.cloud.microsoft/exchange#/, go to **Mail flow** &gt; **Connectors**. Or, to go directly to the **Connectors** page, use https://admin.cloud.microsoft/exchange#/connectors.
    2. On the **Connectors** page, select ![](../exchangeonline/media/itpro_eac_addicon.png)**Add a connector**.
    3. The new connector wizard opens. On the **New connector** page, configure the following options:

        - **Connection from**: Select **Your organization's email server**.
        - **Connection to**: The value **Office 365** is automatically selected and you can't change it.

        [![Screenshot of the New connector page of the new connector wizard in the Exchange admin center with Connection from: Your organization's email server selected.](../exchangeonline/media/choosing-an-option-from-new-connector-page.png)](../exchangeonline/media/choosing-an-option-from-new-connector-page.png#lightbox)

        When you're finished on the **New connector** page, select **Next**.
    4. On the **Connector name** page, configure the following options:

        - **Name**: Enter a unique, descriptive name for the connector.
        - **Description**: Enter an optional description.
        - **What do you want to do after connector is saved?**:
            - Verify **Turn it on** is selected.
            - Verify **Retain internal Exchange email headers** isn't selected.

        When you're finished on the **Connector name** page, select **Next**.
    5. On the **Authenticating sent email** page, select **By verifying that the IP address of the sending server matches one of the following IP addresses which belong exclusively to your organization**.

        In the box, enter the public IP address of the device or application.

        [![Screenshot of the Authenticating sent email page of the new connector wizard in the Exchange admin center with By verifying the IP address... selected.](../exchangeonline/media/choosing-an-option-from-authenticating-sent-email-page.png)](../exchangeonline/media/choosing-an-option-from-authenticating-sent-email-page.png#lightbox)

        When you're finished on the **Authenticating sent email** page, select **Next**.
    6. On the **Review connector** page, verify the configuration of the connector. Use the links on the page or select **Back** to make changes.

        When you're finished on the **Review connector** page, select **Create connector**.
3. To avoid identifying these messages as spam and delivery to recipient Junk Email folders, you need to add this IP address as a message source in the SPF record for the domain. For more information, see [Set up SPF to identify valid email sources for your Microsoft 365 domain](/en-us/defender-office-365/email-authentication-spf-configure).
4. To test the configuration, send a test email from your device or application, and confirm the recipient receives it.

## Direct Send: Send mail directly from your device or application to Microsoft 365 or Office 365

Note

Most customers don't need to use Direct Send. We're working on an option to disable Direct Send by default to protect customers.

If your device or application can act as an email server, no Microsoft 365 or Office 365 settings are required. For more information, see your device or application instructions.

We recommend Direct Send only for advanced customers willing to take on the responsibilities of email server admins. You need to be familiar with setting up and following best practices for sending email over the internet. When correctly configured and managed, Direct Send is a secure and viable option. But customers run the risk of misconfiguration that disrupts mail flow or threatens the security of their communication.

Choose Direct Send only when your legacy device or application doesn't support any of the previously described methods.

- **Features of Direct Send**:

    - Higher sending limits than client SMTP submission.
    - Sends email to Microsoft 365 or Office 365 recipients only. Mail sent to recipients outside your cloud-based organization is rejected.
- **Requirements for Direct Send**:

    - **TCP port**: Port 25 is required and must be unblocked on your network.
    - **Static IP address is recommended**: A static IP address is required for an SPF record in the domain. The SPF record helps avoid your messages being flagged as spam. For more information, see [Set up SPF to identify valid email sources for your Microsoft 365 domain](/en-us/defender-office-365/email-authentication-spf-configure).
    - The application or device needs to send email using address in an [accepted domain](manage-accepted-domains/manage-accepted-domains) in Microsoft 365 or Office 365. In addition to SPF, You need to configure [DKIM](/en-us/defender-office-365/email-authentication-dkim-configure) and [DMARC](/en-us/defender-office-365/email-authentication-dmarc-configure) correctly for the domain. Misconfiguration can lead to security gaps.
    - Doesn't require a licensed cloud mailbox, but you need to use an address associated with an [accepted domain](manage-accepted-domains/manage-accepted-domains) in Microsoft 365 or Office 365.
- **Limitations of Direct Send**:

    - Can't deliver email to external recipients (for example, recipients with Yahoo! or Gmail addresses).
    - Messages are just like anonymous email from the internet (all scanning and protections apply).
    - Email might be disrupted if the IP address is on a spam blocklist.
    - Microsoft 365 and Office 365 use throttling policies to protect the performance of the service.

### Set up Direct Send

Configure your device or application using the settings described in the following table:

| Device or application setting | Value |
| --- | --- |
| Server/smart host | Your MX endpoint. For example, `contoso-com.mail.protection.outlook.com`. To find this value, see Appendix: Find the MX record for the chosen accepted domain in Microsoft 365 or Office 365. |
| TCP port | 25 |
| TLS/StartTLS | Optional |
| Email address | Any email address in an [accepted domain](manage-accepted-domains/manage-accepted-domains) in Microsoft 365 or Office 365. The email address doesn't need to have a mailbox. |

Tip

If you're using a third-party device or application, be aware that this device or application might use different names for the settings; so, check their documentation for instructions.

## Run diagnostic to help set up devices or applications that send email using Microsoft 365 or Office 365

Tip

This feature requires a Microsoft 365 administrator account.

If you need help with setting up devices or applications to send email using Microsoft 365 or Office 365, you can run an automated diagnostic using the following button:

A flyout opens in the Microsoft 365 admin center. Select the appropriate option (for example, new setup or troubleshooting existing setup).

## Use your own email server to send email from multifunction devices and applications

If you happen to have an on-premises email server, you should seriously consider using it for SMTP relay instead of Microsoft 365 or Office 365. A local email server that you physically control is easier to configure for SMTP relay.

Tip

Windows Server 2022 is the last version of Windows Server that has the SMTP server feature (in IIS 6.0). As this is still unsupported for relaying email to Microsoft 365 or Office 365, use a [supported version of Exchange Server](/en-us/exchange/plan-and-deploy/supportability-matrix) or [Azure Communication Service](/en-us/azure/communication-services/concepts/email/email-overview).

For Exchange Server, see the following articles:

- [Allow anonymous relay on Exchange servers](/en-us/exchange/mail-flow/connectors/allow-anonymous-relay)
- [Receive messages from a server, service, or device that doesn't use Exchange](/en-us/exchange/mail-flow/connectors/custom-receive-connectors#scenario-3-receive-messages-from-a-server-service-or-device-that-doesnt-use-exchange)

## Appendix: Find the MX record for the chosen accepted domain in Microsoft 365 or Office 365

SMTP relay and Direct Send require the **Points to address or value** from the MX record for the [accepted domain](manage-accepted-domains/manage-accepted-domains) in Microsoft 365 or Office 365 that contains the email address you plan on using to send email from the device or application. This value uses the syntax `<YourCustomDomain>-com.mail.protection.outlook.com` (for example, `contoso-com.mail.protection.outlook.com`).

To find this value for your domain, do the following steps:

1. In the Microsoft 365 admin center at https://admin.microsoft.com, go to **Show all** &gt; **Settings** &gt; **Domains**. Or, to go directly to the **Domains** page, use https://admin.microsoft.com/#/Domains.
2. On the **Domains** page, verify the **Status** value of the domain you plan on using is **Healthy**. If the domain isn't verified, email could be lost, and you can't use [message trace](../monitoring/trace-an-email-message/message-trace-modern-eac) to track the lost messages.

    Select the domain by clicking anywhere in the row other than the check box next to the first column.
3. On the domain details page that opens, select the **DNS records** tab. The MX record for the domain is listed in the **Microsoft Exchange** section.

    [![Screenshot that shows the MX record page and Points to address or value.](../exchangeonline/media/mx-record.png)](../exchangeonline/media/mx-record.png#lightbox)
4. Select the **MX** entry by clicking anywhere in the row other than the check box next to the first column.
5. In the **MX record** flyout that opens, copy the **Points to address or value**. For example, `contoso-com.mail.protection.outlook.com`.