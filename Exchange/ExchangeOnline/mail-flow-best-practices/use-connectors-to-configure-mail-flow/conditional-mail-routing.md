---
layout: Conceptual
title: Scenario Conditional mail routing in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/conditional-mail-routing
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
description: Admins can learn how to use connectors and mail flow rules to route mail in Exchange Online
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 82d105e2-e955-4e03-99c3-3314a5d21a4c
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: ba3d06e8-313a-0679-bf8d-a1133c96d5af
document_version_independent_id: 888988e6-84de-15aa-492a-e44ba2d5f711
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/conditional-mail-routing.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/conditional-mail-routing
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/conditional-mail-routing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 75145cf4-9d91-f19a-d702-4371f9339595
---

# Scenario Conditional mail routing in Exchange Online | Microsoft Learn

There might be times you need to route mail differently. These different routes depend on the recipient or sender of the mail, where it's being sent, the contents of the message, and so on. For example, if you have multiple sites around the world, you might want to route mails to a specific site. You can do this using connectors and mail flow rules (also known as transport rules).

When the steps below are completed, a mail flow rule will redirect messages addressed to users whose City property is set to New Orleans to the IP address specified by the connector from Office 365 to your organization's email server.

## Step 1: Use the Exchange admin center to create the connector

The first thing we need to do is create a connector from Office 365 to your organization's email server. This connector will be used by the mail flow rule that we'll set up in Step 2. In this connector, you'll select where received messages originate from (such as a mailbox in your Microsoft 365 or Office 365 organization), the type of organization to which the messages will be sent (such as your on-premises servers), the security that should be applied to the connection, and name or IP address of the target server. If you want to learn more about how to create connectors, check out [Configure mail flow using connectors](use-connectors-to-configure-mail-flow).

The subsequent two procedures are for creating connectors from Office 365 to your organization's email server. These connectors are to be created in the Exchange admin center (EAC).

1. Navigate to **Mail flow** &gt; **Connectors**. The **Connectors** screen appears.
2. Click **+ Add a new connector**. The **New connector** screen appears.
3. Under **Connection from**, choose **Office 365**.
4. Under **Connection to**, choose either **Your organization's email server** or **Partner organization** (if you want to connect to a server other than your organizations).

![The screen on which a connector is being created from Office 365 to your organization's mail server](../../exchangeonline/media/365-to-your-organization.png)

1. Click **Next**. The **Connector name** screen appears.
2. Provide a name for the connector and add a description.
3. Check the check box for **Turn it on** under **What do you want to do after connector is saved?**

![The screen on which a name is given to the connector that is then turned on.](../../exchangeonline/media/providing-a-connector-name-and-turning-on.png)

1. Click **Next**. The **Use of connector** screen appears.
2. Choose **Only when I have a transport rule set up that redirects messages to this connector**.

![A screen on which the transport rule is chosen as a condition.](../../exchangeonline/media/configuring-transport-rule.png)

1. Click **Next**. The **Routing** screen appears.
2. Enter one or more smart hosts in the text box. (These smart hosts are the ones to which Microsoft 365 or Office 365 will deliver email messages.)

Note

You must provide either the domain name or the IP address of the server.

1. Click **+**. The smart host value is displayed under the text box.

![The screen on which the smart host address is defined.](../../exchangeonline/media/specifying-smart-host.png)

Note

It is mandatory to click **+** after entering the smart host name to navigate to the next screen.

1. Click **Next**. The **Security restrictions** screen appears.
2. Check the check box for **Always use Transport Layer Security (TLS) to secure the connection (recommended)**.

![The screen on which TLS settings are defined.](../../exchangeonline/media/define-tls-settings.png)

1. Click **Next**. The **Validation email** screen appears.
2. Enter an email address that is valid on the mailbox of your organization's email server.
3. Click **+**. The email address is displayed below the text box, indicating it is ready to be validated.
4. Click **Validate**. The validation process starts.
5. Once the validation process is completed, click **Next**. The **Review connector** screen appears.
6. Review the settings for the new connector and click **Create connector**. The connector is created.

## Step 2: Use the EAC to create a mail flow rule

Now that we've created a connector, we need to create a mail flow rule that will send mail to it based on the criteria you define. There are many conditions you can select from to control when messages should be sent to the connector. In the following example, we are setting rule condition based on specific properties of the recipient.

To create a mail flow rule in EAC, perform the following steps:

1. In the EAC, navigate to **Mail flow** &gt; **Rules**. Click ![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif)**Add a rule** and choose **Create a new rule...**.
2. In the **New rule** window, name the rule.
3. For **Apply this rule if\***, select **The recipient...** and **has specific properties including any of these words**. The **Select user properties** box appears. Under **User property**, choose **City**. **City** is an Active Directory attribute made available for use by the rule. Specify the name of the city, such as New Orleans. Click **Add**, and then click **Save** to close the **Select user properties** box.

    ![Screenshot of apply rule if.](../../exchangeonline/media/apply-rule.png)

    Important

    Check the accuracy of user attributes in Active Directory to ensure that the mail flow rule works as intended. &gt; Note that changes made in the connector from Office 365 to your organization's email server take time to replicate.
4. For **\*Do the following...**, choose **Redirect the message to...** and then specify **the following connector**. The **select connector** box appears. Choose the connector (from Office 365 to your organization's email server) that you created previously.

    You can choose more properties for the rule, such as the test mode and when to activate the rule.
5. To save the connector, click **Save**.