---
layout: Conceptual
title: Create a sharing policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/sharing-policies/create-a-sharing-policy
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
ms.custom:
- has-azure-ad-ps-ref
description: Create a new Sharing Policy to change how people in your organization share calendars with individual business associates, friends, or family members. Sharing policies control how your users share their calendars with people outside your organization. By default, all users can invite anyone with an email address to view their calendar. After you create a new sharing policy, you have to apply that policy to mailboxes before it takes effect. To apply a specific sharing policy to users, see Apply a sharing policy to mailboxes in Exchange Online.
ms.topic: how-to
author: navanethan-msft
ms.author: nagangat
ms.assetid: f412ce6c-74dc-4d77-93ab-362c37414015
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
document_id: f8a1307f-4fc4-4b9c-a4fb-08e536a916d1
document_version_independent_id: f37be797-3801-cf2b-24d7-5c0814455329
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/sharing-policies/create-a-sharing-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/sharing-policies/create-a-sharing-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/sharing-policies/create-a-sharing-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 00655b91-e419-46bf-b091-c80283c48a2a
---

# Create a sharing policy in Exchange Online | Microsoft Learn

Create a new Sharing Policy to change how people in your organization share calendars with individual business associates, friends, or family members. Sharing policies control how your users share their calendars with people outside your organization. By default, all users can invite anyone with an email address to view their calendar. After you create a new sharing policy, you have to apply that policy to mailboxes before it takes effect. To apply a specific sharing policy to users, see [Apply a sharing policy to mailboxes in Exchange Online](apply-a-sharing-policy).

## What do you need to know before you begin?

- Estimated time to complete: 15 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the [Permissions in Exchange Online](../../permissions-exo/permissions-exo) topic.
- Only Outlook 2010 or later and Outlook on the web (formerly known as Outlook Web App) users can create sharing invitations.

## Use the Exchange admin center to create a sharing policy

1. From the Microsoft 365 admin center dashboard, click **Exchange**.
2. Click **Organization** &gt; **Sharing**.
3. In the list view, under **Individual sharing**, click **Add individual sharing policy**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif).
4. In the **New individual sharing policy**, type a friendly name for the sharing policy in the **Policy name** box and click **Next**.
5. In the **Add sharing rule**, click **Specify domain & share information**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif) to define the sharing rules for the policy.
6. Select one of the following options to specify the domains you want to share with:

    - **Sharing with all domains**
    - **Sharing with a specific domain**
7. If you select **Sharing with a specific domain**, type the name of the domain you want to share with. If you need to enter more than one domain for this sharing policy, save the settings for the first domain, then edit the sharing rules to add more domains.
8. To specify the information that can be shared, click **Share your calendar folder** check box, and then select one of the following options:

    - **Calendar free/busy information with time only**
    - **Calendar free/busy information with time, subject, and location**
    - **All calendar appointment information, including time, subject, location and title**
9. Click the **Share your contact folder** to share your contacts.
10. In the **Review and finish** click **Next** to create the sharing policy.

## Use Exchange Online PowerShell to create a sharing policy

- This example creates the sharing policy Contoso. This policy allows users in the contoso.com domain to see your user's detailed calendar availability (free/busy) information. By default, this policy is enabled.

    ```PowerShell
    New-SharingPolicy -Name "Contoso" -Domains 'contoso.com: CalendarSharingFreeBusyDetail'
    ```
- This example creates the sharing policy ContosoWoodgrove for two different domains (contoso.com and woodgrovebank.com) with different sharing settings configured for each domain. The policy is disabled.

    ```PowerShell
    New-SharingPolicy -Name "ContosoWoodgrove" -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'woodgrovebank.com: CalendarSharingFreeBusyDetail' -Enabled $false
    ```

For detailed syntax and parameter information, see [New-SharingPolicy](/en-us/powershell/module/exchangepowershell/new-sharingpolicy).

## How do you know this worked?

To verify that you have successfully created the sharing policy, run the following command to view the sharing policy information.

```PowerShell
Get-SharingPolicy <policy name> | format-list
```