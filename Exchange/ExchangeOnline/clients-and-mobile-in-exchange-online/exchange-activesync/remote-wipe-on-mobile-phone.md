---
layout: Conceptual
title: Perform a remote wipe on a mobile phone in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/exchange-activesync/remote-wipe-on-mobile-phone
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
description: Admins can learn how to remote wipe a mobile phone in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2022-05-09T00:00:00.0000000Z
locale: en-us
document_id: faae0635-50c9-0b0d-819f-dd49df2fb48f
document_version_independent_id: a70499cc-e8b0-c661-0667-ec913ca594ce
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/exchange-activesync/remote-wipe-on-mobile-phone.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/exchange-activesync/remote-wipe-on-mobile-phone
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/exchange-activesync/remote-wipe-on-mobile-phone.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 617a1d24-c2e9-8952-8cfa-5166ac8c5e58
---

# Perform a remote wipe on a mobile phone in Exchange Online | Microsoft Learn

Your users carry sensitive corporate information in their pockets every day. If one of them loses their mobile phone, your data can end up in the hands of another person. If one of your users loses their mobile phone, you can use the Exchange admin center (EAC) or Exchange Online PowerShell to wipe their phone clean of all corporate and user information.

Note

This topic also provides instructions for how to use Outlook on the web (formerly known as Outlook Web App) to perform a remote wipe on a phone. The user must be signed in to Outlook on the web to perform a remote wipe.

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mobile devices" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Note

Prior to EAS v16.1, remote wipe would perform a device-level wipe, restoring the device to factory conditions. With EAS v16.1 and later, EAS also supports account-only remote wipe. In order for this to work, the client must support the EAS v16.1 protocol. If the client doesn't support v16.1, the wipe will fail and an error will be given.

Caution

Exchange ActiveSync v16.1 supports two different remote wipe processes: A **Wipe Data** remote wipe and also an **Account Only Remote Wipe Device** remote wipe. There are important differences between how Outlook responds and how native mail apps on iOS and Android respond to these different wipe commands.

Outlook for iOS and Outlook for Android support only the **Wipe Data** command, which wipes only data within Outlook. The Outlook app will reset and all Outlook email, calendar, contacts, and file data will be removed, but no other data is wiped from the device. The **Account Only Remote Wipe Device** command is therefore redundant and is not supported by Outlook for iOS or Android.

However, if a native iOS or Android mail app is connected to Exchange and receives a **Wipe Data** command from Exchange ActiveSync, all data on the device will be wiped, including photos, personal files, and so on.

If a native iOS or Android mail app is connected to Exchange and receives an **Account Only Remote Wipe Device** command from Exchange ActiveSync, only the native mail app's Exchange ActiveSync mail, calendar, and account data are wiped.

These commands are designed to destroy data. Exercise caution when using them.

After the remote wipe command is requested by the administrator, the wipe happens within seconds of the Outlook app's next connection to Exchange.

Since Outlook for iOS and Android appears as a single mobile device association under a user's mobile devices in Exchange, a remote wipe command will remove data and delete sync relationships from all devices running Outlook (iPhone, iPad, Android) associated with that user.

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use the classic EAC to wipe a user's phone

Note

The classic EAC will be fully deprecated by September 2022. For more information, see [Deprecation of the classic Exchange admin center in WW service](https://techcommunity.microsoft.com/t5/exchange-team-blog/deprecation-of-the-classic-exchange-admin-center-in-ww-service/ba-p/2736358).

You can use the classic EAC to wipe a user's phone or cancel a remote wipe that has not yet completed.

1. In the EAC, navigate to **Recipients** &gt; **Mailboxes**.
2. Select the user, and under **Mobile Devices**, choose **View details**.
3. On the **Mobile Device Details** page, select the lost mobile device, and then select **Wipe Data** (or **Account Only Remote Wipe Device** if desired).
4. Select **Save**.

## Use Exchange Online PowerShell to wipe a user's phone

You can use the **Clear-MobileDevice** cmdlet in Exchange Online PowerShell to wipe a user's phone.

The following command wipes the device named WM\_TonySmith and sends a confirmation message to admin@contoso.com.

```PowerShell
Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"
```

If the device connects to Exchange using a mail app other than Outlook, you can use the following command to wipe only the mail app's Exchange ActiveSync mail, calendar, and account data and leave all other data on the device intact:

```PowerShell
Clear-MobileDevice -AccountOnly -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"
```

The **-AccountOnly** switch has no effect on Outlook devices because an account-only remote wipe is the only type of wipe that is supported by Outlook. See [Clear-MobileDevice](/en-us/powershell/module/exchangepowershell/clear-mobiledevice) for more information.

## Use Outlook on the web to wipe a user's phone

1. In Outlook on the web, select the **Settings** icon.
2. Click on **View All Outlook settings**.
3. Click **General**, and then select **Mobile devices**.
4. Select the mobile phone.
5. Click or tap the **Wipe Device** icon (or the **Account Only Remote Wipe Device** icon if desired).

## How do you know this worked?

There are several ways to verify that the remote wipe completed.

- Run the **Clear-MobileDevice** cmdlet with the *-NotificationEmailAddresses* parameter configured. A message will be sent to the supplied email address when the remote wipe has completed.
- In the EAC, check the status of the mobile device. The status will change from **Wipe Pending** to **Wipe Successful**.
- In Outlook on the web, check the status of the mobile device. The status will change from **Wipe Pending** to **Wipe Successful**.