---
layout: Conceptual
title: Scenario Integrate Microsoft 365 or Office 365 with an email add-on service | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/integrate-office-365-with-an-email-add-on-service
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
description: Admins can learn how to integrate Microsoft 365 or Office 365 with a third-party service that affects mail flow.
ms.topic: integration
author: AshaIyengar21
ms.author: serdars
ms.assetid: 7c5b7408-bfa2-4695-a6b7-21ddc8084d52
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: f44c94af-aa03-b648-7c87-6f77e9ada172
document_version_independent_id: 2608dfd4-92a4-1c8e-5675-26ce9f3423a2
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/integrate-office-365-with-an-email-add-on-service.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/integrate-office-365-with-an-email-add-on-service
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/integrate-office-365-with-an-email-add-on-service.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 758b6877-1753-5369-a1be-7cf26b56357a
---

# Scenario Integrate Microsoft 365 or Office 365 with an email add-on service | Microsoft Learn

Many third-party cloud service solutions provide add-on services for Exchange Online. For security reasons, we don't allow third-party email add-on services to be installed in Exchange Online. But, you can work with the service provider to configure the settings in your Exchange Online organization so that you can use the service.

This topic describes the best practices for how your organization can use a third-party email add-on service by examining a fictional service named Contoso Signature Service. This fictional service runs in Azure and provides custom email signatures.

Note

This service could be deployed in a cloud environment other than Azure.

The mail flow and a high-level summary of the service are shown in the following diagram.

![Functional diagram for fictional Contoso Signature Service email add-on service.](../../exchangeonline/media/a38e832b-0b37-49d8-9074-c9dc6f7710b3.png)

1. When a user in your Exchange Online organization composes and sends a message, the message is diverted to Contoso Signature Service by using a connector and a mail flow rule (also known as a transport rule) that you create.

    Connections from Exchange Online to Contoso Signature Service are encrypted by TLS, because you configure the certificate domain name for the service in the connector settings (for example, smtp.contososignatureservice.com).
2. Contoso Signature Service accepts the message and adds an email signature to the message. The service also stamps the message with a custom header to indicate the message has been processed.
3. Contoso Signature Service routes the message back to Exchange Online. A connector that you create accepts the incoming messages from Contoso Signature Service.

    - Contoso Signature Service uses smart host routing to route messages back to the region where your Exchange Online organization is located. For example, if your Exchange Online domain is fabrikam.onmicrosoft.com, the destination smart host is fabrikam.mail.protection.outlook.com.
    - Contoso Signature Service provides a unique certificate domain name for each customer. You configure this domain name as an accepted domain in your Exchange Online organization and in the connector settings (for example, S5HG3DCG14.smtp.contososignatureservice.com).
4. Exchange Online sends the message with the customized signature to the original recipients.

The rest of this topic explains how to configure mail flow in Exchange Online to work with the email add-on service.

Note

These elements are required for any email add-on service that you want to integrate with your Exchange Online organization. You need to work with the email add-on service provider to configure their required settings in Exchange Online.

Important

This article discusses integrating Exchange Online with an email add-on service. If you're considering integrating non-Microsoft security services with Microsoft 365, please see [Considerations for integrating non-Microsoft security services with Microsoft 365.](/en-us/defender-office-365/mdo-integrate-security-service)

## What do you need to know before you begin?

- Estimated time to complete: 15 minutes
- You need permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mail flow" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center). To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Step 1: Create a connector that routes messages from Office 365 to the email add-on service

The important settings for the connector are:

- From Office 365 to the email add-on service.
- Uses smart host routing to the email add-on service.
- Uses TLS to encrypt the connection based on the domain name of the email add-on service (smart host).

### Use the EAC to create the connector that routes messages from Office 365 to the email add-on service

### Create the outbound connector in the EAC

1. In the EAC, go to **Mail flow** &gt; **Connectors**, and then click **Add a connector**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif).

    ![The connectors screen.](../../exchangeonline/media/connectors-screen.png)
