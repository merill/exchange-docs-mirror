---
layout: Conceptual
title: Built-in security add-on for on-premises mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/standalone-eop/standalone-eop
Manager: deniseb
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: chrisda
author: chrisda
ms.date: 2025-12-11T00:00:00.0000000Z
audience: ITPro
ms.topic: overview
ms.localizationpriority: medium
ms.assetid: 
description: Admins can learn about using the Built-in security add-on for on-premises mailboxes, including hybrid environments.
ms.service: exchange-online
locale: en-us
document_id: 99f5438a-2743-f7cd-037c-805971181fe7
document_version_independent_id: f3c85cbb-19fc-1c72-ce21-5af06966f326
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/standalone-eop/standalone-eop.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standalone-eop/standalone-eop
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/standalone-eop/standalone-eop.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/390894b2-8646-4f7e-b8cd-2209156272a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/12b23b77-ab37-4318-a036-4f6690586386
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: d40ce79e-fd09-63c0-0085-e405ad79217d
---

# Built-in security add-on for on-premises mailboxes | Microsoft Learn

The built-in security features for all cloud mailboxes are present in all organizations with cloud mailboxes and help protect your cloud organization against malware, spam, and phishing (spoofing). For more information, see [Built-in security features for all cloud mailboxes](/en-us/defender-office-365/eop-about).

But, these same security features are also available to on-premises email organizations without cloud mailboxes as a separate subscription named **the Built-in security add-on for on-premises mailboxes**. The on-premises email organization can use Microsoft Exchange or other SMTP email products.

Tip

If you have an on-premises Exchange organization and you purchased additional Exchange Enterprise CAL with Services licenses, the built-in security features for all cloud mailboxes are part of the included services.

If you configured a hybrid deployment between your on-premises Exchange Organization and Exchange Online, you can configure the built-in security features for all cloud mailboxes to protect your on-premises mailboxes. For more information about hybrid, see [Exchange Server hybrid deployments](../exchange-hybrid).

The Built-in security add-on for on-premises mailboxes can simplify the management of your on-premises email organization and alleviate many of the burdens that come with maintaining on-premises hardware and software.

The articles in this content area apply to the Built-in security add-on for on-premises mailboxes. To learn more about the Built-in security add-on for on-premises mailboxes, check out the [Exchange Online Protection service description](/en-us/office365/servicedescriptions/exchange-online-protection-service-description/exchange-online-protection-service-description).

- **General**:
    - [Set up the Built-in security add-on for on-premises mailboxes](set-up-your-eop-service)
    - [Best practices for configuring the Built-in security add-on for on-premises mailboxes](best-practices-for-configuring-eop)
    - [Exchange admin center in the Built-in security add-on for on-premises mailboxes](exchange-admin-center-eop)
    - [The Built-in security add-on for on-premises mailboxes in China](standalone-eop-china)
- **Permissions**:
    - [Permissions in Exchange Online (and in the Built-in security add-on for on-premises mailboxes)](/en-us/exchange/permissions-exo/permissions-exo)
    - [Manage role groups in Exchange Online (and in the Built-in security add-on for on-premises mailboxes)](/en-us/exchange/permissions-exo/role-groups)
- **Recipients**:
    - [Manage recipients in the Built-in security add-on for on-premises mailboxes](manage-recipients-in-eop)
    - [Manage mail users in Exchange Online (and in the Built-in security add-on for on-premises mailboxes)](/en-us/exchange/recipients-in-exchange-online/manage-mail-users)
- **Auditing**:
    - [Auditing reports in the Built-in security add-on for on-premises mailboxes](auditing-reports-in-eop)
    - [View the admin audit log](/en-us/exchange/security-and-compliance/exchange-auditing-reports/view-administrator-audit-log)
    - [Run an administrator role group report](/en-us/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes)
- **Anti-spam**:
    - [Deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes](configure-eop-spam-protection-hybrid)
- **Scripts**:
    - [Sample script to view settings for the Built-in security add-on for on-premises mailboxes in multiple organizations](sample-script-standalone-eop-settings-to-multiple-tenants)