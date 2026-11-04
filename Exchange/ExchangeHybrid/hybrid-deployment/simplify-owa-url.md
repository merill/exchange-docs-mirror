---
layout: Conceptual
title: Simplify the Outlook Web App URL for Microsoft 365 or Office 365 Hybrid | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/simplify-owa-url
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: how-to
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- M365-email-calendar
ms.assetid: 19449aee-3796-4298-90c6-c7579b8d2f7a
ms.reviewer: 
description: Learn how to configure a URL for Outlook on the web (Outlook Web App) for cloud mailbox users in a hybrid environment.
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: f30c4fd6-0e69-cb9a-6a21-327f0ebae3a7
document_version_independent_id: d0217aa4-a37b-8837-4310-108fbf533a5d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/simplify-owa-url.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/simplify-owa-url
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/simplify-owa-url.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 97b942ed-2796-7365-645c-799d2f502928
---

# Simplify the Outlook Web App URL for Microsoft 365 or Office 365 Hybrid | Microsoft Learn

Learn how to configure a URL for Outlook on the web (Outlook Web App) for cloud mailbox users in a hybrid environment.

A major concern for organizations that move to Microsoft 365 or Office 365 from on-premises Exchange is the user experience. Users need uninterrupted access to their mailboxes regardless of where or when their mailbox is moved. With that in mind, the Outlook on the web (formerly known as Outlook Web App) coexistence story is important.

Consider the following scenario: a company uses a hybrid deployment to move some of their mailboxes from on-premises Exchange to Microsoft 365 or Office 365. On Friday before the move, the users accessed their on-premises mailboxes by using the URL `https://mail.contoso.com/owa`. On Monday after the move, those same users now get an error when they try to access their mailboxes by using that URL.

To allow the affected users to connect to their mailboxes by using Outlook on the web, you have two options:

- **Tell the users the new URL (for example, https://outlook.com/owa/contoso.com)**: The issues with this option are:

    - The URL is complex.
    - The experience isn't seamless for the affected users.
- **Configure the *TargetOWAUrl* setting on the organization relationship**: The issues with this option are:

    - The endpoint for the cloud mailboxes is external (it's not in the domain that users expect).
    - The endpoint requires the domain in the URL (to distinguish between Microsoft 365 Apps for business and outlook.com consumer offerings).
    - The endpoint causes users to see certificate mismatch warnings.

To eliminate these issues for users with cloud mailboxes, perform the following steps:

1. **Create a CNAME record in DNS (for example, cloudowa.contoso.com) that points to mail.office365.com**:

    - Be sure to create this CNAME record in your internal and external (public) DNS, because users might connect from internal or external Internet connections.
    - In our example, the domain contoso.com is used in the request (the cloudowa part is dropped). This means you don't need to specify the domain in the URL.
2. **Configure the Outlook on the web redirect in the on-premises organization relationship**: To do this, use the following syntax in the Exchange Management Shell in on-premises Exchange:

    ```
    Set-OrganizationRelationship -Identity <Organization relationship identity> -TargetOWAUrl http://<CNAME value>/owa
    ```

    For example, if the CNAME record that you created in Step 1 is cloudowa.contoso.com, and the organization relationship name is Contoso Cloud, run the following command:

    ```
    Set-OrganizationRelationship -Identity "Contoso Cloud" -TargetOWAUrl http://cloudowa.contoso.com/owa
    ```

    Note

    - Use http, not https. If https is used, users may get a URL redirection issue [AADSTS50011].
    - The trailing value /owa is required in the organization relationship, but users don't need to enter /owa in the URL.
    - You can use the [Get-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/get-organizationrelationship) cmdlet to find the organization relationship name.

After you apply this setting, the users can continue using the current Outlook on the web URL to access their on-premises mailboxes. In the previous example, the value is https://mail.contoso.com/owa.

## Multiple authentication prompts

Users may receive multiple authentication prompts depending on:

- Where they connect from (internal or external Internet connections).
- If their computer is or isn't domain joined.
- If you're using identity federation in your hybrid environment.

The authentication prompt experience that users can expect is described in the following table.

| Authentication method | Client computer | Authentication prompt experience |
| --- | --- | --- |
| Identity federation | Internal Internet connection | Single prompt |
| Identity Federation | External Internet connection | Double prompt |
| No Identity federation | Domain joined (internal or external) | Double prompt |
| With or without identity federation | Not domain joined (internal or external) | Double prompt |

Note

Identity federation requires that the AD FS endpoint is configured in the Intranet Zone of Internet Explorer as described in [KB2535227](https://support.microsoft.com/help/2535227), and that AD FS is configured per the general Microsoft 365 or Office 365 guidance.