2. The new connector wizard opens. On the first page, configure these settings:

    - **Connection from**: Select **Office 365**.
    - **Connection to**: **Your organization's email server**

    ![The screen on which the path Office 365 to Your organization's email server is chosen](../../exchangeonline/media/365-to-org.png)

    When you're finished, click **Next**.
3. On the next page, configure these settings:

    - **Name**: Enter a descriptive name (for example, Office 365 to Contoso Signature Service).
    - **Description**: Enter an optional description.
    - **What do you want to do after connector is saved?**: Configure these settings:
        - **Turn it on** leave this value selected.
        - **Retain internal Exchange email headers (recommended)**: Configure one of these values:
            - **Checked**: Preserves internal headers in messages that are sent to the email add-on service, which means the messages are treated as trusted internal messages. If you select this value, you'll also need to use the same value on this setting for the inbound connector that you create in Step 4 (otherwise, the inbound connector will remove the internal Exchange headers from the returning messages).
            - **Unchecked**: Removes internal headers from messages before they're sent to the email add-on service. If you select this value, the value of this setting on the inbound connector that you create in Step 4 is meaningless (by definition, there will be no internal Exchange headers to keep or remove in returning messages).

    ![The screen on which you provide a name for the connector.](../../exchangeonline/media/connectors-name.png)

    When you're finished, click **Next**.
4. On the **Use of connector** page, select **Only when I have a transport rule set up that redirects messages to this connector**, and then click **Next**.

    ![The screen displaying options that determine how you use your connector.](../../exchangeonline/media/screen-use-of-connector.png)
5. On the **Routing** page, enter the smart host value click or the email add-on service (for example, smtp.contososignatureservice.com), click **Add**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif), and then click **Next**.

    ![The screen displaying options that determine how the connectors route the email messages.](../../exchangeonline/media/screen-routing.png)
6. On the **Security restrictions** page, configure these settings:

    - Verify **Always use Transport Layer Security (TLS) to secure the connection (recommended)** is selected.
    - Verify **Issued by a trusted certificate authority (CA)** is selected.
    - Select **And the subject name or subject alternative name (SAN) matches this domain name**, and enter the smart host that you used in the previous step (for example, smtp.contososignatureservice.com).

    ![The screen displaying options that determine how Office 365 connects to your organization's email server](../../exchangeonline/media/screen-security-restrictions.png)

    When you're finished, click **Next**.
7. On the **Validation email** page, do these steps:

    1. Enter a valid email address on your organization's email server, and then click **Add**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif).
    2. Click **Validate** to start the validation process.

    After the validation process is complete, click **Next**.

    ![The Validation email screen.](../../exchangeonline/media/screen-validation-email.png)
8. On the **Review connector** page, review the settings for the new connector. You can click **Edit** in the specific section to edit those settings.

    When you're finished, click **Create connector**.

    ![The screen on which you can review the settings of the connector.](../../exchangeonline/media/screen-review-connector.png)

### Use Exchange Online PowerShell to create the outbound connector to the email add-on service

To create the outbound connector to the email add-on service in Exchange Online PowerShell, use this syntax:

```powershell
New-OutboundConnector -Name "<Descriptive Name>" -ConnectorType OnPremises -IsTransportRuleScoped $true -UseMxRecord $false -SmartHosts <SmartHost> -TlsSettings DomainValidation -TlsDomain <SmartHost> [-CloudServicesMailEnabled $true]
```

This example creates an outbound connector with these settings:

- **Name**: Office 365 to Contoso Signature Service
- **Smart host destination of the email add-on service**: smtp.contososignatureservice.com
- **TLS domain for domain validation**: smtp.contososignatureservice.com
- Internal Exchange message headers that identify messages as internal are preserved in the outbound messages.

```powershell
New-OutboundConnector -Name "Office 365 to Contoso Signature Service" -ConnectorType OnPremises -IsTransportRuleScoped $true -UseMxRecord $false -SmartHosts smtp.contososignatureservice.com -TlsSettings DomainValidation -TlsDomain smtp.contososignatureservice.com -CloudServicesMailEnabled $true
```

For detailed syntax and parameter information, see [New-OutboundConnector](/en-us/powershell/module/exchangepowershell/new-outboundconnector).

### Verify that you've successfully created the outbound connector

To verify that you've successfully created an outbound connector to route messages to the email add-on service, use either of these procedures:

- In the EAC, go to **Mail flow** &gt; **Connectors**, select the connector, and then verify the settings.
- In Exchange Online PowerShell, replace *&lt;Connector Name&gt;* with the name of the connector, and run this command to verify the property values:

    ```powershell
    Get-OutboundConnector -Identity "<Connector Name>" | Format-List Name,ConnectorType,IsTransportRuleScoped,UseMxRecord,SmartHosts,TlsSettings,TlsDomain,CloudServicesMailEnabled
    ```

## Step 2: Create a mail flow rule to route unprocessed messages to the email add-on service

The rule routes messages from internal senders to the connector that you created in Step 1 if the messages haven't already been processed by the email add-on service (the custom header isn't stamped on the message).

### Use the EAC to create a mail flow rule to route unprocessed messages to the email add-on service

Note

