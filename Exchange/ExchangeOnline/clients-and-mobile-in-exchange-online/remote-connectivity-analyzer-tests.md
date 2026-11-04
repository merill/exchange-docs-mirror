---
layout: Conceptual
title: Remote Connectivity Analyzer tests for Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/remote-connectivity-analyzer-tests
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
description: The Microsoft Exchange Remote Connectivity Analyzer (ExRCA) helps you make sure that connectivity for your Exchange servers is set up correctly. If you're having problems, it can also help you find and fix these problems. The ExRCA website can run tests to check for Microsoft Exchange ActiveSync, Exchange Web Services, Microsoft Outlook, and internet email connectivity.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 251505e6-0907-44cd-859f-bd9402e6a397
ms.reviewer: 
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 21b5e59e-b1df-376c-22f3-fedf3a1e2fe9
document_version_independent_id: 459dc342-6e86-2a47-3552-bfafdf968710
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/remote-connectivity-analyzer-tests.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/remote-connectivity-analyzer-tests
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/remote-connectivity-analyzer-tests.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/390894b2-8646-4f7e-b8cd-2209156272a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/12b23b77-ab37-4318-a036-4f6690586386
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: bd90101f-37a6-5d6f-cc8c-74607ea240ff
---

# Remote Connectivity Analyzer tests for Exchange Online | Microsoft Learn

The [Microsoft Exchange Remote Connectivity Analyzer (ExRCA)](https://testconnectivity.microsoft.com/) helps you make sure that connectivity for your Exchange service is set up correctly. If you're having problems, it can also help you find and fix these problems. The ExRCA website can run tests to check for Microsoft Exchange ActiveSync, Exchange Web Services, Microsoft Outlook, and internet email connectivity.

## Remote Connectivity Analyzer tests

You can perform several tests with the ExRCA. The following tests work on Exchange 2010 and later versions, including Exchange Online:

- Exchange DNS (only available in the Office 365 tab)
- Exchange ActiveSync
- Exchange Web Services
- Outlook
- Internet email

### Exchange Domain Name Server (DNS) tests

You can run the following tests for Exchange DNS:

- **Help Identify My Issue with Exchange DNS (only available in the Office 365 tab)**: This test will check the external domain name settings for your verified domain in Office 365. The test will look for issues with mail delivery such as not receiving incoming email from the Internet and Outlook client connectivity issues that involve connecting to Outlook and Exchange Online.

### Exchange ActiveSync tests

You can run the following tests for Exchange ActiveSync:

- **Exchange ActiveSync**: This test simulates the steps that a mobile device uses to connect to an Exchange server using Exchange ActiveSync.

### Exchange Web Services connectivity tests

The Exchange Web Services tests check the settings for many of the Exchange Web Services. You can run the following tests for Exchange Web Services:

- **Synchronization, Notification, Availability, and Automatic Replies**: These tests walk through many basic Exchange Web Services tasks to confirm that they're working. This is useful for IT administrators who want to troubleshoot external access using Entourage EWS or other Web Services clients.
- **Service Account Access (Developers)**: This test verifies a service account's ability to access a specified mailbox, create and delete items in it, and access it via Exchange impersonation. This test is primarily used by application developers to test the ability to access mailboxes with alternate credentials.
- **Free/Busy (only available in the Office 365 tab)**: This test verifies that an Office 365 mailbox can access the free/busy information of an on-premises mailbox, and vice versa (one direction per test run).

### Microsoft Office Outlook Connectivity tests

You can run the following tests for Outlook connectivity:

- **Outlook Connectivity**: This test walks through the steps Outlook uses to connect from the internet. It tests connectivity using both the RPC over HTTP and the MAPI over HTTP protocols.

### Internet email tests

You can run the following tests for internet email:

- **Inbound SMTP E-Mail**: This test walks through the steps an internet email server uses to send inbound SMTP email to your domain.
- **Outbound SMTP E-Mail**: This test checks your outbound IP address for certain requirements. This includes Reverse DNS, Sender ID, and RBL checks.
- **POP Email**: This test walks through the steps an email client uses to connect to a mailbox using POP3.
- **IMAP Email**: This test walks through the steps an email client uses to connect to a mailbox using IMAP.