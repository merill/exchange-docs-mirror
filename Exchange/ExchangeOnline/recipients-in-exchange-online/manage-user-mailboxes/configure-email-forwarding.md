---
layout: Conceptual
title: Configure email forwarding for a mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding
Manager: serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Email forwarding lets you set up a mailbox to forward email messages sent to that mailbox to another user's mailbox in or outside of your organization.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: c7a7afaf-577e-49d6-8cee-bb4c4a5d570b
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-30T00:00:00.0000000Z
locale: en-us
document_id: 0712dfaf-5113-e50d-19b9-c79ca780e22f
document_version_independent_id: 5482a4ff-b479-69a9-2abe-c7fe253f9fee
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 4db7dda1-887f-b777-6ead-cbe2f3d669fa
---

# Configure email forwarding for a mailbox in Exchange Online | Microsoft Learn

Email forwarding lets you forward emails sent to a mailbox to another user's mailbox or to an external address.

Tip

You can also use the Microsoft 365 admin center to manage mail forwarding. For more information, see [Configure email forwarding](/en-us/microsoft-365/admin/email/configure-email-forwarding).

Important

Automatic email forwarding to external recipients makes your organization vulnerable to takeover attacks. If you choose to do it anyway, you can create an anti-spam outbound policy that allows it only for users who need it. For more information, see [Control automatic external email forwarding in Microsoft 365](/en-us/defender-office-365/outbound-spam-policies-external-email-forwarding).

## Use the Exchange admin center (EAC) to configure email forwarding

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.

1. In the EAC, go to **Recipients** &gt; **Mailboxes**.
2. In the list of user mailboxes, click the mailbox that you want to configure mail forwarding for. A display pane is shown for the selected user mailbox.
3. Under **Mailbox** &gt; **Email forwarding**, click the **Manage email forwarding** link.
4. The **Manage email forwarding** display pane is shown. By default the **Forward all emails sent to this mailbox** setting is OFF. Turn it ON.
5. Under **Forwarding address** text box, select the **Search email** button to find and choose an internal recipient to forward messages to. If you want to forward to an external address, then select **Forward to an external email address** and type in the external address.
6. You can select the **Deliver message to both forwarding address and mailbox** option if you wish to keep a copy of the forwarded email.
7. Click **Save** to save your changes. Click **Close** to exit from the **Manage email forwarding** display pane.