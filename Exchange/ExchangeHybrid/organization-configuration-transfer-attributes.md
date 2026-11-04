---
layout: Conceptual
title: Organization Configuration Transfer Attributes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/organization-configuration-transfer-attributes
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
ms.reviewer: 
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: reference
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- M365-email-calendar
ms.assetid: 696bddbc-d86b-4f43-8dc5-bf3d1f10a02c
description: The following attributes can be copied from an on-premises Exchange organization to Exchange Online when the Organization Configuration Transfer option is selected in the Hybrid Configuration wizard.
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 0ec1d7a5-d43c-aeb4-8f92-35c2c2f326b2
document_version_independent_id: fd02d3b6-99f0-c264-78a5-c2231d588531
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/organization-configuration-transfer-attributes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: organization-configuration-transfer-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/organization-configuration-transfer-attributes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 20bae45e-9a73-d82c-7406-620805c1afc4
---

# Organization Configuration Transfer Attributes | Microsoft Learn

The following attributes can be copied from an on-premises Exchange organization to Exchange Online when the Organization Configuration Transfer option is selected in the Hybrid Configuration wizard.

## OWA Mailbox Policy

| OWAMailboxPolicy | Available In |
| --- | --- |
| ActionForUnknownFileAndMIMETypes | Exchange 2010, 2013, 2016 |
| ActiveSyncIntegrationEnabled | Exchange 2010, 2013, 2016 |
| AllAddressListsEnabled | Exchange 2010, 2013, 2016 |
| AllowCopyContactsToDeviceAddressBook | Exchange 2013, 2016 |
| AllowedFileTypes | Exchange 2010, 2013, 2016 |
| AllowedMimeTypes | Exchange 2010, 2013, 2016 |
| AllowOfflineOn | Exchange 2013, 2016 |
| BlockedFileTypes | Exchange 2010, 2013, 2016 |
| BlockedMimeTypes | Exchange 2010, 2013, 2016 |
| CalendarEnabled | Exchange 2010, 2013, 2016 |
| ClassicAttachmentsEnabled | Exchange 2016 |
| ContactsEnabled | Exchange 2010, 2013, 2016 |
| DefaultTheme | Exchange 2010, 2013, 2016 |
| DelegateAccessEnabled | Exchange 2010, 2013, 2016 |
| DirectFileAccessOnPrivateComputersEnabled | Exchange 2010, 2013, 2016 |
| DirectFileAccessOnPublicComputersEnabled | Exchange 2010, 2013, 2016 |
| DisplayPhotosEnabled | Exchange 2013, 2016 |
| ExplicitLogonEnabled | Exchange 2010, 2013, 2016 |
| ForceSaveAttachmentFilteringEnabled | Exchange 2010, 2013, 2016 |
| ForceSaveFileTypes | Exchange 2010, 2013, 2016 |
| ForceSaveMimeTypes | Exchange 2010, 2013, 2016 |
| ForceWacViewingFirstOnPrivateComputers | Exchange 2013, 2016 |
| ForceWacViewingFirstOnPublicComputers | Exchange 2013, 2016 |
| GlobalAddressListEnabled | Exchange 2010, 2013, 2016 |
| Identity | Exchange 2010, 2013, 2016 |
| InstantMessagingEnabled | Exchange 2010, 2013, 2016 |
| InstantMessagingType | Exchange 2010, 2013, 2016 |
| IRMEnabled | Exchange 2010, 2013, 2016 |
| IsDefault | Exchange 2013, 2016 |
| JournalEnabled | Exchange 2010, 2013, 2016 |
| LogonAndErrorLanguage | Exchange 2010, 2013, 2016 |
| Name | Exchange 2010, 2013, 2016 |
| NotesEnabled | Exchange 2010, 2013, 2016 |
| OrganizationEnabled | Exchange 2010, 2013, 2016 |
| OutboundCharset | Exchange 2010, 2013, 2016 |
| OWALightEnabled | Exchange 2010, 2013, 2016 |
| RecoverDeletedItemsEnabled | Exchange 2010, 2013, 2016 |
| ReferenceAttachmentsEnabled | Exchange 2016 |
| RemindersAndNotificationsEnabled | Exchange 2010, 2013, 2016 |
| ReportJunkEmailEnabled | Exchange 2013, 2016 |
| RulesEnabled | Exchange 2010, 2013, 2016 |
| SaveAttachmentsToCloudEnabled | Exchange 2016 |
| SearchFoldersEnabled | Exchange 2010, 2013, 2016 |
| SetPhotoEnabled | Exchange 2013, 2016 |
| SetPhotoURL | Exchange 2013, 2016 |
| SignaturesEnabled | Exchange 2010, 2013, 2016 |
| SpellCheckerEnabled | Exchange 2010, 2013, 2016 |
| TasksEnabled | Exchange 2010, 2013, 2016 |
| TextMessagingEnabled | Exchange 2010, 2013, 2016 |
| ThemeSelectionEnabled | Exchange 2010, 2013, 2016 |
| UMIntegrationEnabled | Exchange 2010, 2013, 2016 |
| UseGB18030 | Exchange 2010, 2013, 2016 |
| UseISO885915 | Exchange 2010, 2013, 2016 |
| WacEditingEnabled | Exchange 2016 |
| WacExternalServicesEnabled | Exchange 2013, 2016 |
| WacOMEXEnabled | Exchange 2013, 2016 |
| WacViewingOnPrivateComputersEnabled | Exchange 2013, 2016 |
| WacViewingOnPublicComputersEnabled | Exchange 2013, 2016 |
| WebPartsFrameOptionsType | Exchange 2013, 2016 |

