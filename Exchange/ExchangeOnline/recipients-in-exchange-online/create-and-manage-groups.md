---
layout: Conceptual
title: Create and manage groups in the Exchange admin center in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/create-and-manage-groups
Manager: Serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: Benny-54
audience: ITPro
ms.reviewer: akprakash
f1.keywords: 
ms.topic: how-to
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: 
ms.collection: 
ms.custom: 
description: Create and manage groups in the Exchange admin center.
ms.date: 2023-10-31T00:00:00.0000000Z
locale: en-us
document_id: c4e662ce-9c12-d268-3a0d-8434895b5453
document_version_independent_id: 6786e7cf-d2ae-efc3-d02f-6c96f5c00a9b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/create-and-manage-groups.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/create-and-manage-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/create-and-manage-groups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 7c33d172-b78b-791a-34b8-87eb9ac55eca
---

# Create and manage groups in the Exchange admin center in Exchange Online | Microsoft Learn

Use the Exchange admin center (EAC) to create, modify, export, or remove groups in your Exchange Online organization.

There are four types of groups that can be used to distribute messages:

- **Microsoft 365 group** (formerly known as Office 365 groups), is used for collaboration between teams, both inside and outside your company; by giving them a group email and a shared workspace for conversations, files, and calendars.

    Note

    **Microsoft 365 group** is the recommended group as it provides the teams a shared workspace to communicate, share files, appointments, emails, contacts and other mailbox items.
- **Distribution list group** is used for sending emails/notifications to a group of people.
- **Dynamic distribution list group** is used to expedite the mass sending of email messages and other information within a Microsoft Exchange organization.
- **Mail-enabled security group** is used for granting access to resources such as OneDrive, SharePoint, and emailing notifications to those users.

For more information see, [groups](/en-us/microsoft-365/admin/create-groups/compare-groups).

## Create a group

1. In the [Exchange admin center](https://admin.exchange.microsoft.com/#/) click **Recipients** &gt; **Groups**.

    The **Groups** page is displayed.
2. Click **Add a group** and follow the instructions in the details pane.

    For more information see, [Create a group](/en-us/microsoft-365/admin/create-groups/create-groups).

    - On the **Finish** tab, in the **Review and finish adding group** details pane, verify all the details, and then click **Create group**.
3. Click **Close**.

For more information see, [Use groups to collaborate effectively](https://support.microsoft.com/office/learn-about-microsoft-365-groups-b565caa1-5c40-40ef-9915-60fdb2d97fa2?WT.mc_id=365AdminCSH&amp;ui=en-US&amp;rs=en-US&amp;ad=US).

## Edit a group

1. From the list view, select the group name that you want to edit.
2. In the details pane, do the following:

    - In the **General** section, you can edit the **Basic information** and the **Email address** of the group.
    - In the **Members** section, you can view, manage, and add **Owners** and **Members** to the group.
    - In the **Settings** section, you can do the following:

        a. For **Microsoft 365 group**, you can edit/check the confirmation boxes in the **General settings**, change the status in **Privacy** settings, and then click **Save** to save the changes.

        b. For **Distribution list group** and **Mail-enabled security group**, you can edit/check the confirmation box to allow external senders to email this group and then click **Advanced Settings** to edit/manage more settings in the **Exchange admin center**.
    - In the **Microsoft Teams** section, you can manage your **Teams** settings in **Microsoft Teams admin center**.

    Note

    **Microsoft Teams** can be added to only a **Microsoft 365 group**. This option is not available for the other groups. To create a team, all group owners must have a license that includes **Teams**.

## Export a group

You can export group details in a .csv file format.

1. Select the group from the list view that you want to export and click **Export groups**.

    The dialog box to confirm the export is displayed.
2. Click **Continue**.

    The .csv format of the group details file is downloaded.

## Naming policy

You can add prefixes and suffixes to your group names.

1. Click **Add naming policy**.
2. In the **Edit group naming policy** details pane, do the following:

    - In the **Policy** section, provide the details.
    - In the **Blocked words** section, add the specific words that you want to block from being used in group names and aliases.
3. Click **Save**.

## Upgrade the Distribution list group

You can upgrade a **Distribution list group** to **Microsoft 365 group**.

1. Select the group from the list view that you want to upgrade and click **Upgrade distribution group**.

    The dialog box to confirm the upgrade is displayed.
2. Click **Upgrade**.

    Note

    The upgrade is a permanent change and can not be reversed.

## Other actions

1. Click **Refresh** to update the list of groups page after adding a group or editing the details of a group.
2. Click **...** to perform the following actions:

    - Click **Edit name and description** to edit the group information.
    - Click **Delete group** to delete the selected group.
3. Select a group, click **...** &gt; **Edit email address** to edit **Primary** and **Aliases** email address.
4. Click **Filter** to filter the groups based on the displayed options in the drop-down list.
5. Enter information in the **Search** box to search a group, group email id, or other details.