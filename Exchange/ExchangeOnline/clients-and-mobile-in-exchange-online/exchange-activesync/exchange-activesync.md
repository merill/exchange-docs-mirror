---
layout: Conceptual
title: Exchange ActiveSync in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/exchange-activesync/exchange-activesync
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
description: Exchange ActiveSync is a client protocol that lets you synchronize a mobile device with your mailbox.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: ff7f0d3d-1b9d-4c49-b7fe-1ab5d2805b00
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: a2c70b4b-ef89-5bec-5b99-f573b29c037a
document_version_independent_id: fd9d3d74-26ec-77db-82a3-913c7a021919
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/exchange-activesync/exchange-activesync.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/exchange-activesync/exchange-activesync
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/exchange-activesync/exchange-activesync.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/390894b2-8646-4f7e-b8cd-2209156272a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/12b23b77-ab37-4318-a036-4f6690586386
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 722ab0ab-21d4-55e7-2a13-063f986f2fd4
---

# Exchange ActiveSync in Exchange Online | Microsoft Learn

Exchange ActiveSync is a client protocol that lets you synchronize a mobile device with your mailbox.

## Overview of Exchange ActiveSync

Exchange ActiveSync is a Microsoft Exchange synchronization protocol that's optimized to work together with high-latency and low-bandwidth networks. The protocol, based on HTTP and XML, lets mobile phones access an organization's information on a server that's running Microsoft Exchange. Exchange ActiveSync enables mobile phone users to access their email, calendar, contacts, and tasks, and to continue to access this information while they're working offline.

## Features in Exchange ActiveSync

Exchange ActiveSync provides the following:

- Support for HTML messages
- Support for follow-up flags
- Conversation grouping of email messages
- Ability to synchronize or not synchronize an entire conversation
- Support for viewing message reply status
- Support for fast message retrieval
- Meeting attendee information
- Enhanced Exchange Search
- PIN reset
- Enhanced device security through password policies
- Autodiscover for over-the-air provisioning
- Support for setting automatic replies when users are away, on vacation, or out of the office
- Support for task synchronization
- Direct Push
- Support for availability information for contacts

## Managing Exchange ActiveSync

By default, Exchange ActiveSync is enabled. All users who have an Exchange mailbox can synchronize their mobile device with the Microsoft Exchange server.

You can perform the following Exchange ActiveSync tasks:

- Enable and disable Exchange ActiveSync for users
- Set policies such as minimum password length, device locking, and maximum failed password attempts
- Initiate a remote wipe to clear all data from a lost or stolen mobile phone
- Run a variety of reports for viewing or exporting into a variety of formats
- Control which types of mobile devices can synchronize with your organization through device access rules

### Managing mobile device access in Exchange ActiveSync

You can control which mobile devices can synchronize. You do this by monitoring new mobile devices as they connect to your organization or by setting up rules that determine which types of mobile devices are allowed to connect. Regardless of the method you choose to specify which mobile devices can synchronize, you can approve or deny access for any specific mobile device for a specific user at any time.

### Device security features in Exchange ActiveSync

In addition to the ability to configure security options for communications between the Exchange server and your mobile devices, Exchange ActiveSync offers the following features to enhance the security of mobile devices:

- **Remote wipe**: If a mobile device is lost, stolen, or otherwise compromised, you can issue a remote wipe command from the Exchange Server computer or from any web browser by using Outlook on the web (formerly known as Outlook Web App). This command erases all data from the mobile device.
- **Device password policies**: Exchange ActiveSync lets you configure several options for device passwords. These options include the following:

    - **Minimum password length (characters)**: This option specifies the length of the password for the mobile device. The default length is 4 characters, but as many as 18 can be included.
    - **Minimum number of character sets**: Use this text box to specify the complexity of the alphanumeric password and force users to use a number of different sets of characters from among the following: lowercase letters, uppercase letters, symbols, and numbers.
    - **Require alphanumeric password**: This option determines password strength. You can enforce the usage of a character or symbol in the password in addition to numbers.
    - **Inactivity time (seconds)**: This option determines how long the mobile device must be inactive before the user is prompted for a password to unlock the mobile device.
    - **Enforce password history**: Select this check box to force the mobile phone to prevent the user from reusing their previous passwords. The number that you set determines the number of past passwords that the user won't be allowed to reuse.
    - **Enable password recovery**: Select this check box to enable password recovery for the mobile device. Users can use Outlook on the web to look up their recovery password and unlock their mobile device. Administrators can use the Exchange admin center to look up a user's recovery password.
    - **Wipe device after failed (attempts)**: This option lets you specify whether you want the phone's memory to be wiped after multiple failed password attempts.
- **Device encryption policies**: There are a number of mobile device encryption policies that you can enforce for a group of users. These policies include the following:

    - **Require encryption on device**: Select this check box to require encryption on the mobile device. This increases security by encrypting all information on the mobile device.
    - **Require encryption on storage cards**: Select this check box to require encryption on the mobile device's removable storage card. This increases security by encrypting all information on the storage cards for the mobile device.

Important

Although the Exchange ActiveSync protocol provides support for the different features listed above, it is up to the mobile device operating system and manufacturers (OEMs) to build support for these features in their mobile operating system and email apps (default or third-party). Not all EAS features listed above are supported by third-party mobile devices such as iOS and Android. Microsoft has no control over which EAS features are supported by these third-party mobile device manufacturers. Contact the manufactures directly for help with EAS features on third-party mobile devices.