## Retention Policy

| Retention Policy | Available In |
| --- | --- |
| Identity | Exchange 2010, 2013, 2016 |
| IsDefault | Exchange 2013, 2016 |
| IsDefaultArbitrationMailbox | Exchange 2013, 2016 |
| Name | Exchange 2010, 2013, 2016 |
| RetentionId | Exchange 2010, 2013, 2016 |
| RetentionPolicyTagLinks | Exchange 2010, 2013, 2016 |

## Retention Policy Tags\*\*

| RetentionPolicyTag | Available In |
| --- | --- |
| AgeLimitForRetention | Exchange 2010, 2013, 2016 |
| Comment | Exchange 2010, 2013, 2016 |
| Identity | Exchange 2010, 2013, 2016 |
| LegacyManagedFolder | Exchange 2010, 2013, 2016 |
| LocalizedComment | Exchange 2010, 2013, 2016 |
| LocalizedRetentionPolicyTagName | Exchange 2010, 2013, 2016 |
| MessageClass | Exchange 2010, 2013, 2016 |
| MustDisplayCommentEnabled | Exchange 2010, 2013, 2016 |
| Name | Exchange 2010, 2013, 2016 |
| RetentionAction | Exchange 2010, 2013, 2016 |
| RetentionEnabled | Exchange 2010, 2013, 2016 |
| RetentionId | Exchange 2010, 2013, 2016 |
| SystemTag | Exchange 2010, 2013, 2016 |
| Type | Exchange 2010, 2013, 2016 |
| IsDefaultAutoGroupPolicyTag | Exchange 2013, 2016 |
| IsDefaultModeratedRecipientsPolicyTag | Exchange 2013, 2016 |

### Mobile Device Mailbox Policy