Mail flow rule creation in the new EAC is exactly the same as in the classic EAC.

1. Go to **Mail flow** &gt; **Rules**, and click **New**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif), and then select **Create a new rule**.

    ![In the Exchange admin center, click Mail flow &gt; Rules to add a new rule.](../../exchangeonline/media/568bbbf2-e69a-4d59-b7d4-b1af06655433.png)
2. In the **New rule** page that opens, click **More options** near the bottom of the page.

    ![On the new rule page, click More options.](../../exchangeonline/media/18f546af-b5ab-4bce-ac9c-23609816da7e.png)
3. On the **New rule** page, configure these settings:

    - **Name**: Enter a descriptive name (for example, Route email to Contoso Signature Service).
    - **Apply this rule if**: Select **The sender** &gt; **Is external/internal** &gt; Select **Inside the organization**, and then click **OK**.
    - **Do the following**: Select **Redirect the message to** &gt; **The following connector** &gt; Select the connector you created in Step 1, and then click **OK**.
    - **Except if**: Click **Add exception** &gt; Select **A message header** &gt; **Includes any of these words**.
    - Click **Enter text**, enter the name of the custom header field that's applied by the email add-on service (for example, SignatureContoso), and then click **OK**.
    - Click **Enter words**, enter the header field value that indicates a message has been processed by the email add-on service (for example, true), click **Add**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif), and then click **OK**.
    - Near the bottom of the page, select **Stop processing more rules**.

    ![On the new rule page, configure the settings to route messages to the email add-on service.](../../exchangeonline/media/97e895ea-fbf5-437b-a23c-13adf8db93ac.png)

    When you're finished, click **Save**.

### Use Exchange Online PowerShell to create a mail flow rule to route unprocessed messages to the email add-on service

To create the mail flow rule in Exchange Online PowerShell, use this syntax:

```powershell
New-TransportRule -Name "<Descriptive Name>" -FromScope InOrganization -RouteMessageOutboundConnector "<Connector Name>" -ExceptIfHeaderContainsMessageHeader <HeaderName> -ExceptIfHeaderContainsWords <HeaderValue> -StopRuleProcessing $true
```

This example creates the mail flow rule with these settings:

- **Name**: Route email to Contoso Signature Service
- **Outbound connector name**: Office 365 to Contoso Signature Service
- **Header field and value that indicates processing by the email add-on service**SignatureContoso with the value true.

```powershell
New-TransportRule -Name "Route email to Contoso Signature Service" -FromScope InOrganization -RouteMessageOutboundConnector "Office 365 to Contoso Signature Service" -ExceptIfHeaderContainsMessageHeader SignatureContoso -ExceptIfHeaderContainsWords true -StopRuleProcessing $true
```

For detailed syntax and parameter information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).

### Verify that you've successfully created the mail flow rule

To verify that you've successfully created a mail flow rule to route unprocessed messages to the email add-on service, use either of these procedures:

- In the EAC, go to **Mail flow** &gt; **Rules**, select the rule, click **Edit**![Edit icon.](../../exchangeonline/media/itpro_eac_editicon.gif), and verify the settings of the rule.
- In Exchange Online PowerShell, replace *&lt;Rule Name&gt;* with the name of the rule, and run this command to verify the property values:

    ```powershell
    Get-TransportRule -Identity "<Rule Name>" | Format-List Name,FromScope,RouteMessageOutboundConnector,ExceptIfHeaderContainsMessageHeader,ExceptIfHeaderContainsWords,StopRuleProcessing
    ```

## Step 3: Add the custom certificate domain provided by the email add-on service as an accepted domain in Exchange Online

1. In the Microsoft 365 admin center at https://admin.microsoft.com, go to **Settings** &gt; **Domains**, and then click **Add domain**.

    ![The Domains page in the Microsoft 365 admin center.](../../exchangeonline/media/5d4db406-5970-45f4-8955-2bc90d087b6f.png)
2. The add a domain wizard starts. On the **Add a domain** page, enter the custom certificate domain that the email add-on service provided when you enrolled in the service (for example, S5HG3DCG14.smtp.contososignatureservice.com), and then click **Use this domain**.

    **Note**: The value must be 48 characters or less.

    ![Enter the custom certificate domain provided by the email add-on service.](../../exchangeonline/media/b131c36a-754e-4096-8532-1c2c716ef970.png)
3. On the **Domain verification** page, select one of the following values:

    - **Add a TXT record to the domain's DNS records**
    - **If you can't add a TXT record, add an MX record to the domain's DNS records**

    When you're finished, click **Continue**.
