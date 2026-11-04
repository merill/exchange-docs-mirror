---
layout: Conceptual
title: Changes to Get-Mailbox and New-Mailbox specifically with the Migration parameter | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/get-new-mailbox-migration
Manager: <manager-alias>
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn about properties being removed from the Migration parameter scenario for Get-Mailbox and New-Mailbox in Exchange Online.
ms.author: adbhale
author: Swatyario
ms.reviewer: <reviewer-alias>
ms.date: 2026-10-15T00:00:00.0000000Z
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: high
locale: en-us
document_id: 682bbae2-5bab-9f2e-fe6b-11dbd544a049
document_version_independent_id: 5e4063db-850e-8d9e-1092-7e20c583358f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/get-new-mailbox-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: get-new-mailbox-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/get-new-mailbox-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: 1259ee89-57a9-d494-565f-9be774c2b24f
---

# Changes to Get-Mailbox and New-Mailbox specifically with the Migration parameter | Microsoft Learn

We're simplifying legacy management scenarios and removing some properties from the `Get-Mailbox` and `New-Mailbox``-Migration` scenario.

## When these changes take effect

Beginning November 15, 2026, selected properties will no longer be returned when you use the `-Migration` switch with the following mailbox cmdlets:

- `Get-Mailbox -Migration`
- `New-Mailbox -Migration`

Beginning December 15, 2026, the affected properties will be blocked from being configured by using:

- `New-Mailbox -Migration`

Review scripts, tools, and other automation that use the `-Migration` switch, and update any dependencies on the affected properties before these dates.

## Affected properties

