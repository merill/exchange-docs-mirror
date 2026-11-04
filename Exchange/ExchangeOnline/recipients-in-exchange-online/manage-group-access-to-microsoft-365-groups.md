---
layout: Conceptual
title: Manage guest access to Microsoft 365 groups in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-group-access-to-microsoft-365-groups
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn how to allow or block guest access to Microsoft 365 Groups.
ms.topic: how-to
ms.author: serdars
author: AshaIyengar21
ms.assetid: a86bb46f-0e5b-43a3-b6ef-7394f344a8da
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2020-06-22T00:00:00.0000000Z
locale: en-us
document_id: 28bc43ec-5fbf-f8a1-19c6-06ec377e452e
document_version_independent_id: 88ed9745-0bc0-08d5-2481-f5e166a6b8ea
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-group-access-to-microsoft-365-groups.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-group-access-to-microsoft-365-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-group-access-to-microsoft-365-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 6befc65b-7eea-86a1-7247-bf1ca908bb33
---

# Manage guest access to Microsoft 365 groups in Exchange Online | Microsoft Learn

You can allow or block guest users who are using a specific domain. For example, let's say your business (Contoso) has a partnership with another business (Fabrikam). You can add Fabrikam to your allowlist so your users can add those guests to their groups.

Or, let's say you want to block personal email address domains. You can set up a blocklist that contains domains like Gmail.com and Outlook.com.

## Important information about how blocklists work

- You can create either an allowlist or blocklist. **But you can't set up both types of lists**. By default, whatever domains aren't in an allowlist are on a blocklist, and vice versa.
- You can create only one policy per organization. You can update that policy with more domains, or you can delete that policy to create a new one.
- This list works independently from SPO allow/block list. You would need to set up Allow/Block list for SPO if you want to restrict individual file sharing of Group connected site.
- This list doesn't apply to already added guest members. This will be enforced for all the guests added after the list is set up.

## Install the preview version of the Azure Active Directory module for Windows PowerShell

**IMPORTANT**: The procedures in this article require the **PREVIEW** version Azure Active Directory module for Windows PowerShell, specifically, the **AzureADPreview** module version **2.0.0.98** or later.

1. Open Windows PowerShell as an administrator:

    1. In your search bar, type Windows PowerShell.
    2. Right-click on Windows PowerShell and select **Run as Administrator**.

    The Windows PowerShell window will pop open. The prompt C:\Windows\system32 means you opened it as an administrator.
2. Run this command to see if you have any versions of the Azure Active Directory module for Windows PowerShell installed on your computer:

    ```PowerShell
    Get-Module -ListAvailable AzureAD*
    ```

    - If no results are returned, run this command to install the latest version of the **AzureADPreview** module:

        ```PowerShell
        Install-Module AzureADPreview
        ```
    - If *only* the **AzureAD** module is shown in the results, run these commands to install the **AzureADPreview** module:

        ```PowerShell
        Uninstall-Module AzureAD
        ```

        ```PowerShell
        Install-Module AzureADPreview
        ```
    - If *only* the **AzureADPreview** module is shown in the results, but the version is less than **2.0.0.98**, run these commands to update it:

        ```PowerShell
        Uninstall-Module AzureADPreview
        ```

        ```PowerShell
        Install-Module AzureADPreview
        ```
    - If both the **AzureAD***and***AzureADPreview** modules are shown in the results, but the version of the **AzureADPreview** module is less than **2.0.0.98**, run these commands to update it:

        ```PowerShell
        Uninstall-Module AzureAD
        ```

        ```PowerShell
        Uninstall-Module AzureADPreview
        ```

        ```PowerShell
        Install-Module AzureADPreview
        ```

## Create a new Allow or blocklist policy

1. Did you install the **AzureADPreview** module as instructed above? Not having the **preview** version is the #1 reason these steps don't work for people.
2. Go to [Script for Allow/Block policy](https://www.microsoft.com/download/details.aspx?id=55709) at Microsoft Download Center to download the script ( **Set-GuestAllowBlockDomainPolicy.ps1**) for Allow/Block policy.
3. Run the script with this command:

    ```PowerShell
    Set-GuestAllowBlockDomainPolicy.ps1 -Update -AllowList @("contoso.com", "fabrikam.com")
    ```

    Where you replace **contoso.com** and **fabrikam.com** with the domains you want to allow.

    OR

    ```PowerShell
    Set-GuestAllowBlockDomainPolicy.ps1 -Update -BlockList @("contoso.com", "fabrikam.com")
    ```

    Remember, you can create only one policy. You'll get an error if you try to create another one.

## Replace the existing policy with a new list of domains

To replace the existing policy with new list of domains, run this command:

```PowerShell
Set-GuestAllowBlockDomainPolicy.ps1 -Update -AllowList @("contoso.com", "fabrikam.com")
```

Where you replace **contoso.com** and **fabrikam.com** with the domains you want to allow.

OR

```PowerShell
Set-GuestAllowBlockDomainPolicy.ps1 -Update -BlockList @("contoso.com", "fabrikam.com")
```

## Add more domains to an existing policy

To append a new domain to your policy, run this command:

```PowerShell
Set-GuestAllowBlockDomainPolicy.ps1 -Append -AllowList @("contoso.com")
```

Where you replace **contoso.com** and **fabrikam.com** with the domains you want to allow.

OR

```PowerShell
Set-GuestAllowBlockDomainPolicy.ps1 -Append -BlockList @("contoso.com")
```

## Migrate the existing allow/block policy from SharePoint Online

This list works independently from the SharePoint Online allow/block list. You would need to set up allow/block list for SharePoint Online if you want to restrict individual file sharing of Group connected site.

However, if your organization already has an allow/block list for SharePoint Online, you can migrate that list using this command.

1. Install the [SharePoint Online Management tool](https://www.microsoft.com/download/details.aspx?id=35588).
2. Run this command:

    ```PowerShell
    Set-GuestAllowBlockDomainPolicy.ps1 -MigrateFromSharepoint
    ```

## Clear the domain list

To remove all the domains from your policy, run this command:

```PowerShell
Set-GuestAllowBlockDomainPolicy.ps1 -Remove
```

## Script for Allow/Block policy

Go to [Script for Allow/Block policy](https://www.microsoft.com/download/details.aspx?id=55709) at Microsoft Download Center to download the script (**Set-GuestAllowBlockDomainPolicy.ps1**) for Allow/Block policy.