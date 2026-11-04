---
layout: Conceptual
title: Remove an Outlook on the web mailbox policy from Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/remove-outlook-web-app-mailbox-policy
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
description: Admins can learn how to remove an Outlook on the web mailbox policy from an Exchange Online organization by using either the EAC or Exchange Online PowerShell.
ms.topic: how-to
author: Swatyario
ms.author: adbhale
ms.assetid: edab7bac-b62c-4b82-8f21-dcac77cf0e8f
ms.reviewer: chrisda
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2023-11-17T00:00:00.0000000Z
locale: en-us
document_id: 23e0e3f4-7c0e-6661-e12b-30c55e6ab983
document_version_independent_id: 03d72745-d540-b084-d350-ae4d577f4944
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/remove-outlook-web-app-mailbox-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-on-the-web/remove-outlook-web-app-mailbox-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/remove-outlook-web-app-mailbox-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: 6e6726b1-e10f-638d-8ff3-accf826dc1b8
---

# Remove an Outlook on the web mailbox policy from Exchange Online | Microsoft Learn

You can remove a mailbox policy from Outlook on the web (formerly known as an Outlook Web App mailbox policy) and the new Outlook for Windows using either the Exchange admin center (EAC) or Exchange Online PowerShell.

Note

Don't remove the built-in mailbox policy named "OwaMailboxPolicy-Default".

For information on additional management tasks related to Outlook on the web mailbox policies, see [Outlook on the web mailbox policies](outlook-web-app-mailbox-policies).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 3 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. For information on the permissions you need, see the "Outlook on the web mailbox policies" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- For information on how to open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center). For information on how to connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to remove a mailbox policy for Outlook on the web and the new Outlook for Windows

1. In the EAC, go to **Roles** &gt; **Outlook Web App policies**, select the policy that you want to remove, and then select **Delete**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.png).
2. In the confirmation window that appears, select **Confirm** to remove the mailbox policy. Or, select **Close X** to cancel.

## Use Exchange Online PowerShell to remove a mailbox policy for Outlook on the web and the new Outlook for Windows

To remove a mailbox policy for Outlook on the web and the new Outlook for Windows, use the following syntax:

```PowerShell
Remove-OwaMailboxPolicy -Identity "<Policy Name>"
```

This example removes the mailbox policy named "Sales Associates" from Outlook on the web and the new Outlook for Windows.

```PowerShell
Remove-OwaMailboxPolicy -Identity "Sales Associates"
```

For detailed syntax and parameter information, see [Remove-OwaMailboxPolicy](/en-us/powershell/module/exchangepowershell/remove-owamailboxpolicy).

## How do you know this worked?

To verify that you've successfully removed an Outlook on the web mailbox policy, perform any of the following steps:

- In the EAC, go to **Roles** &gt; **Outlook Web App policies** and verify the policy is no longer listed.
- In Exchange Online PowerShell, run the following command to verify the policy is no longer listed:

    ```PowerShell
    Get-OwaMailboxPolicy
    ```