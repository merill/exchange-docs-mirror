---
layout: Conceptual
title: Configure the external postmaster address in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/configure-external-postmaster-address
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
description: Admins can learn how to configure the external postmaster email address in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: ece00da0-743b-4e26-83f5-a2eb68c7de4e
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 71830733-a67d-6563-d5e4-12b86872c765
document_version_independent_id: 251fde83-4e81-e5ac-d032-b05b8a46cb9c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/configure-external-postmaster-address.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/configure-external-postmaster-address
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/configure-external-postmaster-address.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 3e3dde48-dc6b-765d-4b9d-36922790a041
---

# Configure the external postmaster address in Exchange Online | Microsoft Learn

The external postmaster address is used as the sender for system-generated messages and notifications sent to message senders that exist outside your Microsoft Exchange Online organization. An external sender is any sender that has an email address in a domain that isn't configured as an accepted domain in your organization.

By default, the value of the external postmaster address setting is blank. This default value sets the external postmaster address to the value postmaster@&lt;*Default accepted domain*&gt; for your organization.

There's no mailbox associated with the postmaster@&lt;*Default accepted domain*&gt; email address.

Tip

You can't configure an internal postmaster address in Exchange Online. The default internal postmaster address automatically uses @&lt;*Default accepted domain*&gt;.

## What do you need to know before you begin?

- Estimated time to complete: 15 minutes
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mail flow" entry in the [Feature permissions in Exchange Online](../permissions-exo/feature-permissions) topic.
- You can only use Exchange Online PowerShell to perform this procedure. To learn how to connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to configure the external postmaster address

To configure the external postmaster address, use the following syntax:

```powershell
Set-TransportConfig -ExternalPostmasterAddress <EmailAddress>
```

This example sets the external postmaster address to the value `postmaster@contoso.com`.

```powershell
Set-TransportConfig -ExternalPostmasterAddress postmaster@contoso.com
```

This example returns the external postmaster address to the default value.

```powershell
Set-TransportConfig -ExternalPostmasterAddress $null
```

## How do you know this worked?

To verify that you have successfully configured the external postmaster address, do the following:

1. Run the following command to verify the property value:

    ```powershell
    Get-TransportConfig | Format-List ExternalPostmasterAddress
    ```

    A blank value indicates the default value postmaster@&lt;*Default accepted domain*&gt;.
2. From an external email account, send a message to your Exchange organization that will generate a non-delivery report (also known as an NDR or bounce message). For example, you can configure a mail flow rule (also known as a transport rule) to send an NDR for a message from that sender that contains specific keywords. Verify that the sender's email address in the DSN matches the external postmaster address you specified.