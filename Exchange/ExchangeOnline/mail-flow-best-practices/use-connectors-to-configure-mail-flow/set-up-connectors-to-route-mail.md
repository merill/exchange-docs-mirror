---
layout: Conceptual
title: Set up connectors to route mail between Microsoft 365 or Office 365 and your own email servers | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail
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
description: Admins can learn how to use connectors to route mail between Microsoft 365, Office 365, or Exchange Online and on-premises email servers.
ms.topic: install-set-up-deploy
author: AshaIyengar21
ms.author: serdars
ms.assetid: 2e93fd60-a5ef-4e64-8e62-2b862b2d1033
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 498774ba-06b8-5087-f884-bab065225d63
document_version_independent_id: a54b404b-0ade-45e8-3282-402c1a3bb0d0
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 2f43891a-ee87-1147-5c74-18731b3dc5ea
---

# Set up connectors to route mail between Microsoft 365 or Office 365 and your own email servers | Microsoft Learn

This topic helps you set up the connectors you need for the following scenarios:

- You have your own on-premises email servers, and you use the Built-in security add-on for on-premises mailboxes.
- You have (or intend to have) mailboxes both in the cloud and in your on-premises email environment.

Important

Before you get started, make sure to check on your specific scenario in [**I have my own email servers**](use-connectors-to-configure-mail-flow#i-have-my-own-email-servers).

If you apply the steps described in this article to **partner email services**, you may have unintended consequences including *email delivery failure*. To learn more about partner scenarios, see [Set up connectors for secure mail flow with a partner organization](set-up-connectors-for-secure-mail-flow-with-a-partner).

## How do connectors work with my on-premises email servers?

If you have the Built-in security add-on for on-premises mailboxes, or if some of your mailboxes are in Microsoft 365 or Office 365 and some are on your email servers, set up connectors to enable mail flow in both directions. You can enable mail flow between Microsoft 365 or Office 365 and any SMTP-based email server, such as Exchange or a third-party email server.

The diagram below shows how connectors in Microsoft 365 or Office 365 work with your own email servers.

![Connectors between Microsoft 365 or Office 365 and your e-mail server.](../../exchangeonline/media/0df5ec3d-29c1-4add-9e22-5b0c26bec750.png)

In this example, John and Bob are both employees at your company. John has a mailbox on an email server that you manage, and Bob has a mailbox in Office 365. John and Bob both exchange mail with Sun, a customer with an internet email account:

- When email is sent between John and Bob, connectors are needed.
- When email is sent between John and Sun, connectors are needed. (All internet email is delivered via Office 365.)
- When email is sent between Bob and Sun, no connector is needed.

If you have your own email servers and Microsoft 365 or Office 365, you must set up connectors in Microsoft 365 or Office 365. Without connectors, email will not flow between Microsoft 365 or Office 365 and your organization's email servers.

## How do connectors route mail between Microsoft 365 or Office 365 and my own email server?

You need two connectors to route email between Microsoft 365 or Office 365 and your email servers, as follows:

- **A connector from Office 365 to your own email server**

    When you set up Microsoft 365 or Office 365 to accept all emails on behalf of your organization, you will point your domain's MX (mail exchange) record to Microsoft 365 or Office 365. To prepare for this mail delivery scenario, you must set up an alternative server (called a "smart host") so that Microsoft 365 or Office 365 can send emails to your organization's email server (also called "on-premises server"). To complete the scenario, you might need to configure your email server to accept messages delivered by Microsoft 365 or Office 365.
- **A connector from your own email server to Office 365**

    When this connector is set up, Microsoft 365 or Office 365 accepts messages from your organization's email server and send the messages to recipients on your behalf. This recipient could be a mailbox for your organization in Microsoft 365 or Office 365, or it could be a recipient on the internet. To complete this scenario, you'll also need to configure your email server to send email messages directly to Microsoft 365 or Office 365.

This connector enables Microsoft 365 or Office 365 to scan your email for spam and malware, and to enforce compliance requirements such as running data loss prevention policies. When your email server sends all email messages directly to Microsoft 365 or Office 365, your own IP addresses are shielded from being added to a spam-block list. To complete the scenario, you might need to configure your email server to send messages to Microsoft 365 or Office 365.

Note

This scenario requires two connectors: one from Microsoft 365 or Office 365 to your mail servers, and one to manage mail flow in the opposite direction. Before you start, ensure you have all the information you need, and continue with the instructions until you have set up and validated both connectors.

## Overview of the steps

Here is an overview of the steps:

- Complete the prerequisites for your email server environment.
- Part 1: Configure mail to flow from Microsoft 365 or Office 365 to your on-premises email server
- Part 2: Configure mail to flow from your email server to Microsoft 365 or Office 365

## Prerequisites for your on-premises email environment

Prepare your on-premises email server so that it's ready to connect with Microsoft 365 or Office 365. Follow these steps:

1. Ensure that your on-premises email server is set up and capable of sending and receiving Internet (external) email.
2. Check that your on-premises email server has Transport Layer Security (TLS) enabled, with a valid certification authority-signed (CA-signed) certificate. We recommend that the certificate subject name includes the domain name that matches the primary email server in your organization. Buy a CA-signed digital certificate that matches this description, if necessary.
3. If you want to use certificates for secure communication between Microsoft 365 or Office 365 and your email server, update the connector your email server uses to receive mail. This connector must recognize the right certificate when Microsoft 365 or Office 365 attempts a connection with your server. If you're using Exchange, see [Receive connectors](../../mail-flow/connectors/receive-connectors) for more information. On the Edge Transport Server or Client Access Server (CAS), configure the default certificate for the Receive connector. Update the *TlsCertificateName* parameter on the **Set-ReceiveConnector** cmdlet in the Exchange Management Shell. To learn how to open the Exchange Management Shell in your on-premises Exchange organization, see [Open the Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell).
4. Make a note of the name or IP address of your external-facing email server. If you're using Exchange, this IP address is the Fully Qualified Domain Name (FQDN) of your Edge Transport server or CAS that will receive email from Microsoft 365 or Office 365.
5. Open port 25 on your firewall so that Microsoft 365 or Office 365 can connect to your email servers.
6. Ensure that your firewall accepts connections from all Microsoft 365 or Office 365 IP addresses. See [Exchange Online](/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges) for the published IP address ranges.
7. Make a note of an email address for each domain in your organization. You'll need this email address later to test that your connector is working properly.

## Part 1: Configure mail to flow from Microsoft 365 or Office 365 to your on-premises email server

There are three steps for this configuration:

1. Configure your Microsoft 365 or Office 365 environment.
2. Set up a connector from Office 365 to your email server.
3. Change your MX record to redirect your mail flow from the internet to Microsoft 365 or Office 365.

### 1. Configure your Microsoft 365 or Office 365 environment

Make sure you have completed the following tasks in Microsoft 365 or Office 365:

1. To set up connectors, you need permissions assigned before you can begin. To check what permissions you need, see the Microsoft 365 and Office 365 connectors entries in [Permissions in Exchange Online](/en-us/exchange/permissions-exo/permissions-exo).
2. If you want Microsoft 365 or Office 365 to relay email from your on-premises email servers to the internet, use one of the following methods:

    - Use a certificate configured with a subject name that matches an accepted domain in Microsoft 365 or Office 365. We recommend that your certificate's common name or subject alternative name matches the primary SMTP domain for your organization. For details, see [Prerequisites for your on-premises email environment](set-up-connectors-to-route-mail#prerequisites-for-your-on-premises-email-environment).

    -OR-

    - Ensure that all the sender domains and subdomains of your organization are configured as accepted domains in Microsoft 365 or Office 365.

        For more information about defining accepted domains, see [Manage accepted domains in Exchange Online](../manage-accepted-domains/manage-accepted-domains) and [Enable mail flow for subdomains in Exchange Online](../manage-accepted-domains/enable-mail-flow-for-subdomains).
3. Decide whether you want to use mail flow rules (also known as transport rules) or domain names to deliver mail from Microsoft 365 or Office 365 to your email servers. Most businesses choose to deliver mail for all accepted domains. For more information, see [Scenario: Conditional mail routing in Exchange Online](conditional-mail-routing).

    Note

    You can set up mail flow rules as described in [Mail flow rule actions in Exchange Online](../../security-and-compliance/mail-flow-rules/mail-flow-rule-actions). For example, you might want to use mail flow rules with connectors if your mail is currently directed via distribution lists to multiple sites.

### 2. Set up a connector from Microsoft 365 or Office 365 to your email server

Before you set up a new connector, check for any connectors that are already listed here for your organization. For example, if you ran the Exchange [Hybrid Configuration wizard](../../hybrid-configuration-wizard), connectors that deliver mail between Microsoft 365 or Office 365 and Exchange Server will be set up already and listed here, as shown in the following screenshot.

![Home page of the New Exchange admin center.](../../exchangeonline/media/new-exchange-admin-center.png)

If the connectors are already listed, you don't need to set them up again, but you can edit them if you need to.

If you don't plan to use the hybrid configuration wizard, or if you're running a non-Microsoft SMTP mail server, or if no connector is listed from your organization's mail server to Microsoft 365 or Office 365, set up a connector using the wizard, as described in the procedures below.

Note

Before creating a connector, navigate to EAC from the Microsoft 365 admin center by clicking **Exchange** under the **Admin centers** pane.

1. Navigate to **Mail flow &gt; Connectors**. The **Connectors** screen appears.
2. Click **+ Add a connector**. The **New connector** screen appears.

    ![The screen on which the process to create a connector begins.](../../exchangeonline/media/home-screen-to-add-a-new-connector.png)
3. Under **Connection from**, choose **Office 365**.
4. Under **Connection to**, choose **Your organization's email server**.

    ![A page on which new connector is configured.](../../exchangeonline/media/configuring-connector-new-eac.png)
5. Click **Next**. The **Connector name** screen appears.
6. Provide a name for the connector and click **Next**. The **Use of connector** screen appears.
7. Choose an option that determines when you want to use the connector, and click **Next**. The **Routing** screen appears.

    Note

    For information on choosing one of the three option on the **Use of connector** screen and the reasons for choosing that option, see **Options determining use of connector**, below in this article.
8. Enter the domain name or IP address of the host computer to which Office 365 will deliver email messages.
9. Click **+**.

    Note

    It is mandatory to click **+** after entering the smart host name to navigate to the next screen.
10. Click **Next**. The **Security restrictions** screen appears.
11. Define the settings by:

    - Checking the check box for **Always use Transport Layer Security (TLS) to secure the connection (recommended)**.

        Note

        It is not mandatory to configure the Transport Layer Security (TLS) settings on the **Security restrictions** page. You can navigate to the next screen without choosing anything on this screen. The need to define TLS settings on this page depends on whether the destination server supports TLS or not.

        If you opt to define the TLS settings, it becomes mandatory to choose.
    - Choosing any one of the two options under **Connect only if the recipient's email server certificate matches this criteria**.

        Note

        If you are choosing the **Issue by a trusted certificate authority (CA)** option, the **Add the subject name or subject alternative name (SAN) matches this domain name** option is activated.

        It is optional to choose the **Add the subject name or subject alternative name (SAN) matches this domain name** option. However, if you choose it, you must enter the domain name to which the certificate name matches.
    - Clicking **Next**, on which the **Validation email** screen appears.
12. Enter an email that belongs to the mailbox of your organization's domain.
13. Click **+**.

    Note

    It is mandatory to click **+** for the **Validate** button to be enabled.
14. Click **Validate**. The connector validation process starts.
15. Once the validation process is completed, click **Next**. The **Review connector** screen appears.
16. Review the settings you have configured and click **Create connector**.

    The connector is created.

    If the connector does not validate, double-click the message displayed to get more information, and see [Validate connectors](validate-connectors) for help resolving issues.

### 3. Change your MX record to redirect your mail flow from the internet to Microsoft 365 or Office 365

To redirect email flow to Microsoft 365 or Office 365, change the MX (mail exchange) record for your domain. For instructions on how to do this task, see [Add DNS records to connect your domain](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).

## Part 2: Configure mail to flow from your email server to Microsoft 365 or Office 365

There are two steps for this configuration:

1. Set up a connector from your email server to Microsoft 365 or Office 365.
2. Set up your email server to relay mail to the internet via Microsoft 365 or Office 365.

### 1. Set up a connector from your email server to Microsoft 365 or Office 365

1. Navigate to **Mail flow &gt; Connectors**. The **Connectors** screen appears.

    ![Page displaying already created connectors.](../../exchangeonline/media/new-exchange-admin-center.png)

    Note

    If any connectors already exist for your organization, they are displayed on clicking **Connectors**.
2. Click **+ Add a connector**. The **New connector** screen appears.

    ![The screen on which the process to create a connector begins.](../../exchangeonline/media/home-screen-to-add-a-new-connector.png)
3. Under **Connection from**, choose **Your organization's email server**.

    ![The screen on which you configure the sending server as your organization server and the destination server as Microsoft 365 server.](../../exchangeonline/media/from-your-server-to-365.png)

    Note

    After you select the **Your organization's email server** radio button under **Connection from**, the option under **Connection to** is greyed out, implying that it is the default option chosen.
4. Click **Next**. The **Connector name** screen appears.
5. Provide a name for the connector and click **Next**. The **Authenticating sent email** screen appears.
6. Choose either of the two options between **By verifying that the subject name on the certificate that the sending server uses to authenticate with Office 365 matches the domain entered in the text box below (recommended)** and **By verifying that the IP address of the sending server matches one of the following IP addresses, which belong exclusively to your organization**.

    Note

    If you choose the first option, provide your domain name (if your organization has only one domain) or any one of the domains of your organization (in case of multiple domains). If you choose the second option, provide the IP address of organization's domain server.
7. Click **Next**. The **Review connector** screen appears.
8. Review the settings you have configured, and click **Create connector**.

    The connector is created.

    If you need more information, select the **Help** or **Learn More** links. In particular, see [Identifying email from your email server](/en-us/previous-versions/exchange-server/exchange-150/dn910993%28v=exchg.150%29) for help configuring certificate or IP address settings for this connector. The wizard will guide you through set up. At the end, save your connector.

### 2. Set up your email server to relay mail to the internet via Microsoft 365 or Office 365

Next, you must prepare your email server to send mail to Microsoft 365 or Office 365. This configuration of the email server enables mail flow from your email servers to the Internet via Microsoft 365 or Office 365.

If your on-premises email environment is Microsoft Exchange, you create a Send connector that uses smart host routing to send messages to Microsoft 365 or Office 365. For more information, see[Create a Send connector to route outbound mail through a smart host](../../mail-flow/connectors/outbound-smart-host-routing).

To create the Send connector in Exchange Server, use the following syntax in the Exchange Management Shell. To learn how to open the Exchange Management Shell in your on-premises Exchange organization, see [Open the Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell).

Note

In the following procedures, the *CloudServicesMailEnabled* parameter is available in Exchange 2013 or later.

```powershell
New-SendConnector -Name <DescriptiveName> -AddressSpaces * -CloudServicesMailEnabled $true -Fqdn <CertificateHostNameValue> -RequireTLS $true -DNSRoutingEnabled $false -SmartHosts <YourDomain>-com.mail.protection.outlook.com -TlsAuthLevel CertificateValidation
```

This example creates a new Send Connector with the following properties:

- **Name**: My company to Office 365
- **FQDN**: mail.contoso.com
- **SmartHosts**: contoso-com.mail.protection.outlook.com

```powershell
New-SendConnector -Name "My company to Office 365" -AddressSpaces * -CloudServicesMailEnabled $true -Fqdn mail.contoso.com -RequireTLS $true -DNSRoutingEnabled $false -SmartHosts contoso-com.mail.protection.outlook.com -TlsAuthLevel CertificateValidation
```

## Change a connector that Microsoft 365 or Office 365 is using for mail flow

To change settings for a connector, select the connector you want to edit and then select the **Edit** icon as shown in the following screenshots, for New EAC and Classic EAC, respectively.

![The screen on which the option of editing connector details is chosen.](../../exchangeonline/media/editing-connector-new-eac.png)

[![Shows a screen shot with a connector selected and the edit (pencil) icon highlighted.](../../exchangeonline/media/9654b36f-40d2-4791-ae5c-ce3afd9bb683.png)](../../exchangeonline/media/9654b36f-40d2-4791-ae5c-ce3afd9bb683.png#lightbox)

The connector wizard opens, and you can make changes to the existing connector settings. While you change the connector settings, Microsoft 365 or Office 365 continues to use the existing connector settings for mail flow. When you save changes to the connector, Microsoft 365 or Office 365 starts using the new settings.

## What happens when I have multiple connectors for the same scenario?

Most customers don't need to set up connectors. For those customers who do, one connector per single mail flow direction is enough. But you can also create multiple connectors for a single mail flow direction, such as from Microsoft 365 or Office 365 to your email server (also called on-premises server).

When there are multiple connectors, the first step to resolving mail flow issues is to know which connector Microsoft 365 or Office 365 is using. Microsoft 365 or Office 365 uses the following order to choose a connector to apply to an email:

1. Use a connector that exactly matches the recipient domain.
2. Use a connector that applies to all accepted domains.
3. Use wildcard pattern matching. For example, \*.contoso.com would match mail.contoso.com and sales.contoso.com.

### Example of how Microsoft 365 or Office 365 applies multiple connectors

In this example, your organization has four accepted domains, contoso.com, sales.contoso.com, fabrikam.com, and contoso.onmicrosoft.com. You have three connectors configured from Microsoft 365 or Office 365 to your organization's email server. For this example, these connectors are known as **Connector 1**, **Connector 2**, and **Connector 3**.

**Connector 1** is configured for all accepted domains in your organization. The following screenshot shows the connectors wizard screen where you define which domains the connector applies to. In this case, the setting chosen is **For email messages sent to all accepted domains in your organization**. The following two screenshots depict the chosen setting for New EAC and Classic EAC, respectively.

![The connector wizard page for New EAC.](../../exchangeonline/media/365-applying-connectors-1.png)

![Shows the connector wizard page for Classic Exchange admin center: When do you want to use this connector? The second option is selected. This option is: For email messages sent to all accepted domains in your organization.](../../exchangeonline/media/313c3a28-a6f4-46fb-8d12-850216ab5046.png)

**Connector 2** is set up specifically for your company domain Contoso.com. The following screenshot shows the connectors wizard screen where you define which domains the connector applies to. In this case, the setting chosen is **Only when email messages are sent to these domains**. For **Connector 2**, your company domain Contoso.com is specified. The following two screenshots depict the chosen setting for New EAC and Classic EAC, respectively.

![The connector wizard screen for the New EAC.](../../exchangeonline/media/365-applying-connectors-2.png)

![Shows the connector wizard page in the Classic Exchange admin center: When do you want to use this connector? The third option is selected. This option is: Only when email messages are sent to these domains. The domain Contoso.com has been added.](../../exchangeonline/media/c68671c2-d8df-4791-a538-481eae397673.png)

**Connector 3** is also set up by using the option **Only when email messages are sent to these domains**. But, instead of the specific domain Contoso.com, the connector uses a wildcard: \*.Contoso.com as shown in the following screenshot. The following two screenshots depict the chosen setting for New EAC and Classic EAC, respectively.

![The connector wizard screen for the New Exchange admin center.](../../exchangeonline/media/365-applying-connectors-3.png)

![Shows the connector wizard page: When do you want to use this connector? The third option is selected. This option is: Only when email messages are sent to these domains. The domain specified includes a wildcard. *.contoso.com has been added.](../../exchangeonline/media/87f27555-e12c-4ad6-914a-d4439f405d43.png)

For each email sent from Microsoft 365 or Office 365 to mailboxes on your email server, Microsoft 365 or Office 365 selects the most specific connector possible. For email sent to:

- john@fabrikam.com, Microsoft 365 or Office 365 selects **Connector 1**.
- john@contoso.com, Microsoft 365 or Office 365 selects **Connector 2**.
- john@sales.contoso.com, Microsoft 365 or Office 365 selects **Connector 3**.