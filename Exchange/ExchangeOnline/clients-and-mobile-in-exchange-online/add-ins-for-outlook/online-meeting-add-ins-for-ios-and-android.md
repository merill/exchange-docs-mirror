---
layout: Conceptual
title: Using third-party add-ins for online in Exchange Online meetings in Outlook for iOS and Android in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/online-meeting-add-ins-for-ios-and-android
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
description: 'Summary: This article describes how users of Outlook for iOS and Android can use third-party add-ins for online meetings'
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.custom: remotework
ms.reviewer: smithre4
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2020-04-16T00:00:00.0000000Z
locale: en-us
document_id: 90e6be4a-8597-5129-7b8f-de44d2026bae
document_version_independent_id: 5292ca3c-1c6f-09e2-5347-716bb46ee1b8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/add-ins-for-outlook/online-meeting-add-ins-for-ios-and-android.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/add-ins-for-outlook/online-meeting-add-ins-for-ios-and-android
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/add-ins-for-outlook/online-meeting-add-ins-for-ios-and-android.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: dccc35af-62cb-c3cf-1234-79c175fd892b
---

# Using third-party add-ins for online in Exchange Online meetings in Outlook for iOS and Android in Exchange Online | Microsoft Learn

Setting up an online meeting is a core experience for Outlook users. To meet the needs of an increasing number of remote workers and students, Outlook for iOS and Android has enabled add-ins to provide online meetings from third-party providers such as Zoom, BlueJeans, and Webex (among others). End-users in your organization will be able to use these add-ins to set up online meetings on third-party platforms.

Note

Both Outlook for iOS and Android support joining meetings from third-party online meeting providers. In addition, Outlook for Android also supports creating meeting requests for third-party online meeting providers.

## How to enable third-party online meeting integration with Outlook for iOS and Android

Third-party online meeting integration is handled by add-ins that have enabled this functionality specifically for Outlook for iOS and Android. To set up this third-party meeting creation experience, an Exchange Online administrator must install the supported add-in(s) to the mailbox of an end user. Once installed, the third-party meeting creation button will appear on users' screens instead of a Microsoft Teams or Skype meeting button.

Note

Add-ins installed by your end users will **not** override the default Teams or Skype functionality.

The add-ins can be deployed using the following admin portals:

- If all users are Microsoft 365 or Office 365 users, then use the [centralized deployment portal](/en-us/office/dev/add-ins/publish/centralized-deployment). Centralized deployment provides the capability to install add-ins more granularly, such as to sub-groups within a given organization.
- If a tenant has users' mailboxes in on-premises Exchange Server, then use the ECP/EAC portal. More information is available [here](../../install-or-remove-outlook-add-ins-2013-help).

## Creating an online meeting with a third-party add-in

The third-party online meeting provider will appear on the event creation screen in Outlook for iOS and Android, as displayed below. The third-party add-in replaces the Teams or the Skype buttons, but the button users do see will act in a similar way. After tapping the toggle button, the online meeting URL and text is retrieved from the third-party service and is inserted into the meeting body.

Users cannot save the meeting until the online meeting details have been retrieved.

![creating a meeting with a third-party add-in on Outlook for Android.](../../exchangeonline/media/android-meeting-creation.png)

## Meeting providers displayed in the New Event screen

On a user's New Event screen, only a single meeting provider will be shown. If there are multiple options, the logic to select which provider is displayed is as follows:

- Priority 1: Any custom online meeting add-ins that are installed (this is a developer scenario also known as "side loading").
- Priority 2: An online meeting add-in that was installed by an administrator.
- Default selection: If there are no admin-installed online Web conferencing add-ins, the default option of Teams and Skype will be shown, as described [in this article](/en-us/microsoftteams/setting-your-coexistence-and-upgrade-settings).

Note

Installing multiple add-in providers for online meetings on a user's device isn't supported and may result in unexpected behavior.

## Developing add-ins for remote meetings in Outlook for iOS and Android

Add-in developers need to add the MobileOnlineMeetingCommandSurface extension point in their add-in manifest.

Information for add-in developers is available in [Create an Outlook mobile add-in for an online-meeting provider](/en-us/office/dev/add-ins/outlook/online-meeting).

Capabilities exposed to online meeting add-ins include:

- UI-less command. Online meeting add-ins can only run in a UI-less mode, which means the add-ins don't have the capability to launch a task pane.
- Display dialogue. Login flow can be handled using full-screen dialog.
- The specific APIs that are exposed are [listed here](/en-us/office/dev/add-ins/outlook/online-meeting#available-apis).

## How users join meetings

Support for third-party remote meeting add-ins includes making it easy for users to join meetings. A **Join** button gets added to users' calendar events in Outlook for iOS and Android. Clicking **Join** will launch the online meeting app, if the user has it installed. If the app is not installed, the browser will launch and guide the user through the process to join the meeting.

Note that recipients of meeting invitations don't need to have the add-in for the corresponding third-party meeting provider installed on their devices in order to join the meeting.

![Joining a meeting with a third-party meeting provider in Outlook for Android.](../../exchangeonline/media/android-join.png)