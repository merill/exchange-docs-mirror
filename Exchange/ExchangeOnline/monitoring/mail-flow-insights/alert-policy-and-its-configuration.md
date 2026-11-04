---
layout: Conceptual
title: Alert policies in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-insights/alert-policy-and-its-configuration
Manager: dansimp
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords: 
ms.author: serdars
author: v-smandalika
audience: ITPro
ms.topic: how-to
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
description: This alert policy allows you to track and manage your activities.
ms.custom: 
ms.date: 2021-07-05T00:00:00.0000000Z
locale: en-us
document_id: 1e441f38-8a36-7e4d-2729-647064dc906a
document_version_independent_id: 6e2fc705-0baf-b2be-aba3-97cbbf3cb0ea
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-insights/alert-policy-and-its-configuration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-insights/alert-policy-and-its-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-insights/alert-policy-and-its-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 3f69127d-2074-10a6-48f3-a250b764dd57
---

# Alert policies in Exchange Online | Microsoft Learn

Alert policies in the new Exchange admin center (EAC) allow you to track events related to mail flow. They can be created when your organization has fulfilled the Licensing requirements.

Additionally, certain permissions are required for creating, viewing and managing alert policies. For more information, see:

- Permissions associated with alert policies
- *RBAC permissions required to view alerts* section in [Alert policies in Microsoft 365](/en-us/purview/alert-policies#rbac-permissions-required-to-view-alerts)

## Licensing requirements

The alert policies in the new EAC support aggregated alert configurations only. To configure aggregate alert policies based on a threshold, you must have one of the following license configurations:

- E5/G5 subscription
- E1/F1/G1 or E3/G3 subscription that includes one of the following features:

    i. Office 365 Advanced Threat Protection Plan 2

    ii. Microsoft 365 E5 Compliance

    iii. Microsoft 365 eDiscovery and Audit add-on license

## Types of alert policies

There are two types of alert policies on the **Alert policies** page, namely System and Custom.

### System policy

System policy is created by the system, by default, hence, it is also referred to as "default alert policy".

#### Characteristics of a system policy

A system alert policy is one that is:

- Marked in bold
- Labeled as **System** under **Policy type**
- Available for viewing by an admin

#### User tasks on system policies

The user can perform the following tasks on a system policy:

- Turn it off (by default, it is turned on)
- Choose a list of recipients and group them as the recipients entitled to receive email notifications of an alert
- Set the daily notification limit for the list of recipients

### Custom policy

Custom policy is the policy that can be created by the admin.

## Permissions associated with alert policies

To create alert policies you have to be assigned the Manage Alerts or Organization Configuration role in the Microsoft Purview portal or Defender portal. You can assign View-Only Manage Alerts role for viewing alert policies.

The following management role groups are associated with alert policies:

- **Security administrator**: This management role group allows admins to create and manage alert policies.

Note

Managing alert policies involve a list of tasks. For more information, see User tasks on alert policies.

- **Security reader**: This management role group allows admins to only read/view an alert policy.

## User tasks on custom policies

A user with **security administrator** privileges can perform the following tasks on an alert policy:

- **Creation**: A user with **security administrator** privileges can create an alert policy, which is a custom alert policy. For information on how to create an alert policy, see Create custom policy.
- **Disable**: A user can disable both the **system** and **custom** policies. For more information, see Disable alert policy.
- **Disable email notifications of alert policies**: A user can disable the email notifications pertaining to both **system** and **custom** policies. For more information, see Disable email notifications.
- **View**: A user can view alert policies (system or custom) on the **Alerts** screen. For more information, see View/read alert policy.

### Create custom policy

To create an alert policy, perform the following steps:

1. Open the [Exchange Admin Center](https://admin.exchange.microsoft.com).
2. In the left pane, select **Mail flow &gt; Alert policies**, and click **New alert policy**.
3. Provide a name for your policy in the **Name** box and click **Next**.

    Note

    Entering a description for the policy in the **Description** box is optional.
4. From the **Severity** drop-down list, select the severity level.

    Note

    The **Category** drop-down list is disabled because **Mail flow** is the only category supported in the new EAC.
5. From the **Trigger an alert when the following insight is generated** drop-down list, select one from the following types of insights:

    - Mail loop
    - Slow transport rule
    - New users forwarding
    - New domains being forwarded
    - Cert expiry
6. Click **Next**.
7. Provide the name or email address of the alert notification recipients in the **Email recipients** box.
8. From the **Daily notification limit** drop-down list, select daily notification count.

    Note

    Choosing the daily-notification count value is optional.
9. Click **Next**.
10. Review the alert-policy settings and click **Create**. The alert policy is created.

### Disable alert policy

To disable an alert policy, perform the following steps:

1. In the left navigation pane of the new EAC, select **Mail flow** &gt; **Alert policies**. The **Alert policies** screen appears.
2. Select the alert policy you want to disable and click on it.

    ![The screen on which you select an alert policy to disable it.](../../exchangeonline/media/selecting-an-alert-policy-to-disable.png)

    The alert policy details screen appears.
3. Uncheck the **Enable this policy** check box.

    ![The screen on which you disable an alert policy by unchecking the check box.](../../exchangeonline/media/disabling-alert-policy.png)
4. Click **Save**. The alert policy is disabled. The user will no longer receive any email notifications pertaining to this alert policy.

### Disable email notifications

A user has the option of disabling just the email notifications pertaining to an alert policy. This disabling results in non-receipt of email notifications of the alert policy. However, the details of the alert policy can continue to be viewed on the **Alerts** screen.

To disable the email notifications of an alert policy, perform the following steps:

1. In the left navigation pane of the new EAC, select **Mail flow** &gt; **Alert policies**. The **Alert policies** screen appears.
2. Select the alert policy for which you to disable email notifications.

    ![The screen on which you select an alert policy for which email notifications are to be disabled.](../../exchangeonline/media/selecting-an-alert-policy-to-disable.png)

    The alert policy details screen appears.
3. Click the **Settings** tab.
4. Uncheck the **Send email notifications** check box.

    ![The screen on which the email notifications for an alert policy are disabled.](../../exchangeonline/media/disabling-email-notifications.png)

    The email notifications for the alert policy are disabled, and the user will no longer receive email notifications pertaining to the alert policy.

### View/read alert policy

To view alerts generated by alert policies, perform the below steps:

1. Open the [Exchange Admin Center](https://admin.exchange.microsoft.com).
2. In the left pane, select **Mail flow &gt; Alerts**. The **Alerts** screen appears, displaying alerts generated by the alert policies created.
3. Under the **Alert name** column, click the alert for which you want to view the details. Details will be displayed on the screen.