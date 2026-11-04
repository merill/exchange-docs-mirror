---
layout: Conceptual
title: Sensitivity labeling and protection in Outlook for iOS and Android in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android
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
description: How to classify and/or protect messages when using Outlook for iOS and Android.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.reviewer: smithre4
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2019-09-10T00:00:00.0000000Z
locale: en-us
document_id: 4a2a05a7-4cff-8198-b6f8-1f068b3b1d51
document_version_independent_id: 549cd4fb-c9b9-d590-d85f-f6a0b5ee864e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 76d139fe-2683-701f-6f5f-e008dccb46bd
---

# Sensitivity labeling and protection in Outlook for iOS and Android in Exchange Online | Microsoft Learn

**Summary**: How to classify and/or protect messages when using Outlook for iOS and Android.

Protecting company or organizational data is extremely important. Outlook for iOS and Android supports two scenarios for classifying and/or protecting content:

- Sensitivity labeling
- Secure/Multipurpose Internet Mail Extension (S/MIME)

Sensitivity labeling and S/MIME in Outlook for iOS and Android are supported with Microsoft 365 or Office 365 accounts using the native Microsoft sync technology.

## Understanding sensitivity labeling

Sensitivity labeling enables organizations to classify and protect sensitive content. For more information, see [Learn about sensitivity labels](/en-us/purview/sensitivity-labels).

From a classification perspective, a sensitivity label is applied to a message and is retained throughout the message's lifecycle (assuming the label is not removed). In addition, sensitivity labels can be configured to mark content by adding a header or footer to the message body.

Sensitivity labels can also be configured to protect messages with access restrictions or encryption. Access restrictions include ensuring only users within the organization can open the message, restricting editing rights, preventing forwarding, printing, or copying the contents of the message. Encryption provides at-rest encryption and ensures only authorized users can decrypt the message.

When a sensitivity label is configured with encryption, the encryption process depends on the client platform. With Outlook for iOS and Android, encryption occurs within Exchange Online transport after the message is sent from the sender, prior to recipient delivery. Encryption does not occur within the app. For more information, see [Manage sensitivity labels in Office apps](/en-us/purview/sensitivity-labels-office-apps).

Likewise, Outlook for iOS and Android does not perform decryption of received messages, either. Exchange Online performs the decryption prior to delivering the message to Outlook for iOS and Android. For more information, see [Outlook for iOS and Android in Exchange Online: FAQ](outlook-for-ios-and-android-faq).

## Deploying sensitivity Labeling with Outlook for iOS and Android

For information about how to create and define sensitivity labels, as well as, publishing a label policy, see [Create and configure sensitivity labels and their policies](/en-us/purview/create-sensitivity-labels). If you are new to sensitivity labels, you might also find it useful to review [Get started with sensitivity labels](/en-us/purview/get-started-with-sensitivity-labels) for information about licensing, permissions, deployment strategies, and a list of common scenarios that support sensitivity labels.

Important

If your organization has previously deployed Azure Information Protection labels, you must migrate to the unified labeling platform that supports sensitivity labels. To determine which platform is being used, see [Frequently asked questions for Azure Information Protection](/en-us/azure/information-protection/faqs#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform). To complete the migration, see [How to migrate Azure Information Protection labels to unified sensitivity labels](/en-us/azure/information-protection/configure-policy-migrate-labels).

## Using sensitivity labeling with Outlook for iOS and Android

For information about the end user experience, see [Apply sensitivity labels to your documents and email within Office](https://support.microsoft.com/office/2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9).

## Understanding S/MIME

S/MIME provides encryption, which protects the content of email messages, and it provides digital signatures, which verify the identity of the sender of an email message. S/MIME in Outlook for iOS and Android is supported with Microsoft 365 or Office 365 accounts using the native Microsoft sync technology. For a general overview of S/MIME, see [S/MIME in Exchange Online](../../security-and-compliance/smime-exo/smime-exo).

## Deploying and using S/MIME with Outlook for iOS and Android

See [S/MIME for Outlook for iOS and Android](smime-outlook-for-ios-and-android).