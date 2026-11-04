---
layout: Conceptual
title: Modify, disable, or remove a sharing policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/sharing-policies/modify-a-sharing-policy
Manager: dansimp
ms.subservice: sharing
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Sharing policies control how your users share their calendars with people outside your organization. You may want to change some sharing policy properties, such as changing sharing rules, changing the free/busy access level, temporarily disabling a sharing policy, or removing a sharing policy entirely.
ms.topic: article
author: navanethan-msft
ms.author: nagangat
ms.assetid: a494c4d2-9316-44ce-9a39-268398378f08
ms.reviewer: AkshayaPrakash-PM
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-02-28T00:00:00.0000000Z
locale: en-us
document_id: a8d16376-3fe5-cbf5-4bbd-8c729c7f4b30
document_version_independent_id: 017b0bab-28aa-7728-a29f-e72d17b54aa2
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/sharing-policies/modify-a-sharing-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/sharing-policies/modify-a-sharing-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/sharing-policies/modify-a-sharing-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: bd9659d2-be94-03e5-b51e-1b978f970949
---

# Modify, disable, or remove a sharing policy in Exchange Online | Microsoft Learn

Sharing policies control how your users share their calendars with people outside your organization. You may want to change some sharing policy properties, such as changing sharing rules, changing the free/busy access level, temporarily disabling a sharing policy, or removing a sharing policy entirely.

For details about how to create a sharing policy, see [Create a sharing policy in Exchange Online](create-a-sharing-policy)

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the [Permissions in Exchange Online](../../permissions-exo/permissions-exo) topic.

## Use the Exchange admin center to change a sharing policy

1. From the Microsoft 365 admin center dashboard, click **Exchange**.
2. Go to **Organization** &gt; **Individual sharing**.
3. Under **Individual Sharing**, select a sharing a policy, and click anywhere in the row other than the button option that appears in the blank area next to the Display name column.
4. In the **Sharing policy** flyout that opens, click **Manage domains**.
5. In the **Manage sharing rules** details pane, click Domains check box and click **Edit**![Edit icon.](../../exchangeonline/media/itpro_eac_editicon.gif) to change the settings such as the domain you want to share information with and specify information level for calendars. Click **Save** to update the rule.
6. In **Manage sharing rules**, click **Save** to update the sharing policy.

## Use the Exchange admin center to set a sharing policy as the default sharing policy

1. From the Microsoft 365 admin center dashboard, go to **Exchange**.
2. Go to **Organization** &gt; **Sharing**.
3. Under **Individual sharing**, select a sharing a policy, and click anywhere in the row other than the button option that appears in the blank area next to the Display name column.
4. In the **Sharing policy** details pane, click **Manage policy name** and select **Default Sharing Policy**.
5. Click **Save changes** to update the sharing policy.

## Use the Exchange admin center to disable a sharing policy

1. From the Microsoft 365 admin center dashboard, go to **Exchange**.
2. Go to **Organization** &gt; **Sharing**.
3. Under **Individual Sharing**, select a sharing a policy.
4. In the **Manage sharing rules**, clear the check box for the sharing policy you want to disable.

### Use the Exchange admin center to remove a sharing policy

Important

Before you remove a sharing policy, the sharing policy must be removed from all user mailboxes.

1. From the Microsoft 365 admin center dashboard, click **Exchange**.
2. Go to **Organization** &gt; **Sharing**.
3. Under **Individual Sharing**, select a sharing a policy, and then click **Delete**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.gif).
4. In the warning, click **Confirm** to delete the sharing policy.

## Use Exchange Online PowerShell to modify, disable or remove a sharing policy

- This example modifies the sharing policy Contoso. This policy allows users in the Contoso domain to see simple free/busy information.

    ```PowerShell
    Set-SharingPolicy -Identity Contoso -Domains 'sales.contoso.com: CalendarSharingFreeBusySimple'
    ```
- This example adds a second domain to the sharing policy Contoso. When you're adding a domain to an existing policy, you must include any previously included domains.

    ```PowerShell
    Set-SharingPolicy -Identity Contoso -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'atlanta.contoso.com: CalendarSharingFreeBusyReviewer', 'beijing.contoso.com: CalendarSharingFreeBusyReviewer'
    ```
- This example sets the sharing policy Contoso as the default sharing policy.

    ```PowerShell
    Set-SharingPolicy -Identity Contoso -Default $True
    ```
- This example disables the sharing policy Contoso.

    ```PowerShell
    Set-SharingPolicy -Identity "Contoso" -Enabled $False
    ```
- The first example removes the sharing policy Contoso. The second example removes the sharing policy Contoso and suppresses the confirmation that you want to remove the policy.

    ```PowerShell
    Remove-SharingPolicy -Identity Contoso
    ```

    ```PowerShell
    Remove-SharingPolicy -Identity Contoso -Confirm
    
    ```

For detailed syntax and parameter information, see [Set-SharingPolicy](/en-us/powershell/module/exchangepowershell/set-sharingpolicy) and [Remove-SharingPolicy](/en-us/powershell/module/exchangepowershell/remove-sharingpolicy).