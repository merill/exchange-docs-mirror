---
layout: Conceptual
title: Microsoft 365 and Office 365 migration performance and best practices | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/office-365-migration-best-practices
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.topic: best-practice
author: AshaIyengar21
ms.author: serdars
ms.reviewer: 
description: There are many paths to migrate data from an on-premises email organization to Microsoft 365 or Office 365. When planning a migration to Microsoft 365 or Office 365, a common question is about how to improve the performance of data migration and optimize migration velocity.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: 77c518bc-12b9-6ee8-362d-70ac54983dd6
document_version_independent_id: 102cd602-f1a6-acf9-a9b8-f47f57de3708
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/office-365-migration-best-practices.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/office-365-migration-best-practices
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/office-365-migration-best-practices.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: db5ce835-478e-3042-815c-294640c8757e
---

# Microsoft 365 and Office 365 migration performance and best practices | Microsoft Learn

There are many paths to migrate email data for an organization hosted on-premises to Microsoft 365 or Office 365. When planning a migration to Microsoft 365 or Office 365, a clear understanding of data migration process and velocity helps the admins to plan better.

## Overview of migrating email to Microsoft 365 or Office 365

Microsoft 365 or Office 365 supports several methods to migrate email, calendar, and contact data from your existing messaging environment to Microsoft 365 or Office 365 as described in [Ways to migrate multiple email accounts to Microsoft 365 or Office 365](mailbox-migration).

For networking and performance related questions on Microsoft 365 or Office 365, see [Network planning and performance tuning for Microsoft 365 or Office 365](/en-us/office365/enterprise/network-planning-and-performance).

### Frequently used migration methods

