---
layout: Conceptual
title: Manually migrate Permissions, Delegates, Rooms, Resources, and Tasks | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/manual-migration
Manager: jtremper
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Documentation for admins looking to migrate permissions, delegates, rooms, resources, and tasks from Google Workspace (GWS) to Exchange Online.
author: MicrosoftHeidi
ms.author: heidip
ms.date: 2024-06-15T00:00:00.0000000Z
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: Medium
ms.collection: 
ms.custom: QuickDraft
ms.reviewer: tonymathew
search.appverid: MET150
f1.keywords: 
audience: ITAdmin
locale: en-us
document_id: ace772c9-681a-7fed-8120-99891c02331f
document_version_independent_id: 8685e28f-5ac5-789b-ae71-35bcbeb222a1
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/manual-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/manual-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/manual-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: 97f592fe-b636-9350-39f6-843718bf0184
---

# Manually migrate Permissions, Delegates, Rooms, Resources, and Tasks | Microsoft Learn

This guide is for migration admins who are copying content from Google Workspace Gmail to Microsoft 365 Exchange Online. It explains how to migrate permissions, delegates, rooms, resources, and tasks through cmdlets. The solution is only available for Google's Gmail mailboxes. Currently, there are no plans to migrate similar features from other email/IMAP providers.

## Introduction

The Exchange Online migration team is building 1P solutions to automatically migrate permissions, delegates, rooms, resources, and tasks from Google Workspace (GWS). This feature maps the existing data and settings from the source mailboxes in Google to corresponding entities in the Exchange Online mailbox.

Important

The article references migrations of smaller batches or even single-item migration. Admins can also migrate in one large single batch using the information in this article.

## Rooms and Resources

### Prerequisites for rooms and resources

GWS doesn't expose any API to connect the resource mailbox directly. Exchange Online Migration (or MRS, Mailbox Relocation Services) connects to the users specified in the Gmail endpoint and treats the resource calendar as a shared calendar. This work requires the users specified in the Gmail endpoint to have access permission to the resource calendar. Usually, all users within the organization should have read permission by default.

