---
layout: Conceptual
title: Validate connectors in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/validate-connectors
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
description: If your organization has its own email server (also called on-premises server), you must set up connectors to enable mail flow between Microsoft 365 or Office 365 and your email server. For mail flow to work correctly, your connectors must be validated and turned on. Connector validation runs as part of the connector setup process. This article helps if you want to validate your connectors at a different time, or if you want to understand more about the process. Use built-in connector validation to test whether a connector is set up correctly and fix any mail flow issues before you turn the connector on.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 7805c2f9-302d-4409-a57f-2b4d8296cd5e
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: e113579e-5da4-50e4-bb37-cfd0a8907b50
document_version_independent_id: 4c59d5fe-ebc6-9fc3-bee5-2db0c5cac501
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/validate-connectors.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/validate-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/validate-connectors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: c29b1599-5a03-6de1-8dcd-2c4ea8b9a32f
---

# Validate connectors in Exchange Online | Microsoft Learn

If your organization has its own email server (also called on-premises server), you must set up connectors to enable mail flow between Microsoft 365 or Office 365 and your email server. For mail flow to work correctly, your connectors must be validated and turned on. Connector validation runs as part of the connector setup process. This article helps if you want to validate your connectors at a different time, or if you want to understand more about the process. Use built-in connector validation to test whether a connector is set up correctly and fix any mail flow issues before you turn the connector on.

Note

If you want to change connector settings, Microsoft 365 or Office 365 uses the existing connector settings for mail flow until you save your changes. For more information, see [Change a connector that Microsoft 365 or Office 365 is using for mail flow](set-up-connectors-to-route-mail#change-a-connector-that-microsoft-365-or-office-365-is-using-for-mail-flow)

## Validate and turn on connectors

This section describes the procedures to validate and turn on connectors in both the New Exchange admin center (EAC) and Classic EAC.

Before validating and turning on the connectors, sign in to Microsoft 365 or Office 365, choose **Admin**, and then select **Exchange** to go to the New EAC.

Note

To navigate to Classic EAC, you need not seperately launch its URL. You can navigate from New EAC interface by clicking **Classic Exchange admin center** on the left-bottom.

**For New EAC**

1. Navigate to **Mail flow &gt; Connectors**. The **Connectors** screen appears.

Note

Any Microsoft 365 or Office 365 connectors that exist for your organization are listed on the **Connectors** page. This list includes connectors that were created by using the Hybrid Configuration Wizard or PowerShell. You can validate any connector configured for mail flow from Microsoft 365 or Office 365 to your organization's email server, or to a partner organization.

1. Choose and click the connector you want to validate or turn on.

![The screen of New EAC on which the user chooses a connector for viewing its details.](../../exchangeonline/media/connector-chosen-in-new-eac.png)

1. Click the connector. The connector details screen appears.
2. View the information.

![The screen on which the validation history details for the connector is displayed.](../../exchangeonline/media/display-of-validation-details.png)

When you select a connector for mail flow that originates in Microsoft 365 or Office 365, you can choose the **Validate this connector** link. You can also see whether the connector was validated previously as shown in the following screenshot.

![The screen on which the link that enables connector validation is displayed.](../../exchangeonline/media/connector-validation-link.png)

1. Under **Status**, if **Off** is displayed, click **Edit name or status**. The **Connector name** screen appears.
2. Under **What do you want to do after connector is saved**, check the check box for **Turn it on**.
3. Click **Next**. The **Validation email** screen appears.
4. Enter an email address that is part of the active mailbox on your organization's email server.
5. Click **+**, and then click **Validate**. The validation process starts.
6. Once the validation process is completed, click **Save**.

The connector is updated successfully from **being turned off** to **being turned on**.

**For Classic EAC**

1. Navigate to the Classic EAC portal by clicking **Classic Exchange admin center**. Select **mail flow** and then **connectors**.

    Any Microsoft 365 or Office 365 connectors that exist for your organization are listed on the **Connectors** page. This includes connectors that were created by using the Hybrid Configuration Wizard or PowerShell. You can validate any connector configured for mail flow from Microsoft 365 or Office 365 to your organization's email server, or to a partner organization.
2. Choose the connector you want to validate or turn on. You can see information about the connector in the details pane as shown in the following screen shot.

    ![Shows a connector from Microsoft 365 or Office 365 to an Exchange Server that is turned off and has failed validation.](../../exchangeonline/media/94d4c6ed-70d0-4a1d-915b-9d089f58d714.png)
3. When you select a connector for mail flow that originates in Microsoft 365 or Office 365, you can choose the **Validate this connector** link. You can also see whether the connector was validated previously as shown in the following screen shot.

    ![Shows a connector that was previously validated and a link to validate the connector again.](../../exchangeonline/media/e563a5dd-5e3c-4e78-8d3b-1e4b05a8e5d1.png)
4. With the connector selected, choose **Validate this connector**. The **Validate this connector** dialog box opens. Enter one or more email addresses to start the validation. Microsoft 365 or Office 365 uses these addresses to make sure your mail flow is set up correctly. For example, if you want to validate a connector for mail flow from Microsoft 365 or Office 365 to your organization's email server, enter an email address for a mailbox located on that email server.
5. Choose **Validate** to continue. To find out what issues validation examines, and for details about fixing any validation errors, see [Validate connectors](validate-connectors).
6. For each connector, check whether the connector is turned on. If a connector that you need for mail flow isn't turned on, under **Status** choose **Turn it on**.

Note

If you continue to have mail flow issues after validating a connector, check whether you have set up multiple connectors that might apply in a single scenario. For example, problems can occur if you have more than one connector set up for mail flow from Microsoft 365 or Office 365 to your email server. If you need multiple connectors for mail flow from Microsoft 365 or Office 365 to your email server (or to a partner), ensure you validate and turn on each connector. If you want to change a connector, Microsoft 365 or Office 365 uses the existing connector settings for mail flow until you save your changes. For more information, see [Change a connector that Microsoft 365 or Office 365 is using for mail flow](set-up-connectors-to-route-mail#change-a-connector-that-microsoft-365-or-office-365-is-using-for-mail-flow)