---
layout: Conceptual
title: Add-ins for Outlook in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/add-ins-for-outlook
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
description: Admins can learn about add-ins for Outlook in Exchange Online.
ms.topic: overview
author: AshaIyengar21
ms.author: serdars
ms.assetid: 28b6f2a1-a235-4023-b561-6fd304962775
ms.reviewer: 
ms.collection: exchange-online
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: b208cbdc-d46e-af0f-3d99-b1627277d3f0
document_version_independent_id: 4e43510d-946b-83cc-da53-a6416145f7a5
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/add-ins-for-outlook/add-ins-for-outlook.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/add-ins-for-outlook/add-ins-for-outlook
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/add-ins-for-outlook/add-ins-for-outlook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: e222beed-665b-cd8d-9f3b-f22a058b1490
---

# Add-ins for Outlook in Exchange Online | Microsoft Learn

Add-ins for Outlook are applications that extend the usefulness of Outlook clients by adding information or tools that your users can use without having to leave Outlook. Add-ins are built by third-party developers and can be installed either from a file or URL or from the Office Store. By default, all users can install add-ins. Exchange Online admins can control whether users can install add-ins for Office.

Tip

For information about add-ins for Outlook from an end-user perspective, check out [Installed add-ins](https://support.microsoft.com/office/a61762b7-7a82-47bd-b14e-bbc15eaeb70f). The topic provides an overview of the add-ins and also shows you some of the add-ins for Outlook that might be installed by default.

Note

The UI support for managing add-ins for Outlook in EAC will be discontinued. However, you can still install them using the Powershell cmdlets mentioned here.

## Office Store add-ins and custom add-ins

Outlook clients supports a variety of add-ins that are available through the Office Store. Outlook also supports custom add-ins that you can create and distribute to users in your organization.

**Notes**:

- Access to the Office Store isn't supported for mailboxes or organizations in specific regions. For more information, contact your service provider.
- URLs with redirections aren't supported in Exchange Server 2016, Exchange Server 2019, and Exchange Online. Use a direct URL to the manifest.
- Some add-ins for Outlook are installed by default. Default add-ins for Outlook only activate on English language content. For example, German postal addresses in the message body won't activate the Bing Maps add-in.

## Add-in access and installation using UI

By default, all users can install and remove add-ins. Exchange Online admins have a number of controls available for managing add-ins and users' access to them. Admins can disable users from installing add-ins that aren't downloaded from the Office Store (instead they are "side loaded" from a file or URL). Admins can also disable users from installing Office Store add-ins, and from installing add-ins on behalf of other users.

To install add-ins for some or all users in your organization, see [Get started with Integrated apps](/en-us/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

## Install add-ins for Outlook using cmdlets

You can manage Outlook add-ins using PowerShell cmdlets as a replacement for *Add-ins* page experience in classic Exchange Admin Center.

The following cmdlets are a part of [ExchangePowerShell](/en-us/powershell/module/exchangepowershell/?view=exchange-ps&amp;preserve-view=true) module and are available in on-premise Exchange and in the cloud-based service. Some parameters and settings might be exclusive to one environment or the other, and details for the same can be found in respective documentation for each section.

### Deploying a new app

Use the `New-App` cmdlet to install apps for Outlook.

For more information, see [New-App (ExchangePowerShell) | Microsoft Learn](/en-us/powershell/module/exchangepowershell/new-app?view=exchange-ps&amp;preserve-view=true).

### Removing a deployed app

Use the `Remove-App` cmdlet to uninstall an app. You can use `Remove-App` cmdlet to uninstall a specified app that has been installed using only `New-App` cmdlet. Apps installed by default can't be uninstalled, but can be disabled.

For more information, see [Remove-App (ExchangePowerShell) | Microsoft Learn](/en-us/powershell/module/exchangepowershell/remove-app?view=exchange-ps&amp;preserve-view=true).

### Getting list of deployed apps

Use the `Get-App` cmdlet to view installed apps. The `Get-App` cmdlet returns information about all installed apps or the details of a specific installed app.

For more information, see [Get-App (ExchangePowerShell) | Microsoft Learn](/en-us/powershell/module/exchangepowershell/get-app?view=exchange-ps&amp;preserve-view=true).

### Updating an app

Use the `Set-App` cmdlet to modify the availability of organization apps. The `Set-App` cmdlet can only be used when configuring the availability of an organization app. This task requires that the specified app has either been installed using `New-App` cmdlet or is a default app for Outlook.

Default apps in Outlook on the web and apps that you've installed for use by users in your organization are known as organization apps. End users cannot remove organization apps, but can enable or disable them. If an app is an organization app (scope - default or organization), the delete control on the toolbar is disabled for end users. Administrators can remove organization apps. They can't remove default apps but can disable them for the entire organization.

For more information, see [Set-App (ExchangePowerShell) | Microsoft Learn](/en-us/powershell/module/exchangepowershell/set-app?view=exchange-ps&amp;preserve-view=true).

### Enabling an app

Use the `Enable-App` cmdlet to enable (turn on) a specific app for a specific user. The `Enable-App` cmdlet requires that the specified app has already been installed (for example, that it has been installed with the `New-App` cmdlet, or that it's a default app for Microsoft Outlook).

For more information, see [Enable-App (ExchangePowerShell) | Microsoft Learn](/en-us/powershell/module/exchangepowershell/enable-app?view=exchange-ps&amp;preserve-view=true).

### Disabling an app

Use the `Disable-App` cmdlet to disable (turn off) a specific app for a specific user. The `Disable-App` cmdlet requires that the specified app is an app that has either been installed using `New-app` cmdlet or is a default app for Microsoft Outlook.

For more information, see [Disable-App (ExchangePowerShell) | Microsoft Learn](/en-us/powershell/module/exchangepowershell/disable-app?view=exchange-ps&amp;preserve-view=true).