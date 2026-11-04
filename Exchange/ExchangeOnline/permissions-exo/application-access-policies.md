---
layout: Conceptual
title: Application Access Policies (legacy) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/permissions-exo/application-access-policies
Manager: dansimp
ms.subservice: exo-roles
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.custom:
- has-azure-ad-ps-ref
- azure-ad-ref-level-one-done
description: Learn about how to use Exchange's legacy granular application permissions feature
ms.topic: article
author: Simonv100
ms.author: simonklan
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2023-06-26T00:00:00.0000000Z
locale: en-us
document_id: f4a99046-0c18-4d59-c552-54d9fdf6719d
document_version_independent_id: 298eb23e-0321-4414-5158-b62ece67b66e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/permissions-exo/application-access-policies.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: permissions-exo/application-access-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/permissions-exo/application-access-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 0ad17b43-9dc1-e97c-df60-c59914f82036
---

# Application Access Policies (legacy) | Microsoft Learn

This article will guide you through using Application Access Policies, a legacy feature for scoping application permissions in Exchange which has been replaced by [App RBAC](/en-us/exchange/permissions-exo/application-rbac)

Important

App Access Policies has been replaced by Role Based Access Control for Applications. To learn more, see [Role Based Access Control for Exchange Applications](/en-us/exchange/permissions-exo/application-rbac). New access configuration should not use Application Access Policies since this feature will have deprecation announced in the future which will require migration.

## Limiting application permissions to specific Exchange Online mailboxes using Application Access Policies (legacy)

Administrators who want to limit app access to specific mailboxes can create an application access policy by using the **New-ApplicationAccessPolicy** PowerShell cmdlet. This article covers the basic steps to configure access control. These steps are specific to Exchange Online resources and don't apply to other Microsoft Graph workloads.

## Background

Some apps call Microsoft Graph using their own identity and not on behalf of a user. These apps are usually background services or daemon apps that run on a server without the presence of a signed-in user. These apps make use of [OAuth 2.0 client credentials grant flow](/en-us/azure/active-directory/develop/v2-oauth2-client-creds-grant-flow) to authenticate and are configured with application permissions, which by default enables such apps to access *all* mailboxes in an organization on Exchange Online. For example, the `Mail.Read` application permission allows apps to read mail in all mailboxes without a signed-in user.

Important

By default, apps that have been granted [application permissions](/en-us/graph/permissions-reference) to the following data sets can access all the mailboxes in the organization:

- Calendars
- Contacts
- Mail
- Mailbox settings

Administrators can configure application access policy to limit app access to *specific* mailboxes. There are scenarios where administrators might want to limit an app to only specific mailboxes and *not all* Exchange Online mailboxes in the organization. Administrators can identify the set of mailboxes to permit access by putting them in a mail-enabled security group. Administrators can then limit third-party app access to only that set of mailboxes by creating an application access policy for access to that group.

As further described in the Supported permissions and other resources section, application access policy restricts mailbox access for apps that are granted any of the Microsoft Graph or Exchange Web Services permission scopes that the policy supports.

## Configure ApplicationAccessPolicy

To configure an application access policy and limit the scope of application permissions:

1. Connect to Exchange Online PowerShell. For details, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell?view=exchange-ps&amp;preserve-view=true).
2. Identify the app's client ID and a mail-enabled security group to restrict the app's access to.

    - Identify the app's application (client) ID in the [Microsoft Entra admin center &gt; app registrations page](https://entra.microsoft.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade/).
    - Create a new mail-enabled security group or use an existing one and identify the email address for the group.
3. Create an application access policy.

    Run the following command, replacing the arguments for **AppId**, **PolicyScopeGroupId**, and **Description**.

    ```powershell
    New-ApplicationAccessPolicy -AppId e7e4dbfc-046f-4074-9b3b-2ae8f144f59b -PolicyScopeGroupId EvenUsers@contoso.com -AccessRight RestrictAccess -Description "Restrict this app to members of distribution group EvenUsers."
    ```
4. Test the newly created application access policy.

    Run the following command, replacing the arguments for **Identity** and **AppId**.

    ```powershell
    Test-ApplicationAccessPolicy -Identity user1@contoso.com -AppId e7e4dbfc-046f-4074-9b3b-2ae8f144f59b
    ```

    The output of this command indicates whether the app has access to User1's mailbox.

Note

Changes to application access policies can take longer than 1 hour to take effect in Microsoft Graph REST API calls, even when `Test-ApplicationAccessPolicy` shows positive results.

## Supported permissions and other resources

Administrators can use ApplicationAccessPolicy cmdlets to control mailbox access of an app that is granted any of the following Microsoft Graph application permissions or Exchange Web Services permissions.

Microsoft Graph application permissions:

- `Mail.Read`
- `Mail.ReadBasic`
- `Mail.ReadBasic.All`
- `Mail.ReadWrite`
- `Mail.Send`
- `MailboxSettings.Read`
- `MailboxSettings.ReadWrite`
- `Calendars.Read`
- `Calendars.ReadWrite`
- `Contacts.Read`
- `Contacts.ReadWrite`

Exchange Web Services permission scope: `full_access_as_app`.

For more information about configuring application access policy, see the [PowerShell cmdlet reference for New-ApplicationAccessPolicy](/en-us/powershell/module/exchangepowershell/new-applicationaccesspolicy?view=exchange-ps&amp;preserve-view=true).

## Handling API errors

You might encounter the following error when an API call is denied access due to a configured application access policy.

```json
{
    "error": {
        "code": "ErrorAccessDenied",
        "message": "Access to OData is disabled.",
        "innerError": {
            "request-id": "2f038156-cf40-403d-8e46-831fe42a8229",
            "date": "2019-05-24T10:16:21"
        }
    }
}
```

If the Microsoft Graph API calls from your app return this error, work with the Exchange Online administrator for the organization to ensure that your app has permission to access the mailbox resource.