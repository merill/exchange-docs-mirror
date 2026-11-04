---
layout: Conceptual
title: Set up a connector to apply security restrictions to mail sent from Microsoft 365 or Office 365 to your partner organization | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-secure-mail-sent-to-partner-organization
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
description: You can set up connectors to apply security restrictions for mails sent from Microsoft 365 or Office 365 to your partner organization.
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
document_id: ce0f13ce-ba34-f19c-c741-8d64aa87a9d6
document_version_independent_id: 0d15903f-098d-2467-4e64-cc76a90f091e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-secure-mail-sent-to-partner-organization.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-secure-mail-sent-to-partner-organization
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-secure-mail-sent-to-partner-organization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 23e5ee8b-5b90-5740-e391-bf5221a8fff3
---

# Set up a connector to apply security restrictions to mail sent from Microsoft 365 or Office 365 to your partner organization | Microsoft Learn

This section describes the process of setting up a connector in both the New Exchange admin center (EAC) and the Classic EAC. Before you set up a new connector, do the following tasks:

- Check for any connectors that are already listed here for your organization. For example, if you already have a connector set up for a partner organization, you'll see it listed. Ensure you don't create duplicate connectors for a single organizational partner; when this duplication happens, it can cause errors, and your mail might not be delivered.

If any connectors already exist for your organization, you can see them listed here, as shown in the below screenshots for New EAC and Classic EAC, respectively.

![Screenshot that shows existing list of connectors.](../../exchangeonline/media/new-exchange-admin-center.png)

![Screenshot that shows Microsoft 365 and Office 365 connectors partner organization examples.](../../exchangeonline/media/9e8f0035-24b6-4d62-aecf-17f740530e31.png)

- Navigate to the new EAC from the Microsoft 365 admin center by selecting **Exchange** under the **Admin centers** pane.

Below are the procedures to set up a new connector.

## For New EAC

1. Navigate to **Mail flow &gt; Connectors**. The **Connectors** screen appears.
2. Select **+Add a connector**. The **New connector** screen appears.
3. Under **Connection from**, choose **Office 365**.
4. Under **Connection to**, choose **Partner Organization**.

![Screenshot that shows the screen on which a connector for Office 365 is added.](../../exchangeonline/media/office-365-to-partner.png)

1. Select **Next**. The **Connector name** screen appears.
2. Provide a name for the connector and select **Next**. The **Use of connector** screen appears.
3. Choose any one of the two options between **Only when I have a transport rule set up that redirects messages to this connector** and **Only when email messages are sent to these domains**.

Note

If you choose the second option, provide the name of any one of the domains that are part of your organization. If there is only one domain for your organization, enter its name.

1. Click **+** (after entering the domain name, if you have chosen **Only when email messages are sent to these domains**)

The domain name is displayed under the text box.

1. Select **Next**. The **Routing** screen appears.
2. Choose any of the two options between **Use the MX record associated with the partner's domain** and **Route email through these smart hosts**.
3. Select **Next**. The **Security restrictions** screen appears.

Note

If you choose the first option, you need not mention the details of smart host. If you choose second option, enter the domain name of the smart host in the text box.

1. Check the **Always use Transport Layer Security (TLS) to secure the connection (recommended)** checkbox.

Note

It's not mandatory to configure the TLS settings on the **Security restrictions** page. You can navigate to the next screen without choosing anything on this screen. The need to define TLS settings on this page depends on whether the destination server supports TLS or not.

1. Choose one of the options under **Connect only if the recipient's email server certificate matches this criteria**.

Note

If you're choosing the **Issue by a trusted certificate authority (CA)** option, the **Add the subject name or subject alternative name (SAN) matches this domain name** option is activated.

It's optional to choose the **Add the subject name or subject alternative name (SAN) matches this domain name** option. However, if you choose it, you must enter the domain name to which the certificate name matches.

1. Select **Next**. The **Validation email** screen appears.
2. Enter an email address that's part of the mailbox in your organization's email server.
3. Click **+**.
4. Select **Validate**. The validation process starts.
5. Once the validation process is completed, select **Next**. The **Review connector** screen appears.
6. Review the settings you've configured, and select **Create connector**.

The connector is created.

Note

For more information about the setup, select the **Help** or **Learn More** links.

1. At the end, ensure your connector validates. If the connector doesn't validate, see [Validate connectors](validate-connectors) for help with resolving issues.

## For Classic EAC

Navigate to the Classic EAC portal by selecting **Classic Exchange admin center**. Select **mail flow** and then **connectors**.

To start the wizard, click **+**. On the first screen, choose the options that are depicted in the following screenshot:

![Screenshot that shows Microsoft 365 and Office 365 to partner organization connector options.](../../exchangeonline/media/93cb9e70-f8d8-4e63-bb92-caafd8b79ad7.png)

Select **Next**, and follow the instructions in the wizard. For more information, select the **Help** or **Learn More** links. The wizard will guide you through the setup. At the end, ensure your connector validates. If the connector doesn't validate, see [Validate connectors](validate-connectors) for help with resolving issues.

If you want to create a secure channel with your partner organization in both directions, set up a connector that restricts mail flow from your partner organization to Microsoft 365 or Office 365.