| MobileDeviceMailboxPolicy | Available In |
| --- | --- |
| AllowBluetooth | Exchange 2010, 2013, 2016 |
| AllowBrowser | Exchange 2010, 2013, 2016 |
| AllowCamera | Exchange 2010, 2013, 2016 |
| AllowConsumerEmail | Exchange 2010, 2013, 2016 |
| AllowDesktopSync | Exchange 2010, 2013, 2016 |
| AllowExternalDeviceManagement | Exchange 2010, 2013, 2016 |
| AllowHTMLEmail | Exchange 2010, 2013, 2016 |
| AllowInternetSharing | Exchange 2010, 2013, 2016 |
| AllowIrDA | Exchange 2010, 2013, 2016 |
| AllowMobileOTAUpdate | Exchange 2010, 2013, 2016 |
| AllowNonProvisionableDevices | Exchange 2010, 2013, 2016 |
| AllowPOPIMAPEmail | Exchange 2010, 2013, 2016 |
| AllowRemoteDesktop | Exchange 2010, 2013, 2016 |
| AllowSimplePassword | Exchange 2010, 2013, 2016 |
| AllowSMIMEEncryptionAlgorithmNegotiation | Exchange 2010, 2013, 2016 |
| AllowSMIMESoftCerts | Exchange 2010, 2013, 2016 |
| AllowStorageCard | Exchange 2010, 2013, 2016 |
| AllowTextMessaging | Exchange 2010, 2013, 2016 |
| AllowUnsignedApplications | Exchange 2010, 2013, 2016 |
| AllowUnsignedInstallationPackages | Exchange 2010, 2013, 2016 |
| AllowWiFi | Exchange 2010, 2013, 2016 |
| AlphanumericPasswordRequired | Exchange 2010, 2013, 2016 |
| ApprovedApplicationList | Exchange 2010, 2013, 2016 |
| AttachmentsEnabled | Exchange 2010, 2013, 2016 |
| DeviceEncryptionEnabled | Exchange 2010, 2013, 2016 |
| DevicePolicyRefreshInterval | Exchange 2010, 2013, 2016 |
| Identity | Exchange 2010, 2013, 2016 |
| IrmEnabled | Exchange 2010, 2013, 2016 |
| IsDefault | Exchange 2010, 2013, 2016 |
| MaxAttachmentSize | Exchange 2010, 2013, 2016 |
| MaxCalendarAgeFilter | Exchange 2010, 2013, 2016 |
| MaxEmailAgeFilter | Exchange 2010, 2013, 2016 |
| MaxEmailBodyTruncationSize | Exchange 2010, 2013, 2016 |
| MaxEmailHTMLBodyTruncationSize | Exchange 2010, 2013, 2016 |
| MaxInactivityTimeLock | Exchange 2010, 2013, 2016 |
| MaxPasswordFailedAttempts | Exchange 2010, 2013, 2016 |
| MinPasswordComplexCharacters | Exchange 2010, 2013, 2016 |
| MinPasswordLength | Exchange 2010, 2013, 2016 |
| Name | Exchange 2010, 2013, 2016 |
| PasswordEnabled | Exchange 2010, 2013, 2016 |
| PasswordExpiration | Exchange 2010, 2013, 2016 |
| PasswordHistory | Exchange 2010, 2013, 2016 |
| PasswordRecoveryEnabled | Exchange 2010, 2013, 2016 |
| RequireDeviceEncryption | Exchange 2010, 2013, 2016 |
| RequireEncryptedSMIMEMessages | Exchange 2010, 2013, 2016 |
| RequireEncryptionSMIMEAlgorithm | Exchange 2010, 2013, 2016 |
| RequireManualSyncWhenRoaming | Exchange 2010, 2013, 2016 |
| RequireSignedSMIMEAlgorithm | Exchange 2010, 2013, 2016 |
| RequireSignedSMIMEMessages | Exchange 2010, 2013, 2016 |
| RequireStorageCardEncryption | Exchange 2010, 2013, 2016 |
| UnapprovedInROMApplicationList | Exchange 2010, 2013, 2016 |
| UNCAccessEnabled | Exchange 2010, 2013, 2016 |
| WSSAccessEnabled | Exchange 2010, 2013, 2016 |

## Active Sync Mailbox Policy\*\*