| Category | Properties |
| --- | --- |
| Custom attributes | `CustomAttribute1`-`CustomAttribute13`, `ExtensionCustomAttribute1`-`ExtensionCustomAttribute5` |
| Delivery and moderation | `AcceptMessagesOnlyFrom`, `AcceptMessagesOnlyFromDLMembers`, `AcceptMessagesOnlyFromSendersOrMembers`, `AcceptMessagesOnlyFromWithDisplayNames`, `AcceptMessagesOnlyFromSendersOrMembersWithDisplayNames`, `AcceptMessagesOnlyFromDLMembersWithDisplayNames`, `RejectMessagesFrom`, `RejectMessagesFromDLMembers`, `RejectMessagesFromSendersOrMembers`, `BypassModerationFromSendersOrMembers`, `ModeratedBy`, `ModerationEnabled`, `SendModerationNotifications`, `GrantSendOnBehalfTo`, `GrantSendOnBehalfToWithDisplayNames`, `RequireSenderAuthenticationEnabled`, `DeliverToMailboxAndForward`, `ForwardingAddress`, `ForwardingAddressWithDisplayNames`, `ForwardingSmtpAddress`, `MessageCopyForSentAsEnabled`, `MessageCopyForSendOnBehalfEnabled`, `MessageCopyForSMTPClientSubmissionEnabled`, `DowngradeHighPriorityMessagesEnabled`, `MessageRecallProcessingEnabled` |
| Database and store | `MailboxContainerGuid`, `UnifiedMailbox`, `AggregatedMailboxGuids`, `DisabledMailboxLocations`, `ServerName`, `ServerLegacyDN`, `MailboxProvisioningConstraint`, `MailboxProvisioningPreferences`, `UseDatabaseQuotaDefaults` |
| Archive | `ArchiveDatabase`, `ArchiveDatabaseGuid`, `ArchiveGuid`, `ArchiveName`, `ArchiveQuota`, `ArchiveWarningQuota`, `ArchiveDomain`, `ArchiveStatus`, `ArchiveState`, `ArchiveRelease`, `AutoExpandingArchiveEnabled`, `AutoArchivingEnabled`, `JournalArchiveAddress`, `DisabledArchiveDatabase`, `DisabledArchiveGuid` |
| Point-in-time restore, backup, and soft delete | `PitrEnabled`, `PitrCopyIntervalInSeconds`, `PitrPaused`, `PitrPausedTimestamp`, `PitrOffboardedTimestamp`, `PitrState`, `M365BackupState`, `WasInactiveMailbox`, `IsInactiveMailbox`, `InactiveMailboxRetireTime`, `OrphanSoftDeleteTrackingTime`, `IsSoftDeletedByRemove`, `IsSoftDeletedByDisable`, `WhenSoftDeleted`, `RecipientSoftDeletedStatus`, `IncludeInGarbageCollection`, `RetainDeletedItemsFor`, `SingleItemRecoveryEnabled`, `RetentionPolicy` |
| Quota (non-shard) | `CalendarLoggingQuota`, `RulesQuota`, `RecipientLimits`, `MaxReceiveSize` |
| SCL, antispam, and throttling | `SCLDeleteThreshold`, `SCLDeleteEnabled`, `SCLRejectThreshold`, `SCLRejectEnabled`, `SCLQuarantineThreshold`, `SCLQuarantineEnabled`, `SCLJunkThreshold`, `SCLJunkEnabled`, `AntispamBypassEnabled`, `ThrottlingPolicy`, `RecipientThrottlingThreshold`, `MaxSafeSenders`, `MaxBlockedSenders` |
| Identity and account | `SamAccountName`, `WindowsLiveID`, `MicrosoftOnlineServicesID`, `NetID`, `ReconciliationId`, `SourceAnchor`, `ExternalDirectoryObjectId`, `LinkedMasterAccount`, `AccountDisabled`, `ExchangeUserAccountControl`, `ResetPasswordOnNextLogon`, `StsRefreshTokensValidFrom`, `UsageLocation`, `Office`, `UserIdentityParent`, `AgentIdentityBlueprintId`, `IsAgenticUser`, `IsExchangeCloudManaged`, `IsDirSynced`, `SKUAssigned` |
| Resource, room, and public folder | `IsResource`, `ResourceCapacity`, `ResourceCustom`, `ResourceType`, `RoomMailboxAccountEnabled`, `IsLinked`, `IsShared`, `IsMonitoringMailbox`, `IsPublicFolderSystemMailbox`, `IsRootPublicFolderMailbox`, `DefaultPublicFolderMailbox`, `EffectivePublicFolderMailbox` |
| Policies | `AddressBookPolicy`, `SharingPolicy`, `RemoteAccountPolicy`, `RoleAssignmentPolicy`, `MailboxPlan`, `GeneratedOfflineAddressBooks`, `PoliciesIncluded`, `PoliciesExcluded`, `EmailAddressPolicyEnabled` |
| Audit | `AuditEnabled`, `AuditLogAgeLimit`, `AuditAdmin`, `AuditDelegate`, `AuditOwner`, `DefaultAuditSet` |
| Mailbox move | `MailboxMoveTargetMDB`, `MailboxMoveSourceMDB`, `MailboxMoveFlags`, `MailboxMoveRemoteHostName`, `MailboxMoveBatchName`, `MailboxMoveStatus`, `MailboxRelease`, `RemoteRecipientType` |
| Hierarchy, protocol, and miscellaneous | `IsExcludedFromServingHierarchy`, `IsHierarchyReady`, `IsHierarchySyncEnabled`, `HasSnackyAppData`, `ProtocolSettings`, `IsMailboxEnabled`, `MessageTrackingReadStatusEnabled`, `ExternalOofOptions`, `CalendarRepairDisabled`, `CalendarVersionStoreDisabled`, `ImListMigrationCompleted`, `Languages`, `AdminDisplayVersion`, `ExchangeVersion`, `ExchangeSecurityDescriptor`, `EnforcedTimestamps`, `HttpDeliveryScenario`, `HttpDeliveryEndpoint`, `NonCompliantDevices`, `HasPicture`, `HasSpokenName`, `UserSMimeCertificate`, `UserCertificate`, `IsPersonToPersonTextMessagingEnabled`, `IsMachineToPersonTextMessagingEnabled`, `UMDtmfMap` |
| Shared domain | `SharedEmailDomainTenant`, `SharedEmailDomainState`, `SharedWithTargetSmtpAddress`, `SharedEmailDomainStateLastModified` |
| Directory and Active Directory | `ObjectCategory`, `ObjectClass`, `OrganizationalUnit`, `OrganizationalUnitRoot`, `QueryBaseDN`, `QueryBaseDNRestrictionEnabled`, `AddressListMembership`, `AdministrativeUnits`, `ArbitrationMailbox`, `LastExchangeChangedTime`, `DirectoryObjectVersion`, `OriginatingServer`, `IsValid`, `SimpleDisplayName`, `WindowsEmailAddress`, `EmailAddressDisplayNames`, `MailTip`, `MailTipTranslations`, `SharingAnonymousIdentities` |