4. The next page that you see depends on your previous selection. Use the details on the page to create the required TXT or MX proof of domain ownership record for the custom certificate domain.

    After you've created the proof of domain ownership record, click **Verify** and wait for the results.

    ![The TXT proof of domain ownership record for the custom certificate domain.](../../exchangeonline/media/fd0ab875-925d-46ea-96fd-00924e6f298f.png)
5. On the **Connect domain** page, click **Save and close**.

For more information, see [Add your domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).

## Step 4: Create a connector that receives messages from the email add-on service

The important settings for the connector are:

- From the email add-on service to Office 365.
- TLS encryption and certificate verification is based on the custom certificate domain name that you configured as an accepted domain in the previous step.

### Use the EAC to create a connector that receives messages from the email add-on service

#### Create the inbound connector in the EAC

1. Go to **Mail flow** &gt; **Connectors**, and then click ![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif)**Add a connector**.

    ![The connectors screen.](../../exchangeonline/media/connectors-screen.png)
2. The new connector wizard opens. On the first page, configure these settings:

    - **Connection from**: Select **Your organization's email server**.
    - **Connection to**: Verify that **Office 365** is selected.

    ![The screen on which connector settings are configured.](../../exchangeonline/media/org-to-365.png)
3. When you're finished, click **Next**.
4. On the **Connector name** page, configure these settings:

    - **Name**: Enter a descriptive name (for example, Contoso Signature Service to Office 365).
    - **Description**: Enter an optional description.
    - **What do you want to do after connector is saved?**: Configure these settings:
        - **Turn it on**: Verify that this setting is selected.
        - **Retain internal Exchange email headers (recommended)**: Configure one of these values:
            - **Checked**: Preserves internal headers in messages that are returning from the email add-on service. If you selected this value on this setting for the connector that you create in Step 1, you'll need to configure the same value here. The internal Exchange headers in the returning messages are preserved, which means the messages returning from the email add-on service are treated as trusted internal messages.
            - **Unchecked**: Removes the internal Exchange headers (if any) from messages that are returning from the email add-on service.

    ![The screen on which you provide a name to the connector.](../../exchangeonline/media/screen-connector-name.png)

    When you're finished, click **Next**.
5. On the **Authenticating sent email** page, verify that the first option is selected (verify by certificate), and enter the certificate domain that the email add-on service gave to you when you enrolled in the service (for example, S5HG3DCG14.smtp.contososignatureservice.com).

    ![The authenticating sent email screen.](../../exchangeonline/media/authenticating-sent-email.png)

    When you're finished, click **Next**.
6. On the **Review connector** page, verify the settings. You can click **Edit** in the appropriate section to make changes. When you're finished, click **Create connector**\*.

    ![The review connector screen.](../../exchangeonline/media/screen-review-connector-org-365.png)

### Use Exchange Online PowerShell to create an inbound connector to receive messages from the email add-on service

To create the inbound connector from the email add-on service in Exchange Online PowerShell, use this syntax:

```powershell
New-InboundConnector -Name "<Descriptive Name>" -SenderDomains * -ConnectorType OnPremises -RequireTls $true -RestrictDomainsToCertificate $true -TlsSenderCertificateName <CertificateDomainName> [-CloudServicesMailEnabled $true]
```

- **Name**: Contoso Signature Service to Office 365
- **Domain name used by the email add-on service's certificate to authenticate with your Office 365 organization**: S5HG3DCG14.smtp.contososignatureservice.com
- Internal Exchange message headers that identify messages as internal are preserved in the outbound messages.

```powershell
New-InboundConnector -Name "Contoso Signature Service to Office 365" -SenderDomains * -ConnectorType OnPremises -RequireTls $true -RestrictDomainsToCertificate $true -TlsSenderCertificateName S5HG3DCG14.smtp.contososignatureservice.com -CloudServicesMailEnabled $true
```

For detailed syntax and parameter information, see [New-InboundConnector](/en-us/powershell/module/exchangepowershell/new-inboundconnector).

### Verify that you've successfully created the inbound connector

To verify that you've successfully created an inbound connector to receive messages from the email add-on service, use either of these procedures:

- In the EAC, go to **Mail flow** &gt; **Connectors**, select the connector, and then verify the settings.
- In Exchange Online PowerShell, replace *&lt;Connector Name&gt;* with the name of the connector, and run this command to verify the property values:

    ```powershell
    Get-InboundConnector -Identity "<Connector Name>" | Format-List Name,SenderDomains,ConnectorType,RequireTls,RestrictDomainsToCertificate,TlsSenderCertificateName,CloudServicesMailEnabled
    ```