| Migration method | Description | Resources |
| --- | --- | --- |
| Internet Message Access Protocol (IMAP) migration | You can use the [Exchange admin center](https://admin.exchange.microsoft.com/) or [Exchange Online PowerShell](/en-us/powershell/module/exchangepowershell/) to migrate the contents of users' mailboxes from an **IMAP** messaging system to their Microsoft 365 or Office 365 mailboxes. This includes migrating your mailboxes from other hosted email services, such as Gmail or Yahoo Mail. Note that Exchange Online now offers a [highly specialized process in Modern EAC](/en-us/exchange/mailbox-migration/automated-migration-neweac) for migrating emails from an organizations existing *Gmail/G Suite/Google WorkSpace (GWS) deployment to Exchange Online*. | [Migrate your IMAP mailboxes to Microsoft 365 or Office 365](migrating-imap-mailboxes/migrating-imap-mailboxes) |
| Cutover migration | Use cutover migration to migrate all on-premises mailboxes to Microsoft 365 or Office 365 over a few days. Use cutover migration if you plan to move your entire email organization to Microsoft 365 or Office 365 and manage user accounts in Microsoft 365 or Office 365. You can migrate a maximum of 2,000 mailboxes from your on-premises Exchange organization to Microsoft 365 or Office 365 using a cutover migration. The recommended number of mailboxes, however, is **150**. Performance may likely degrade with numbers higher than that. The mail contacts and distribution groups in your on-premises Exchange organization are also migrated. | [Cutover migration to Microsoft 365 or Office 365](cutover-migration-to-office-365) |
| Staged migration | Use Staged migration if you plan to eventually migrate your organization's all mailboxes to Microsoft 365 or Office 365, over time. Using a staged migration, you migrate batches of on-premises mailboxes to Microsoft 365 or Office 365 over the course of a few weeks or months. | [What you need to know about a staged email migration to Microsoft 365 or Office 365](what-to-know-about-a-staged-migration) |
| Hybrid deployment | Hybrid deployment offers organizations the ability to extend the feature-rich experience and administrative control they have with their existing on-premises Exchange organization to the cloud. A hybrid deployment provides the seamless look and feel of a single Exchange organization between an on-premises Exchange organization and Exchange Online in Microsoft 365 or Office 365. In addition, a hybrid deployment can serve as an intermediate step to moving completely to a Microsoft 365 or Office 365 organization. | [Microsoft 365 and Office 365 Mail migration advisor](/en-us/exchange/mail-migration-jump)[Exchange Server Hybrid Deployments](/en-us/exchange/exchange-hybrid)[Mail migration advisor](../mail-migration-jump)[Exchange Deployment Assistant for Exchange Server](../exchange-deployment-assistant)[Exchange Server 2013 hybrid deployments](../exchange-hybrid)[Minimal Hybrid Configuration](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/HCW-Improvement-The-Minimal-Hybrid-Configuration-option/ba-p/605072) |
| Third-party migration | There are many tools available from third parties. They use distinctive protocols and approaches to conduct email migrations from email platforms like GWS, GoDaddy, Yahoo, IBM Lotus Notes and Novell GroupWise. | Here are some third-party migration tools and partners that can assist with Exchange migrations from third-party platforms: <br>[Binary Tree](https://www.binarytree.com/) / [Quest](https://www.quest.com/) / [QuadroTech](https://www.quadrotech-it.com/): Binary Tree and QuadroTech are now part of Quest. Quest is a provider of cross-platform messaging migration and coexistence software, with products for analysis, co-existence, and migration between multiple platforms to Exchange Online. Quest solutions synchronize mailboxes, public folders and calendar information while maintaining coexistence throughout the migration. <br><br>[BitTitan](https://www.bittitan.com): Provides automated solution for migrations to Microsoft 365 or Office 365 from a wide range of platforms. <br><br>[CodeTwo](https://www.codetwo.com/): Provider of Microsoft 365 and Office 365 migration solutions for secure and automated data migrations to Microsoft 365 (Office 365) from Exchange On-Prem, IMAP servers, and between Microsoft 365 tenants. <br><br>[Transvault](https://www.transvault.com/email-archive-migrations/): Provider of Cloud Office migration solutions to Microsoft 365 from Exchange and Notes. Transvault supports dozens of sources for migration and offers products which deliver any size of project, complex email archive migrations and PST management. The enterprise migration solutions are secure, compliant, efficient, and user-focused, and can be run both on-premises and in the Cloud. <br><br>[BCC](http://www.bcchub.com/): Helping companies by supporting their collaboration migration strategy. Best in class supplier of migration tools based on Domino platform, for migrating to Microsoft Exchange, Microsoft 365, and Office 365. |

## Performance for Migration methods

The following sections compare mailbox migration workloads and the observed performance results for the different migration methods for migrating mailboxes and mailbox data to Microsoft 365 or Office 365. These results are based on internal testing and actual customer migrations to Microsoft 365 or Office 365.

Important

Because of differences in how migrations are performed and when they're performed, your actual migration velocity may vary.

### Customer migration workloads

The following table describes the different workloads involved in a typical migration, and the challenges and options for each.

| Workload | Notes |
| --- | --- |
| Onboarding (Migrating to Microsoft 365 or Office 365) | Microsoft offers data migration capability and tools for customers to use to migrate their data from Exchange Server On-premises (via [Cutover](/en-us/exchange/mailbox-migration/cutover-migration-to-office-365)/[Staged](/en-us/exchange/mailbox-migration/perform-a-staged-migration/perform-a-staged-migration)/[Hybrid](/en-us/exchange/hybrid-deployment/hybrid-deployment)) or from Gmail/S Suite/GWS aka Google Work Space (via [EAC](/en-us/exchange/mailbox-migration/automated-migration-neweac), [PowerShell](/en-us/exchange/mailbox-migration/perform-gspace-migration-powershell)) or from [Other IMAP sources](/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrate-other-types-of-imap-mailboxes)([PowerShell](/en-us/microsoft-365/enterprise/use-powershell-to-perform-an-imap-migration-to-microsoft-365), [Gmail via IMAP](/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrate-g-suite-mailboxes)) or [Cross Tenant migrations](/en-us/exchange/mailbox-migration/migrate-mailboxes-across-tenants) to Exchange Online in Microsoft 365 or Office 365. |
| Multi-Geo | Multinational companies with offices around the world often have a need to store their employee data at-rest in specific regions, in order to meet their data residency requirements. Multi-Geo enables a single Microsoft 365 or Office 365 organization to span across multiple Microsoft 365 or Office 365 datacenter geographies (geos), which gives you the ability to store Exchange data, at-rest, on a per-user basis, in your chosen geos. For more details, see [Get enterprise-grade global data location controls with Multi-Geo](https://products.office.com/business/multi-geo-capabilities). |
| Encryption | Service Encryption with Customer Key is a feature that allows a customer to provision and manage the root keys that are used to encrypt data at-rest at the application layer in Microsoft 365 or Office 365. For a mailbox to become encrypted the first time, a mailbox move is required. For more details, see [Service encryption with Microsoft Purview Customer Key](/en-us/purview/customer-key-overview). |
| GoLocal | Microsoft continues to open new datacenters in new regions, or geos. Existing customers, when eligible, can request to have their customer data from their original datacenter moved to a new geo. The period in which you can make this request is usually one or two years, depending on the overall demand for the service. Note that this period during which you can request to have your customer data moved becomes shorter once a datacenter (DC) for the new geo launches (at that point you have approximately three to six months to request a move). Details are available in [Moving core data to new Microsoft 365 datacenter geos](/en-us/Office365/Enterprise/moving-data-to-new-datacenter-geos). |

When mailboxes are migrated within Microsoft 365 data centers, every mailbox move or bulk-mailbox move requires time for the operation to complete. There are a number of factors, such as Microsoft 365 service activity, that can affect exactly how much time. The service is designed to throttle discretionary workloads like mailbox moves, to ensure that the service runs optimally for all users. You can still expect mailbox moves to be processed, however, depending on the service's discretionary resource availability. More details about resource throttling can be found in [this blog post](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/Resource-Based-Throttling-and-Prioritization-in-Exchange-Online/ba-p/608020).

### Duration estimates for mailbox migration in Exchange Online

To help you plan your migration, the following tables present guidelines about when to expect bulk mailbox migrations or individual migrations to complete. These estimates are based on a data analysis of previous customer migrations. Because every environment is unique, your exact migration velocity may vary.

**Mailbox migration duration based on mailbox size profiles**:

- [GoLocal](/en-us/microsoft-365/enterprise/moving-data-to-new-datacenter-geos)/[Multi-Geo](https://www.microsoft.com/microsoft-365/business/multi-geo-capabilities?rtc=1)/[Encryption](/en-us/purview/customer-key-overview) in Exchange Online

    | Workload | Mailbox size (GB) | P50 (50th percentile duration) (days) | P90 (90th percentile duration) (days) |
    | --- | --- | --- | --- |
    | GoLocal/Multi-Geo/Encryption | 0 - 10 | 1 | 1 |
    | GoLocal/Multi-Geo/Encryption | 10 - 50 | 2 | 6 |
    | GoLocal/Multi-Geo/Encryption | 50 - 100 | 4 | 11 |
    | GoLocal/Multi-Geo/Encryption | 100 - 200 | 6 | 14 |
    | GoLocal/Multi-Geo/Encryption | &gt; 200 | Not supported | Not supported |
- Onboarding to Exchange Online from On-Premises Exchange Servers ([Cutover](/en-us/exchange/mailbox-migration/cutover-migration-to-office-365)/[Staged](/en-us/exchange/mailbox-migration/perform-a-staged-migration/perform-a-staged-migration)/[Hybrid](/en-us/exchange/hybrid-deployment/hybrid-deployment))

    | Workload | Mailbox size (GB) | P50 (50th percentile duration) (days) | P90 (90th percentile duration) (days) |
    | --- | --- | --- | --- |
    | Onboarding from On-Premises | 0 - 10 | 1 | 3 |
    | Onboarding from On-Premises | 10 - 50 | 2 | 6 |
    | Onboarding from On-Premises | 50 - 100 | 4 | 13 |
    | Onboarding from On-Premises | 100 - 200 | 10 | 31 |
    | Onboarding from On-Premises | &gt; 200 | Not supported | Not supported |
- Cross Tenant Migration to Exchange Online (use [Microsoft first party solution](/en-us/microsoft-365/enterprise/cross-tenant-mailbox-migration?view=o365-worldwide&amp;preserve-view=true) or use [Third party solutions](migrate-mailboxes-across-tenants)).

    | Workload | Mailbox size (GB) | P50 (50th percentile duration) (days) | P90 (90th percentile duration) (days) |
    | --- | --- | --- | --- |
    | Cross Tenant | 0 - 10 | 1 | 1 |
    | Cross Tenant | 10 - 50 | 1 | 2 |
    | Cross Tenant | 50 - 100 | 2 | 5 |
    | Cross Tenant | 100 - 200 | 3 | 6 |
    | Cross Tenant | &gt; 200 | Not supported | Not supported |
- Specialized Onboarding to Exchange Online from Gmail/G Suite/GWS ([EAC](/en-us/exchange/mailbox-migration/automated-migration-neweac), [PowerShell](/en-us/exchange/mailbox-migration/perform-gspace-migration-powershell))

    | Workload | Mailbox size (GB) | P50 (50th percentile duration) (days) | P90 (90th percentile duration) (days) |
    | --- | --- | --- | --- |
    | Specialized Gmail Onboarding | 0 - 10 | 1 | 2 |
    | Specialized Gmail Onboarding | 10 - 50 | 1 | 8 |
    | Specialized Gmail Onboarding | 50 - 100 | 3 | 12 |
    | Specialized Gmail Onboarding | 100 - 200 | 5 | 19 |
    | Specialized Gmail Onboarding | &gt; 200 | Not supported | Not supported |
- [Onboarding to Exchange Online from IMAP sources](/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes) ([Other IMAP sources](/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrate-other-types-of-imap-mailboxes), [PowerShell](/en-us/microsoft-365/enterprise/use-powershell-to-perform-an-imap-migration-to-microsoft-365), [Gmail via IMAP](/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrate-g-suite-mailboxes))

    | Workload | Mailbox size (GB) | P50 (50th percentile duration) (days) | P90 (90th percentile duration) (days) |
    | --- | --- | --- | --- |
    | Generic IMAP Onboarding | 0 - 10 | 1 | 1 |
    | Generic IMAP Onboarding | 10 - 50 | 1 | 2 |
    | Generic IMAP Onboarding | 50 - 100 | 1 | 8 |
    | Generic IMAP Onboarding | 100 - 200 | 3 | 29 |
    | Generic IMAP Onboarding | &gt; 200 | Not supported | Not supported |
- [Onboarding to Exchange Online via PST Import](/en-us/purview/importing-pst-files-to-office-365)

    | Workload | Mailbox size (GB) | P50 (50th percentile duration) (days) | P90 (90th percentile duration) (days) |
    | --- | --- | --- | --- |
    | PST Import | 0 - 10 | 1 | 1 |
    | PST Import | 10 - 50 | 1 | 3 |
    | PST Import | 50 - 100 | 2 | 5 |
    | PST Import | 100 - 200 | 3 | 6 |
    | PST Import | &gt; 200 | Not supported | Not supported |

Note

Some outlier mailboxes would take longer to complete based on the mailbox profile. Also, if a tenant has larger mailboxes on average, this can also contribute to the extended duration of migration.

## Migration performance factors

Mailbox/Email migration have several common factors that affect migration performance.

### Common migration performance factors

The following table provides a list of common factors that affect migration performance. More details are covered in the sections describing the individual migration methods.

| Factor | Description | Example |
| --- | --- | --- |
| Data source | The device or service that hosts the data to be migrated. Many limitations might apply to the data source because of hardware specifications, end-user workload, and back-end maintenance tasks. | Gmail limits how much data can be extracted during a specific period of time. |
| Data type and density | Because of the unique nature of a customer's business, the type and mix of mail items within mailboxes vary greatly. | One 4-GB mailbox with 400 items, each with 10 megabytes (MB) of attachments, will migrate faster than one 4-GB mailbox with 100,000 smaller items. |
| Migration server | Many migration solutions use a "jump box" type of migration server or workstation to complete the migration. | Customers often use a low-performance virtual machine to host the MRSProxy service for hybrid deployments or for client PC non-hybrid migrations. |
| Migration engine | The data migration engine responsible for pulling data from the source server converts data, if necessary. The engine then transmits the data over the network and injects the data into the Microsoft 365 or Office 365 mailbox. mailbox. | MRSProxy service has its own capabilities and limitations. |
| On-premises network appliances | The end-to-end network performance (from the data source to Exchange Online client access servers) affects migration performance. | Firewall configuration and specifications on the on-premises organization. |
| Microsoft 365 or Office 365 service | Microsoft 365 and Office 365 have built-in support and features to manage the migration workload. | The user-throttling policy has default settings and limits the overall maximum data transfer rate. |

### Network performance factors

This section describes best practices for improving network performance during migration. The discussion is general because the biggest impact on network performance during migration is related to third-party hardware and Internet service providers (ISPs).

Use the Exchange Analyzer to get a deeper understanding of your network connectivity with Microsoft 365 or Office 365. To run the Exchange Analyzer tests in [Microsoft Support and Recovery Assistant](https://support.microsoft.com/en-us/office/about-the-microsoft-support-and-recovery-assistant-e90bb691-c2a7-4697-a94f-88836856c72f), go to Advanced Diagnostics &gt; Exchange Online &gt; Check Exchange Online network connectivity &gt; Yes. Read about the Microsoft Support and Recovery Assistant to learn more about [Microsoft Support and Recovery Assistant](https://support.microsoft.com/en-us/office/about-the-microsoft-support-and-recovery-assistant-e90bb691-c2a7-4697-a94f-88836856c72f).

| Factor | Description | Best practices |
| --- | --- | --- |
| Network capacity | The amount of time it takes to migrate mailboxes to Microsoft 365 or Office 365 is determined by the available and maximum capacity of your network. | Identify your available network capacity and determine the maximum upload capacity.  Contact your ISP to confirm your allocated bandwidth and to get details about restrictions, such as the total amount of data that can be transferred in a specific period of time.  Use tools to evaluate your actual network capacity. Make sure you test the end-to-end flow of data from your on-premises data source to the Microsoft datacenter gateway servers.  Identify other loads on your network (for example, backup utilities and scheduled maintenance) that can affect your network capacity. |
| Network stability | A fast network doesn't always result in fast migrations. If the network isn't stable, data transfer takes longer because of error correction. Depending on the migration type, error correction can significantly affect migration performance. | Network hardware and driver issues often cause network stability problems. Work with your hardware vendors to understand your network devices and apply the vendor's latest recommended drivers and software updates. |
| Network delays | Intrusion detection functionality configured on a network firewall often causes significant network delays and affects migration performance.  Migrating data to Microsoft 365 or Office 365 mailboxes relies on your internet connection. Internet delays affect overall migration performance.  Also, users in the same company might have cloud mailboxes that reside in datacenters in different geographical locations. Depending on the customer's ISP, migration performance may vary. | Evaluate network delays to all potential Microsoft datacenters to help ensure that the result is consistent. (This also helps ensure a consistent experience for end users.) Work with your ISP to address internet-related issues.  Add IP addresses for Microsoft datacenter servers to your allow list, or bypass all migration-related traffic from your network firewall. For more information about the Microsoft 365 or Office 365 IP ranges, see [Microsoft 365 and Office 365 URLs and IP address ranges](/en-us/office365/enterprise/urls-and-ip-address-ranges). |

For a deeper analysis of migrations within your environment, check out our [Mailbox Migration Performance Analysis](https://techcommunity.microsoft.com/t5/exchange-team-blog/mailbox-migration-performance-analysis/ba-p/587134). The post includes a script to help you analyze move requests.

## Microsoft 365 and Office 365 throttling

Microsoft 365 and Office 365 use various throttling mechanisms to help ensure security and service availability. The following three types of throttling can affect migration performance:

- User throttling
- Migration-service throttling
- Resource health-based throttling

Note

The three types of Microsoft 365 and Office 365 throttling don't affect all migration methods.

### Microsoft 365 and Office 365 user throttling

User throttling affects most third-party migration tools and the client-uploading migration method. These migration methods use client access protocols, such as the Remote Procedure Call (RPC) over HTTP Protocol, to migrate mailbox data to Microsoft 365 or Office 365 mailboxes. These tools are used to migrate data from platforms such as IBM Lotus Domino and Novell GroupWise.

User throttling is the most restrictive throttling method in Microsoft 365 and Office 365. Because user throttling is set up to work against an individual end user, any application-level usage will easily exceed the throttling policy and result in slower data migration.

### Microsoft 365 and Office 365 migration-service throttling

Migration-service throttling affects all Microsoft 365 or Office 365 migration tools. Migration-service throttling manages migration concurrency and service resource allocation for Microsoft 365 or Office 365 migration solutions.

Migration-service throttling affects migrations performed by using the following migration methods:

- IMAP migration
- Cutover Exchange migration
- Staged Exchange migration
- Hybrid migrations (MRSProxy service-based moves in a hybrid environment)

Important

The aforementioned migration methods are not affected by user throttling.

An example of migration-service throttling is controlling the number of mailboxes that are migrated simultaneously during simple Exchange migrations and IMAP migrations. The default value is 20. This means that a maximum of 20 mailboxes from all migration batches are migrated at any time. You can increase the number of concurrent mailbox migrations for a migration batch in either the Exchange admin center or Windows PowerShell. To learn more about how to optimize this setting, see [Manage migration batches in Microsoft 365 or Office 365](manage-migration-batches).

### Microsoft 365 or Office 365 resource health-based throttling

All migration methods are subject to the governance of availability throttling. Microsoft 365 or Office 365 service throttling, however, doesn't affect Microsoft 365 or Office 365 migrations as much as the other types of throttling described previously.

Resource health-based throttling is the least aggressive throttling method. It occurs to prevent a service availability issue that could affect end users and critical service operations.

Before performance of the service degrades to the point where end-user performance could be impacted, hybrid migrations will be stalled until performance is recovered and the service returns to a level below the throttling threshold.

The following shows what the customers will see regarding stall durations using `Get-MoveRequestStatistics - <> -IncludeReport` cmdlet:

```
$R.REPORT.TARGETTHROTTLES
NETWORKTHROTTLE : 00:00:00
CPUTHROTTLE : 00:02:07.6222549
REMOTESERVERTHROTTLE : 00:00:00
MDBREPLICATIONTHROTTLE : 00:38:41.7018480
CONTENTINDEXINGTHROTTLE : 00:00:00
BIGFUNNELTHROTTLE : 00:00:00
MDBAVAILABILITYTHROTTLE : 00:26:34.6588104
DISKLATENCYTHROTTLE : 1.15:45:37.7873632

$R.REPORT.SOURCETHROTTLES
NETWORKTHROTTLE : 00:00:00
CPUTHROTTLE : 3.03:21:07.7192848
REMOTESERVERTHROTTLE : 00:00:00
MDBREPLICATIONTHROTTLE : 00:00:00

CONTENTINDEXINGTHROTTLE : 00:00:00
BIGFUNNELTHROTTLE : 00:00:00
MDBAVAILABILITYTHROTTLE : 00:00:00
DISKLATENCYTHROTTLE : 00:20:47.1101552
MDBMAINTENANCETHROTTLE : 00:00:00

```

**Solution and practice**:

If you experience a comparable situation, wait for the Microsoft 365 or Office 365 resources to become available.

## Performance factors and best practices for non-hybrid deployment migrations

This section describes factors that affect migrations using the IMAP, cutover, or staged migration methods. It also identifies best practices to improve migration performance.

### Factor 1: Data source for non-hybrid deployment migrations

The following table describes the impact on migration by the source servers in your current email organization and the best practices for mitigating the impact on migration.

| Checklist | Description | Best practices |
| --- | --- | --- |
| System performance | Data extraction is an intensive task. The source system needs to have sufficient resources, such as CPU time and memory, to provide optimal migration performance. During migration, the source system is often close to full capacity in terms of the regular end-user workload. If system resources are inadequate, the additional workload that results from migration can affect end users. | Monitor system performance during a pilot migration test. If the system is busy, we recommend avoiding an aggressive migration schedule for the specific system because of potential migration slowness and service availability issues. If possible, enhance the source system performance by adding hardware resources and reduce the load on the system by moving tasks and users to other servers that aren't involved in the migration. <br> For more information, see: Server Health and Performance of Exchange Server ([2007](/en-us/previous-versions/office/exchange-server-2007/bb201689%28v=exchg.80%29), [2010](/en-us/previous-versions/office/exchange-server-2010/dd351192%28v=exchg.141%29), [2013](/en-us/exchange/server-health-and-performance-exchange-2013-help), [2016](/en-us/exchange/server-health/server-health), [2019](/en-us/exchange/server-health/server-health)) <br><br>**Note**: Exchange Servers 2007 and 2010 are no longer actively supported. Exchange 2013 Server end of support is scheduled for [April, 2023](https://techcommunity.microsoft.com/t5/exchange-team-blog/exchange-server-2013-end-of-support-reminder/ba-p/3549596). Exchange Server 2016 and 2019 are in extended support until October 2025. See the [Exchange Server supportability matrix](/en-us/exchange/plan-and-deploy/supportability-matrix) for more details. <br><br> When migrating from an on-premises Exchange organization where there are multiple mailbox servers, we recommend that you create a migration-user list that is evenly distributed across multiple mailbox servers. Based on individual server performance, the list can be further fine-tuned to maximize throughput. <br><br> For example, if server A has 50 percent more resource availability than server B, it's reasonable to have 50 percent more users from server A in the same migration batch. Similar practices can be applied to other source systems. Perform migrations when servers have maximum resource availability such as after hours or on weekends and holidays. |
| Back-end tasks | Other back-end tasks that are running during migration time. Because it's a best practice to perform migration after business hours, it's common that migrations conflict with maintenance tasks (such as data backup) running on your on-premises servers. | Review other system tasks that might be running during migration. We recommend that you perform data migration when no other resource-intensive tasks are running. **Note**: For customers using on-premises Exchange, the common back-end tasks are backup solutions and Exchange store maintenance ([2013](/en-us/exchange/managed-store-exchange-2013-help), [2016](/en-us/exchange/architecture/mailbox-servers/managed-store/managed-store), [2019](/en-us/exchange/architecture/mailbox-servers/managed-store/managed-store)). |
| Throttling policy | It is a common practice to protect email systems with a throttling policy that sets a specific limit on how fast and how much data can be extracted from the system during a certain amount of time. | Verify the throttling policy deployed for your email system. For example, Google Mail limits how much data can be extracted in a certain period. Depending on the version, Exchange has policies that restrict IMAP access to the on-premises mail server (used by IMAP migrations) and RPC over HTTP Protocol access (used by cutover Exchange migrations and staged Exchange migrations). <br> To check the throttling settings, run the [Get-ThrottlingPolicy](/en-us/powershell/module/exchangepowershell/Get-ThrottlingPolicy) cmdlet. For more information about throttling, see: ([2007](/en-us/previous-versions/office/exchange-server-2007/cc540454%28v=exchg.80%29), [2010](/en-us/previous-versions/office/exchange-server-2010/dd297964%28v=exchg.141%29), [2013](/en-us/exchange/exchange-workload-management-exchange-2013-help), [2016](/en-us/exchange/server-health/workload-management), [2019](/en-us/exchange/server-health/workload-management)). <br><br> For more information about IMAP throttling, see [Migrate your IMAP mailboxes to Microsoft 365 or Office 365](/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes). |

### Factor 2: Migration server for non-hybrid deployment migrations

IMAP, cutover, and staged migrations are cloud-initiated data-pull migration methods, so there's no need for a dedicated migration server. The internet-facing protocol hosts (IMAP or RPC over HTTP Protocol), however, function as the migration server for migrating mailboxes and mailbox data to Microsoft 365 or Office 365. Therefore, the migration performance factors and best practices, described in the previous section about the data source server for your current email organization, also apply to the internet edge servers. For Exchange 2007, Exchange 2010, and Exchange 2013, organizations, the client access server functions as a migration server.

For more information, see:

- [Exchange Server 2007: Monitoring Client Access Servers](/en-us/previous-versions/office/exchange-server-2007/bb201674%28v=exchg.80%29)
- [Exchange Server 2010: Client Access Server Counters](/en-us/previous-versions/office/exchange-server-2010/ff367877%28v=exchg.141%29)
- [Exchange Server 2013: Exchange workload management](/en-us/exchange/exchange-workload-management-exchange-2013-help)
- [Exchange Server 2016: User workload management in Exchange Server](/en-us/exchange/server-health/workload-management)
- [Exchange Server 2019: User workload management in Exchange Server](/en-us/exchange/server-health/workload-management)

### Factor 3: Migration engine for non-hybrid deployment migrations

IMAP, cutover, and staged Exchange migrations are performed by using the Migration dashboard in the Exchange admin center. This is subject to Microsoft 365 or Office 365 migration-service throttling.

**Solution and practice**:

Customers now can specify migration concurrency (for example, the number of mailboxes to migrate simultaneously) by using Windows PowerShell. The default is 20 mailboxes. After you create a migration batch, you can use the following Windows PowerShell cmdlet to increase this to a maximum of 100.

```PowerShell
Set-MigrationEndPoint <Identity> -MaxConcurrentMigrations <value between 1 and 100>
```

For more information, see [Manage migration batches in Microsoft 365 or Office 365](manage-migration-batches).

Note

If your data source doesn't have sufficient resources to manage all the connections, we recommend avoiding high concurrency. Start with a small concurrency value, for example, 10. Increase this number while monitoring the data source performance to avoid end-user access issues.

### Factor 4: Network for non-hybrid deployment migrations

**Verification tests**:

Depending on the migration method, you can try the following verification tests:

- **IMAP migrations**: Prepopulate a source mailbox with sample data. Then from the internet (outside your on-premises network), connect to the source mailbox by using a standard IMAP email client such as Microsoft Outlook, and then measure network performance by determining how long it takes to download all the data from the source mailbox. The throughput should be similar to what customers can get by using the IMAP migration tool in Microsoft 365 or Office 365, given that there are no other constraints.
- **Cutover and staged Exchange migrations**: Prepopulate a source mailbox with sample data. Then, from the internet (outside of your on-premises network), connect to the source mailbox with Outlook by using RPC over HTTP Protocol. Make sure that you're connecting by using [cached mode](/en-us/outlook/troubleshoot/deployment/cached-exchange-mode). Measure network performance by checking how long it takes to synchronize all data from the source mailbox. The throughput should be similar to what customers can get by using the simple Exchange migration tools in Microsoft 365 or Office 365, given that there are no other constraints.

There is some overhead during an actual IMAP, cutover, or staged Exchange migration. The actual throughput, however, should be similar to the results of these verification tests.

### Factor 5: Microsoft 365 and Office 365 service for non-hybrid deployment migrations

Microsoft 365 or Office 365 resource health-based throttling affects migrations using the native Microsoft 365 or Office 365 simple migration tools. See the Microsoft 365 or Office 365 resource health-based throttling section.

## Move requests in the Microsoft 365 or Office 365

For general information about getting status information for move requests, see View Move Request Properties:

- [Move-Mailbox](/en-us/previous-versions/office/exchange-server-2007/aa997599%28v=exchg.80%29)
- [Get-MoveRequestStatistics]](/powershell/module/exchangepowershell/get-moverequeststatistics)

In the Microsoft 365 or Office 365 service the migration queue and the service resources allocated for migrations are shared among tenants and affects how move requests are managed in each stage of the move process.

There are two types of move requests in Microsoft 365 and Office 365:

- **Onboarding "move" requests**: The new customer migrations are considered onboarding move requests. These requests have regular priority.
- **Datacenter internal "move" requests**: These are mailbox move requests initiated by datacenter operation teams. These requests have a lower priority because the end-user experience isn't affected if the move request is delayed.

### Potential impact and delays to move requests with a status of "Queued" and "In Progress"

- **Queued move requests**: This status specifies that the move has been queued and is waiting for Exchange Mailbox Replication Service to pick it up. For Exchange 2003 move requests, users can still access their mailboxes at this stage.

    Two factors influence which request will be picked up by the Mailbox Replication Service:

    - **Priority**: Queued move requests with a higher priority are picked up before lower-priority move requests. This helps ensure that customer-migration move requests always get processed before datacenter internal move requests.
    - **Position in the queue**: If move requests have the same priority, the earlier the request gets into the queue, the earlier it will be picked up by the Mailbox Replication Service. Because there might be multiple customers performing mailbox migrations at the same time, it's normal that new move requests remain in the queue before they're processed.

Often, the time that mailbox requests wait in the queue before being processed isn't considered during migration planning. This results in customers not being allocated enough time to complete all planned migrations.

- **In-progress move requests**: This status specifies that the move is still in progress. If this is an online mailbox move, the user will still be able to access the mailbox.

After the mailbox move request has a status of "In Progress," the priority no longer matters and a new move request won't be processed until an existing "In Progress" move request is completed, even if the new move request has a higher priority.

### Best practices

**Planning**: As previously mentioned, because Exchange 2003 users lose access during a hybrid migration, Exchange 2003 customers are usually more concerned about when to schedule migrations and how long they will take.

When planning how many mailboxes to migrate during a specific time period, consider the following:

- Include the amount of time the move request waits in the queue. Use the following to calculate this:

    *(total number of mailboxes to migrate) = ((total time) - (average queue time)) \* (migration throughput)*

    where the migration throughput equals the total number of mailboxes that can be migrated per hour.

For example, assume you have a six-hour window to migrate mailboxes. If the average queue time is one hour and you have a migration throughput of 100 mailboxes per hour, you can migrate 500 mailboxes in the six-hour time frame: 500 = (6 - 1) \* 100.

- Start the migration sooner than initially planned to mitigate time in the queue. When mailboxes are queued, Exchange 2003 users can still access their mailboxes.

**Determine queue time**: The queue time is always changing because Microsoft doesn't manage customers' migration schedules.

To determine the potential queue time, a customer can try to schedule a test move several hours before the actual migration starts. Then, based on the observed amount of time the request is in the queue, the customer can better estimate when to start the migration and how many mailboxes can be moved in a specific period of time.

For example, if a test migration was completed four hours before the start of a planned migration. The customer determines the queue time for the test migration was about one hour. Then, the customer should consider starting the migration one hour earlier than originally planned to make sure there is enough time to complete all migrations.

## Third-party tools for Microsoft 365 or Office 365 migrations

Third-party tools are mostly used in migration scenarios that don't involve Exchange, such as those from Gmail/G Suite/GWS (Google Workspace), IBM Lotus, Domino, and Novell GroupWise. This section focuses on the migration protocols used by third-party migration tools, rather than on the actual products and migration tools. The following table provides a list of factors that apply to third-party tools for Microsoft 365 or Office 365 migration scenarios.

Important

For issues with data consistency or integrity after performing a migration using third-party tools, please contact the vendor who provided the tool for support.

### Factor 1: Data source for third-party tool migrations

| Checklist | Description | Best practices |
| --- | --- | --- |
| System performance | Data extraction is an intensive task. The source system must have sufficient resources, such as CPU time and memory, to provide optimal migration performance. During migration, the source system is often close to full capacity in terms of the regular end-user workload. If system resources are inadequate, the additional workload that results from migration can affect end users. | Monitor system performance during a pilot migration test. If the system is busy, we recommend avoiding an aggressive migration schedule for the specific system because of potential migration slowness and service availability issues. If possible, enhance the source system performance by adding hardware resources and reduce the load on the system by moving tasks and users to other servers that aren't involved in the migration. <br> For more information, see: Server Health and Performance of Exchange Server ([2007](/en-us/previous-versions/office/exchange-server-2007/bb201689%28v=exchg.80%29), [2010](/en-us/previous-versions/office/exchange-server-2007/bb201689%28v=exchg.80%29), [2013](/en-us/exchange/server-health-and-performance-exchange-2013-help), [2016](/en-us/exchange/server-health-and-performance-exchange-2013-help), [2019](/en-us/exchange/server-health-and-performance-exchange-2013-help)). <br><br>**Note**: Exchange Servers 2007 and 2010 are no longer actively supported. Exchange 2013 Server end of support is scheduled for [April, 2023](https://techcommunity.microsoft.com/t5/exchange-team-blog/exchange-server-2013-end-of-support-reminder/ba-p/3549596). Exchange Server 2016 and 2019 are in extended support until October 2025. See the [Exchange Server supportability matrix](/en-us/exchange/plan-and-deploy/supportability-matrix) for more details. <br><br> When migrating from an on-premises Exchange organization where there are multiple mailbox servers, we recommend that you create a migration user list that's evenly distributed across multiple mailbox servers. Based on individual server performance, the list can be further fine-tuned to maximize throughput. <br><br> For example, if server A has 50 percent more resource availability than server B, it is reasonable to have 50 percent more users from server A in the same migration batch. A similar practice can be applied to other source systems. <br><br> Perform migrations when servers have maximum resource availability such as after hours or on weekends and holidays. |
| Back-end tasks | Other back-end tasks usually run during migration time. Because it's a best practice to perform migration after business hours, it's common that migrations conflict with other maintenance tasks running on your on-premises servers, such as data backup. | Review other system tasks that might be running during migration. We recommend that you perform data migration when no other resource-intensive tasks are running. <br>**Note**: For customers using on-premises Exchange, the common back-end tasks are backup solutions and Exchange store maintenance ([2013](/en-us/exchange/managed-store-exchange-2013-help), [2016](/en-us/exchange/architecture/mailbox-servers/managed-store/managed-store), [2019](/en-us/exchange/architecture/mailbox-servers/managed-store/managed-store)). |
| Throttling policy | It's a common practice to protect email systems with a throttling policy, which sets a specific limit on how fast and how much data can be extracted from the system within a certain amount of time and by using a specific migration method. | Verify the throttling policy deployed for your email system. For example, Google Mail limits how much data can be extracted in a certain period. Depending on the version, Exchange has policies that restrict IMAP access to the on-premises mail server (used by IMAP migrations) and RPC over HTTP Protocol access (used by cutover Exchange migrations and staged Exchange migrations). <br> To check the throttling settings, run the [Get-ThrottlingPolicy](/en-us/powershell/module/exchangepowershell/Get-ThrottlingPolicy) cmdlet. For more information about throttling, see: ([2007](/en-us/previous-versions/office/exchange-server-2007/cc540454%28v=exchg.80%29), [2010](/en-us/previous-versions/office/exchange-server-2010/dd297964%28v=exchg.141%29), [2013](/en-us/exchange/exchange-workload-management-exchange-2013-help), [2016](/en-us/exchange/server-health/workload-management), [2019](/en-us/exchange/server-health/workload-management)). <br><br> For more information about IMAP throttling, see [Migrate your IMAP mailboxes to Microsoft 365 or Office 365](/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes). |

### Factor 2: Migration server for third-party tool migrations

Most third-party tools for Microsoft 365 or Office 365 migrations are client initiated and push data to Microsoft 365 or Office 365. These tools typically require a migration server. Factors such as system performance, back-end tasks, and throttling policies for the source servers apply to these migration servers.

Note

Some third-party migration solutions are hosted on the internet as cloud-based services and don't require an on-premises migration server.

**Solution and practice**:

To improve migration performance when using a migration server, apply the same best practices as the ones described in the Factor 1: Data source for third-party tool migrations section.

### Factor 3: Migration engine for third-party tool migrations

For third-party migration tools, the most common protocols used are Exchange Web Services and RPC over HTTP Protocol.

**Exchange Web Services**:

Exchange Web Services is the recommended protocol to use for migrating to Microsoft 365 or Office 365 because it supports large data batches and has better service-oriented throttling. In Microsoft 365 or Office 365, when used in impersonation mode, migrations using Exchange Web Services don't consume the user's budgeted amount of Microsoft 365 or Office 365 Exchange Web Services resources, consuming instead a copy of the budgeted resources:

- All Exchange Web Services impersonating calls made by the same administrator account are calculated separately from the budget applied to this administrator account.
- For each impersonation session, a shadow copy of the actual user's budget is created. All migrations for this particular session will consume this shadow copy.
- Throttling under impersonation is isolated to each user migration session.
- Exchange Web Services throttling policy can be temporarily changed in the tenant (for a duration of 30, 60, or 90 days) to allow migration to complete. This can be requested from the Help section of the Microsoft 365 admin center.

**Best practices**:

- Migration performance for customers using third-party migration tools that use EWA impersonation competes with Exchange Web Services-based migrations and service resource usage by other tenants. Therefore, migration performance will vary.
- Whenever possible, customers should use third-party migration tools that use Exchange Web Services impersonation because it's usually faster and more efficient than using client protocols such as RPC over HTTP Protocol.

**RPC over HTTP Protocol**:

Traditional migration solutions use the RPC over HTTP Protocol. This method is completely based on a client access model such as that of Outlook, and scalability and performance are limited because the Microsoft 365 or Office 365 service throttles access on the assumption that usage is by a user instead of by an application.

**Best practices**:

- For migration tools that use RPC over HTTP Protocol, it's a common practice to increase migration throughput by adding more migration servers and using multiple Microsoft 365 or Office 365 administrative user accounts. This practice can gain data injection parallelism and achieve higher data throughput because each administrative user is subject to Microsoft 365 and Office 365 user throttling. We have received reports that many enterprise customers had to set up more than 40 migration servers to obtain 20-30 GB/hour of migration throughput.
- In a migration tool development phase, it's critical to consider the number of RPC operations needed to migrate a message. To illustrate this, we have collected logs captured by Microsoft 365 or Office 365 services for two third-party migration solutions (developed by third-party companies) used by customers to migrate mailboxes to Microsoft 365 or Office 365. We compared two migration solutions developed by third-party companies. We compared the migration of two mailboxes for each migration solution, and we also compared them to uploading a .pst file in Outlook. Here are the results.

| Method | Mailbox size | Item count | Time to migrate | Total RPC transactions | Average client latency (ms) | AvgCasRPCProcessingTime (ms) |
| --- | --- | --- | --- | --- | --- | --- |
| Solution A (mailbox 1) | 376.9 MB | 4,115 | 4:24:33 | 132,040 | 48.4395 | 18.0807 |
| Solution A (mailbox 2) | 249.3 MB | 12,779 | 10:50:50 | 423,188 | 44.1678 | 4.8444 |
| Solution B (mailbox 1) | 618.1 MB | 4,322 | 1:54:58 | 12,196 | 37.2931 | 8.3441 |
| Solution B (mailbox 2) | 56.7 MB | 2,748 | 0:47:08 | 5,806 | 42.1930 | 7.4439 |
| Outlook | 201.9MB | 3,297 | 0:29:47 | 15,775 | 36.9987 | 5.6447 |

Note

The client and service process times are similar, but solution A takes a lot more RPC operations to migrate data. Because each operation consumes client-latency time and server-process time, solution A is much slower to migrate the same amount of data compared to Solution B and to Outlook.

### Factor 4: Network for third-party tool migrations

**Best practice**:

For third-party migration solutions that use the RPC over HTTP Protocol, here's a good way to measure potential migration performance:

1. From the migration server, connect to the Microsoft 365 or Office 365 mailbox with Outlook by using RPC over HTTP Protocol. Make sure that you aren't connecting by using [cached mode](/en-us/outlook/troubleshoot/deployment/cached-exchange-mode).
2. Import a large .pst file with sample data to the Microsoft 365 or Office 365 mailbox.
3. Measure migration performance by timing how long it takes to upload the .pst file. The migration throughput should be similar to what customers can get from a third-party migration tool that uses RPC over HTTP Protocol, given no other constraints. There's overhead during an actual migration, so the throughput might be slightly different.

### Factor 5: Microsoft 365 and Office 365 service

Microsoft 365 and Office 365 resource health-based throttling affects migrations using third-party migration tools. See Microsoft 365 and Office 365 resource health-based throttling for more details.