For the autoprovisioning option, Migration Service (Exchange Online Migration's batching service) reads the resource information from the Admin portal. This work requires the admin to do the following steps for the service account used, in addition to the existing prerequisites required for the existing automated GWS mail migration for Mail, Calendar, and contacts:

1. Enable the Admin SDK API from API Console Portal: https://console.developers.google.com/
2. Add the new scope "https://www.googleapis.com/auth/admin.directory.resource.calendar.readonly" to Domain-wide Delegation from Admin Console: https://admin.google.com/ac/owl/domainwidedelegation

### Onboarding steps for rooms and resources

There are two options for onboarding Google resources/rooms:

#### Option 1 (recommended)

Migration Service does the provisioning automatically for the rooms and resources mailboxes. There are two options for the csv schema.

##### Csv schema 1

- **ResourceId**: The resource ID of the Google resource, which can be found in the Google Admin Console: https://admin.google.com/ac/calendarresources/resources.
- **EmailAddress**: Optional, the email address of the EXO resource mailbox. The Migration Service autogenerates an email address if this information isn't provided. We're using New-Mailbox -Name "resource name" to create a mailbox, which autogenerates an email address for the mailbox.

The admin can download a resource list from the Google Admin Console: https://admin.google.com/ac/calendarresources/resources. The downloaded list contains many fields that aren't needed, so the admin needs to modify the list to just keep the **Resource ID** and remove the space between the two words, it should be **ResourceId** after the removal.

##### Csv schema 2

- **Username**: The email address of the Google resource, which can be found in Google Admin Console: https://admin.google.com/ac/calendarresources/resources.
- **EmailAddress**: Optional, the email address of the EXO resource mailbox. The Migration Service autogenerates an email address if this information isn't provided. We're using New-Mailbox -Name "resource name" to create a mailbox, which autogenerates an email address for the mailbox.

##### The PowerShell command to create the migration batch

`New-MigrationBatch -SourceEndpoint MigGmailEndpoint -Name resourceOnboarding -CSVData $([System.IO.File]::ReadAllBytes("C:\ gmail_rooms_resources.csv")) -GoogleResource`

##### Differences with standard Gmail onboarding

1. There's one new parameter that needs to be specified: `-GoogleResource`. a. GoogleResource indicates that we're migrating only rooms and resources. Regular users aren't migrated; if a regular user email is added to the .csv, the migration for the particular user fails.
2. This job doesn't have switch over because Google doesn't support forwarding email address for resources, so: a. The subdomain in't needed. b. The forwarding email address isn't needed. c. The parameter `TargetDeliveryDomain` isn't needed.

#### Option 2

The admin provisions the **resource** mailboxes by themselves. MRS copies the data within the resources.

##### Csv schema 3

The admin is required to create a file (for example gmail\_rooms\_resources.csv) with two fields:

1. Username: The email address of Google resource, which can be found in Google Admin Console: https://admin.google.com/ac/calendarresources/resources.
2. EmailAddress: The email address of Exchange Online resource mailbox.

An example of the csv file:

`Username,EmailAddress c_1887rgsar65nig0clnmdl856s87j2@resource.calendar.google.com, conf96@mrs.com`

##### PowerShell command to create the migration batch

`New-MigrationBatch -SourceEndpoint MigGmailEndpoint -Name resourceOnboarding -CSVData $([System.IO.File]::ReadAllBytes("C:\ gmail_rooms_resources.csv ")) -GoogleResource -SkipProvisioning`

##### The differences with Gmail onboarding

1. There are two new parameters that need to be specified: `-GoogleResource -SkipProvisioning`. a. GoogleResource indicates that we're only migrating rooms and resources calendar data. Regular users aren't migrated. If a regular user email is added to the .csv, the migration for the particular user fails. b. SkipProvisioning, as the name suggests, indicates that there isn't any auto provisioning.
2. This job doesn't have switch over because Google doesn't support forwarding email address for resources, so: a. The subdomain isn't needed. b. The forwarding email address isn't needed. c. The parameter `TargetDeliveryDomain` isn't needed.

### Rooms and resource properties that are currently supported during provisioning process

Google resources are mapped to EXO resource mailboxes. Google buildings are mapped to EXO DistributionGroups.

| Google resource property | EXO resource mailbox property |
| --- | --- |
| Name | Name |
| Category | ResourceType |
| CONFERENCE\_ROOM | Room |
| Others | Equipment |
| Capacity | Capacity |
| Name | Display Name |
| Floor Section | Floor Label |
| Floor | Floor |
| Building ID | BuildingID |
| Building Name | Building |
| Building RegionCode | CountryOrRegion |
| Building AdministrationArea | State |
| Building Locality | City |
| Building Address | Street |
| Building PostalCode | PostalCode |
| Building Coordinates | GeoCoordinates |

Note

Resource migration is a new feature and wasn't supported in the existing Gmail migration.

### Rooms and resources lifeCycle

We recommend starting resource onboarding before regular (Mail, Calendar, Contact) onboarding, and completing resource onboarding after all the mailboxes in the organization are migrated to EXO. This onboarding order provides a better user experience for the customer.

### Rooms and resources limitations

The coexistence scenario isn't supported because Google doesn't support forwarding email address for resource mailboxes. MRS only supports syncing data from Google to EXO; it doesn't support syncing data from EXO back to Google.

## Permissions and Delegates

Note

As of June 2024, the option to migrate permissions and delegates for calendars is turned off worldwide. You can still migrate permissions and delegates for mailboxes.

### Prerequisites for permissions and delegates

Assign a license to users with permissions and delegates before onboarding, so MRS can find the mailboxes during migration. The users with permissions and delegates and owner mailboxes can migrate together, but you need to ensure that all users (owners and users with permissions and delegates) are assigned a license so MRS can find the mailbox and set permissions to them. Otherwise, MRS marks them as bad items.

Note

The user should be provisioned with a mailbox and license. A mailbox without a license is converted to a mail user, which isn't supported.

### Onboarding steps for permissions and delegates

#### Enable or Disable the feature for permissions and delegates

Mailbox delegates, send as, and calendar permission are supported while onboarding a Gmail mailbox. They're enabled by default, and admins can specify `-SkipDelegates` to skip them while creating migration batches.

Once a new migration batch is started, the `-SkipDelegates` option can't be changed or added later using `Set -MigrationBatch` cmdlets. If the admin wants to change course and change the options, they need to remove the migration batch and create a new one. You can't edit a migration batch in progress.

#### Permission sync behavior

Because applying permissions needs time to take effect, and permission changes don't happen often, MRS copies permissions in both incremental sync and final sync, giving AD enough time to sync the permissions. Because Google doesn't support ICS for permissions, MRS saves the source permissions to persisted sync state after each sync, enabling MRS to detect permission changes in the next round of sync.

For existing permissions on the EXO mailbox, MRS merges the permissions:

1. If the Gmail mailbox applied some permissions for the same user, MRS overrides the permissions during onboarding.
2. If the Gmail mailbox doesn't apply any permissions for the same user, it isn't affected during onboarding, meaning MRS doesn't remove it from EXO.

#### Permission mapping

| Google | EXO |
| --- | --- |
| Delegates | Full access and Send on behalf to |
| Send as | Send as |
| See only free/busy | Can view when I'm busy |
| See all event details | Can view all details |
| Manage changes to events | Edit |
| Manage changes and manage sharing | Edit |

Note

MRS only migrates the permissions that have an accepted status in Google. All other statuses mean it isn't applied successfully in Google. We rely on Google APIs to learn the delegate status.

### Migration lifecycle for permissions and delegates

We recommend that users with permissions and delegates be migrated first among the population. The automated migration of permissions and delegates for mail and calendars is enabled by default during regular migrations from GWS Mails, Calendars, and Contacts. The admin can specify `-SkipDelegates` to skip them while creating migration batches.

### Permissions and delegates limitations

1. If a mailbox or group doesn't exist in the target organization, MRS doesn't migrate the permissions, and MRS reports a bad item.
2. MRS doesn't support copying permissions partially for a single object. An object means a single folder, mailbox security descriptor, or user security descriptor.
    - Example 1: (Mailbox permission - not affecting **SendAs** or any of the calendar permissions, only affecting **Delegate**). For example, your Google account has two delegates: `user1@google.com` and `user2@google.com`. If user2 doesn't exist in the target organization, all the delegates (including user1) aren't copied, but SendAs and calendar permissions aren't affected. This situation is only for Mailbox.
    - Example 2: (for Calendar permissions - Mailbox permissions aren't affected, affects all calendar permissions for that specific calendar of that particular user). Google calendar has two permissions: users `user1@google.com` and `user2@google.com`. If user2 doesn't exist in the target organization, all permissions of this calendar aren't copied, but mailbox and the permissions of other calendars (of the same user) aren't affected. This situation is only for Calendar.

Note

After the admin fixes the issue, a new round of incremental sync can copy the permissions to the target successfully.

## Tasks

### Tasks prerequisites

Migration Service needs to read the resource information from the Admin portal. This work requires the customer to enable the new API:

1. Enable Google Tasks API from API Console Portal: https://console.developers.google.com/.
2. Add the new scope "https://www.googleapis.com/auth/tasks.readonly" to Domain-wide Delegation from Admin Console: https://admin.google.com/ac/owl/domainwidedelegation.

### Onboarding steps for tasks

#### Enable or disable the feature for tasks

Once a new migration batch is started, the `-MigrateTasks` option can't be changed or added later using `Set -MigrationBatch` cmdlets. If the admin wants to change course and change the options, they need to remove the migration batch and create a new one. You can't edit a migration batch in progress.

Customers need to specify `-MigrateTasks` when using `New-MigrationBatch`.

Example:

```powershell
New-MigrationBatch -SourceEndpoint MigGmailEndpoint1 -Name TaskMigrationTest -TimeZone "Pacific Standard Time" -NotificationEmails <zhowa@contoso.com> -CSVData $([System.IO.File]::ReadAllBytes("D:\gmail.csv"))  -autostart -TargetDeliveryDomain "mrs.com" -MigrateTasks  -AutoComplete
```

#### Task migration process

This step happens before the migration batch is completed. Task folders are created, and the tasks are migrated only once. Incremental Sync isn't supported for an already-migrated task.

| Google entities | Exchange entities |
| --- | --- |
| Task list | Task folder |
| Parent task | Task |
| Child task | Task |

| Google task list properties | Exchange task folder properties |
| --- | --- |
| ID | ID |
| Title | Name |

| Google task properties | Exchange task properties |
| --- | --- |
| ID | ID |
| Title | Subject |
| Notes | Body |
| Status | Status |
| DueDate | Due |
| CompletedDate | Completed |

#### Tasks lifecycle

We recommend the automated migration of Tasks along with the migration of mail, calendar, and contacts, with the `-MigrateTasks` parameter.

#### Tasks limitations

1. No instances of repeated tasks are migrated because the existing Google API doesn't provide that information in the API.
2. Task attachments aren't migrated, because Google can't provide that information in the API.
3. Exchange doesn't support task hierarchy. As a result, tasks hierarchy isn't preserved when migrating from GWS to Exchange.
4. Deleted or hidden tasks aren't migrated.
5. Google tasks can be parent tasks or child tasks. Exchange tasks don't support child tasks very well. The tasks hierarchy and parent-child relationship isn't preserved during migration.