| ActiveSyncMailboxPolicy | Available In |
| --- | --- |
| AllowApplePushNotifications | Exchange 2013, 2016 |
| AllowBluetooth | Exchange 2010, 2013, 2016 |
| AllowBrowser | Exchange 2010, 2013, 2016 |
| AllowCamera | Exchange 2010, 2013, 2016 |
| AllowConsumerEmail | Exchange 2010, 2013, 2016 |
| AllowDesktopSync | Exchange 2010, 2013, 2016 |
| AllowExternalDeviceManagement | Exchange 2010, 2013, 2016 |
| AllowHTMLEmail | Exchange 2010, 2013, 2016 |
| AllowInternetSharing | Exchange 2010, 2013, 2016 |
| AllowIrDA | Exchange 2010, 2013, 2016 |
| AllowMobileOTAUpdate | Exchange 2010, 2013, 2016 |
| AllowNonProvisionableDevices | Exchange 2010, 2013, 2016 |
| AllowPOPIMAPEmail | Exchange 2010, 2013, 2016 |
| AllowRemoteDesktop | Exchange 2010, 2013, 2016 |
| AllowSimpleDevicePassword | Exchange 2010, 2013, 2016 |
| AllowSMIMEEncryptionAlgorithmNegotiation | Exchange 2010, 2013, 2016 |
| AllowSMIMESoftCerts | Exchange 2010, 2013, 2016 |
| AllowStorageCard | Exchange 2010, 2013, 2016 |
| AllowTextMessaging | Exchange 2010, 2013, 2016 |
| AllowUnsignedApplications | Exchange 2010, 2013, 2016 |
| AllowUnsignedInstallationPackages | Exchange 2010, 2013, 2016 |
| AllowWiFi | Exchange 2010, 2013, 2016 |
| AlphanumericDevicePasswordRequired | Exchange 2010, 2013, 2016 |
| ApprovedApplicationList | Exchange 2010, 2013, 2016 |
| AttachmentsEnabled | Exchange 2010, 2013, 2016 |
| DeviceEncryptionEnabled | Exchange 2010, 2013, 2016 |
| DevicePasswordEnabled | Exchange 2010, 2013, 2016 |
| DevicePasswordExpiration | Exchange 2010, 2013, 2016 |
| DevicePasswordHistory | Exchange 2010, 2013, 2016 |
| DevicePolicyRefreshInterval | Exchange 2010, 2013, 2016 |
| Identity | Exchange 2010, 2013, 2016 |
| IrmEnabled | Exchange 2010, 2013, 2016 |
| IsDefault | Exchange 2013, 2016 |
| IsDefaultPolicy | Exchange 2010, 2013, 2016 |
| MaxAttachmentSize | Exchange 2010, 2013, 2016 |
| MaxCalendarAgeFilter | Exchange 2010, 2013, 2016 |
| MaxDevicePasswordFailedAttempts | Exchange 2010, 2013, 2016 |
| MaxEmailAgeFilter | Exchange 2010, 2013, 2016 |
| MaxEmailBodyTruncationSize | Exchange 2010, 2013, 2016 |
| MaxEmailHTMLBodyTruncationSize | Exchange 2010, 2013, 2016 |
| MaxInactivityTimeDeviceLock | Exchange 2010, 2013, 2016 |
| MinDevicePasswordComplexCharacters | Exchange 2010, 2013, 2016 |
| MinDevicePasswordLength | Exchange 2010, 2013, 2016 |
| Name | Exchange 2010, 2013, 2016 |
| PasswordRecoveryEnabled | Exchange 2010, 2013, 2016 |
| RequireDeviceEncryption | Exchange 2010, 2013, 2016 |
| RequireEncryptedSMIMEMessages | Exchange 2010, 2013, 2016 |
| RequireEncryptionSMIMEAlgorithm | Exchange 2010, 2013, 2016 |
| RequireManualSyncWhenRoaming | Exchange 2010, 2013, 2016 |
| RequireSignedSMIMEAlgorithm | Exchange 2010, 2013, 2016 |
| RequireSignedSMIMEMessages | Exchange 2010, 2013, 2016 |
| RequireStorageCardEncryption | Exchange 2010, 2013, 2016 |
| UnapprovedInROMApplicationList | Exchange 2010, 2013, 2016 |
| UNCAccessEnabled | Exchange 2010, 2013, 2016 |
| WSSAccessEnabled | Exchange 2010, 2013, 2016 |