---
layout: FAQ
title: Hybrid Configuration wizard FAQs | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-configuration-wizard-faqs
summary: >
  <p>Microsoft has released a new Hybrid Configuration wizard (HCW) that simplifies the configuration of a hybrid deployment, allows for more flexibility with your hybrid configuration, and ensures you are always running the most up-to-date versions of the experience. This version of the hybrid wizard is built into Exchange 2016 and releases of Exchange 2013 starting with Cumulative Update 10, but even if you're running an older Exchange 2013 cumulative update (CU), you can still download the new wizard.<br><br></p>

  <p>To download the Hybrid Configuration wizard, go to <a href="https://aka.ms/HybridWizard">https://aka.ms/HybridWizard</a>.</p>
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.date: 2026-10-13T00:00:00.0000000Z
ai-usage: ai-assisted
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: faq
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
ms.assetid: e911e6e0-e36e-4430-ac36-c745a10d6c26
description: Microsoft has released a new Hybrid Configuration wizard that simplifies the configuration of a hybrid deployment, allows for more flexibility with your hybrid configuration, and ensures you are always running the most up-to-date versions of the experience. This version of the hybrid wizard is built into Exchange 2016 and releases of Exchange 2013 starting with Cumulative Update 10, but even if you're running an older Exchange 2013 cumulative update (CU), you can still download the new wizard.
locale: en-us
document_id: 3ec121a3-cccf-1164-777e-be5e4dc9d2c5
document_version_independent_id: 37c911be-c56e-8975-260b-6f8ddc497ee9
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-configuration-wizard-faqs.yml
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: faq
toc_rel: hybridtoc/toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-configuration-wizard-faqs
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-configuration-wizard-faqs.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 495ccf32-44d3-8167-ecb4-c6487e56a172
---

# Hybrid Configuration wizard FAQs | Microsoft Learn

Microsoft has released a new Hybrid Configuration wizard (HCW) that simplifies the configuration of a hybrid deployment, allows for more flexibility with your hybrid configuration, and ensures you are always running the most up-to-date versions of the experience. This version of the hybrid wizard is built into Exchange 2016 and releases of Exchange 2013 starting with Cumulative Update 10, but even if you're running an older Exchange 2013 cumulative update (CU), you can still download the new wizard.

To download the Hybrid Configuration wizard, go to https://aka.ms/HybridWizard.

## Which versions of Exchange support the new Hybrid Configuration wizard?

You can use a combination of one or more of the following versions of Exchange:

- Exchange 2013 CU1 or later
- Exchange 2016 and Exchange 2019

Important

To remain in a supported hybrid configuration, you need to make sure you're running the latest available released CU for your Exchange version. Cumulative updates are released on a quarterly cadence. If you're unable to upgrade to the latest available CU, the previous CU is also supported.

For role-specific requirements and prerequisites, see [Prerequisites for hybrid deployment](hybrid-deployment-prerequisites#prerequisites-for-hybrid-deployment).

## Does the current HCW configure federation trust for Exchange 2010 or earlier?

No. Federation Trust configuration is no longer available in HCW.

## Will this Hybrid Configuration wizard work with Exchange 2007?

No. Exchange 2007 isn't supported.

## Can I opt out of the new Hybrid Configuration wizard?

No. HCW is the supported tool for configuring hybrid mode.

## Can I upgrade my current Exchange 2010 hybrid configuration to Exchange 2013 or Exchange 2016 by using the new Hybrid Configuration wizard?

Yes. Make sure you have at least one server that meets the current Hybrid Configuration wizard requirements and then run it. The wizard will know the current state of your hybrid configuration and seamlessly take you through the upgrade process.

## Does the Exchange hybrid server in my on-premises organization require an Exchange license?

Yes. You need to license your hybrid server when you configure a hybrid deployment. The HCW can detect and license your designated Exchange 2010 SP3, Exchange 2013, or Exchange 2016 hybrid servers for free. You don't need to visit a separate web site or contact Microsoft support. You download the HCW at https://aka.ms/HybridWizard.

The free Exchange Server license isn't available for Exchange 2019 or later hybrid servers.