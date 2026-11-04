---
layout: Conceptual
title: Set up a connector to apply security restrictions to mail sent from your partner organization to Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-secure-mail-sent-from-partner-organization
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
description: You can set up connectors to apply security restrictions for mails sent from your partner organization to Microsoft 365 or Office 365.
ms.topic: install-set-up-deploy
author: v-smandalika
ms.author: v-smandalika
ms.assetid: 1ce4d6a4-41ba-4d1e-9ca9-e826252c1041
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2023-10-20T00:00:00.0000000Z
locale: en-us
document_id: 60725e3c-0551-9586-c9cd-102673eec9b1
document_version_independent_id: 7f381167-926d-8999-5b37-c953404a6d50
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-secure-mail-sent-from-partner-organization.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-secure-mail-sent-from-partner-organization
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-secure-mail-sent-from-partner-organization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 14d81674-05ac-d5d1-4946-c67c4ef218ae
---

# Set up a connector to apply security restrictions to mail sent from your partner organization to Microsoft 365 or Office 365 | Microsoft Learn

You can set up a connector to apply security restrictions to emails that your partner organization sends to you. The procedure to set up a connector is described as follows:

## For New EAC

1. Navigate to **Mail flow &gt; Connectors**. The **Connectors** screen appears.
2. Select **+Add a connector**. The **New connector** screen appears.

![Screenshot that shows the screen on which the process to create a connector begins.](../../exchangeonline/media/home-screen-to-add-a-new-connector.png)

1. Under **Connection from**, choose **Partner organization**.

Note

Once you select the **Partner organization** radio button under **Connection from**, the option under **Connection to** is greyed out, implying that **Office 365** is chosen by default.

![Screenshot that shows the screen on which a connector is set up to apply security restrictions.](../../exchangeonline/media/partner-to-365-new-eac.png)

1. Select **Next**. The **Connector name** screen appears.
2. Provide a name for the connector and select **Next**. The **Authenticating sent email** screen appears.
3. Choose one of the two options between **By verifying that the sender domain matches one of the following domains** and **By verifying that the IP address of the sending server matches one of the following IP addresses, which belong to your partner organization**.

Note

If you choose **By verifying that the sender domain matches one of the following domains**, you can provide the name of any one domain from the list of domains for your organization. If you have only one domain for your organization, enter its name. If you choose **By verifying that the IP address of the sending server matches one of the following IP addresses, which belong to your partner organization**, provide an IP address of any of the recipients who are part of your organization's mailbox.

1. Select **Next**. The **Security restrictions** screen appears.
2. Check the **Reject email messages if they aren't sent over TLS** checkbox.

Note

It's optional to choose the option of **And require that the subject name of the certificate that the partner uses to authenticate with Office 365 matches this domain name**. If you choose this option, enter the domain name of the partner organization.

1. Check the **Reject email messages if they aren't sent from within this IP address range** checkbox, and provide the IP address range.

Important

You can choose this option in addition to the option specified in Step 5; Else, you can choose either this option or the one in Step 5. Choosing at least one of these options is mandatory.

1. Select **Next**. The **Review connector** screen appears.
2. Review the settings you've configured, and select **Create connector**.

The connector is created.

Note

For more information, select the **Help** or **Learn More** links. In particular, see [Identifying email from your email server](/en-us/previous-versions/exchange-server/exchange-150/dn910993%28v=exchg.150%29) for help in configuring certificate or IP address settings for this connector. The wizard will guide you through the setup.

## For Classic EAC

To start the wizard, click **+**. On the first screen, choose the options as shown in the following screenshot:

![Screenshot that shows connector from partner organization to Microsoft 365 or Office 365.](../../exchangeonline/media/e6d15001-989b-48b3-a848-427b800c2a70.png)

Select **Next**, and follow the instructions in the wizard. For more information, select the **Help** or **Learn More** links. The wizard will guide you through the setup. At the end, save your connector.

Ask your partner organization to send a test email. Ensure that the email your partner organization sends will cause the connector to be applied. For example, if you specified security restrictions for mails sent from a specific partner domain, ensure they send test mail from that domain. Check that the test email is delivered to confirm that the connector works correctly.