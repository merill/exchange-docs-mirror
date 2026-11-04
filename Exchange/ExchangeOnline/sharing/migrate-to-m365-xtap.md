---
layout: Conceptual
title: Migrate to Microsoft 365 Cross-Tenant Access Policy for sharing Free/Busy, Calendars, and MailTips | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/migrate-to-m365-xtap
Manager: dansimp
ms.subservice: outlook-services
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: A step-by-step guide for tenant administrators migrating existing Organization Relationship, Availability Address Space, and Sharing Policy configurations for accessing Free/Busy, Shared Calendars, and MailTips between organizations hosted in Microsoft 365.
ms.date: 2026-10-21T00:00:00.0000000Z
author: alexcotsalas
ms.author: alexcotsalas
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
locale: en-us
document_id: 03fe8101-a4aa-6653-96a9-c6113a694066
document_version_independent_id: 7ddfa0e9-55dc-654f-9ad3-36cf23a40791
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/migrate-to-m365-xtap.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/migrate-to-m365-xtap
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/migrate-to-m365-xtap.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: ea50ae1f-50fb-d234-d743-b64957cf93fb
---

# Migrate to Microsoft 365 Cross-Tenant Access Policy for sharing Free/Busy, Calendars, and MailTips | Microsoft Learn

## Overview

Microsoft 365 Cross-Tenant Access Policy is the new Microsoft standard for collaboration between Microsoft 365 tenants and replaces Organization Relationship and Sharing Policies for sharing Free/Busy, Calendars, and MailTips between organizations hosted in Microsoft 365. This guide provides step-by-step instructions for completing the migration: understand your current configurations, set up new Cross-Tenant Access Policies, test functionality, and lastly clean up old configurations.

## Why Migrate?

Sharing Free/Busy, Calendars, and MailTips with another Exchange organization via Organization Relationship or Sharing Policy relies on Exchange Web Services (EWS) which is being deprecated in Exchange Online and High-Privilege Access which is being migrated to modern authentication technology. As part of this effort, all Microsoft products — including Outlook, Teams, and Dynamics 365 — are removing their EWS dependencies and moving away from High-Privilege Access patterns. Migrating to Microsoft 365 Cross-Tenant Access Policy ensures your existing scenarios continue to work and moves your organization to a stronger security posture. For more context, see:

- [Exchange Online EWS, Your Time is Almost Up](https://techcommunity.microsoft.com/blog/Exchange/exchange-online-ews-your-time-is-almost-up/4492361)
- [Deprecation of EWS in Exchange Online](/en-us/exchange/clients-and-mobile-in-exchange-online/deprecation-of-ews-exchange-online)
- [Enhancing Microsoft 365 security by eliminating high-privilege access](https://www.microsoft.com/security/blog/2025/07/08/enhancing-microsoft-365-security-by-eliminating-high-privilege-access/)

Important

Microsoft 365 Cross-Tenant Access Policies for managing Free/Busy, Shared Calendar, and MailTips is rolling out and may not have reached your tenant yet. Check Message Center and [the post in the Exchange Blog](https://techcommunity.microsoft.com/blog/exchange/cross-tenant-freebusy-mailtips-and-calendar-sharing-are-moving-to-cross-tenant-a/4545169) for the latest rollout information. Plan to migrate after the rollout reaches your tenant and before EWS deprecation.

## Part 1 – Understand your current configurations

Before making any changes, create an inventory of existing configurations that need to be migrated. You’ll use this inventory in Part 2 to set up the equivalent Microsoft 365 Cross-Tenant Access Policy.

Note

The following steps require connecting to Exchange Online PowerShell with an account assigned the Organization Management role. For more information, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

### Review your Organization Relationship configurations

Organization Relationship configurations allow organizations to share Free/Busy or MailTips information, with granular controls for access levels and scopes. Use the following steps to understand your existing configurations and decide which ones to migrate to Cross-Tenant Access Policies.

1. From Exchange Online PowerShell, run the following command to view all configured Organization Relationships:

    ```PowerShell
    Get-OrganizationRelationship | Format-List Name, DomainNames, Enabled, FreeBusyAccessEnabled, FreeBusyAccessLevel, FreeBusyAccessScope, MailTipsAccessEnabled, MailTipsAccessLevel, MailTipsAccessScope, TargetSharingEpr, TargetAutodiscoverEpr, TargetApplicationUri
    ```

    Tip

    If you have many Organization Relationships or configurations with many domains, use these commands instead to filter out disabled relationships and show all domains.

    ```PowerShell
    $FormatEnumerationLimit = -1
    Get-OrganizationRelationship | Where-Object { $_.Enabled -eq $True } | Format-List Name, DomainNames, Enabled, FreeBusyAccessEnabled, FreeBusyAccessLevel, FreeBusyAccessScope, MailTipsAccessEnabled, MailTipsAccessLevel, MailTipsAccessScope, TargetSharingEpr, TargetAutodiscoverEpr, TargetApplicationUri
    ```
2. Review the output. If nothing is returned, you have no Organization Relationships configured and can move on to review your Availability Address Space configurations. For each configured Organization Relationship, review the following values to understand how Free/Busy and MailTips sharing is configured.

    | Parameter | Description |
    | --- | --- |
    | ***Name*** | A unique name for the Organization Relationship. |
    | ***DomainNames*** | The SMTP domain(s) of the external organization. |
    | ***Enabled*** | Whether this Organization Relationship is enabled. If this value is False, the entire Organization Relationship is disabled and isn't functional for sharing Free/Busy or MailTips, regardless of FreeBusyAccessEnabled and MailTipsAccessEnabled values. |
    | ***FreeBusyAccessEnabled*** | Specifies if this Organization Relationship can be used to access Free/Busy information in the external organization. If this value is False, this Organization Relationship isn't functional for retrieving Free/Busy information from the external organization. |
    | ***FreeBusyAccessLevel*** | Specifies the maximum amount of detail returned to the requesting organization. Valid values are None: no free/busy access, AvailabilityOnly: free/busy access with time only, and LimitedDetails: free/busy access with time, subject, and location. |
    | ***FreeBusyAccessScope*** | Specifies the scope of this Organization Relationship for sharing Free/Busy with the external organization. If this value is set, users in the external organization can only retrieve Free/Busy information from members of this group. |
    | ***MailTipsAccessEnabled*** | Specifies if this Organization Relationship can be used by the external organization to access MailTips information for users in this organization. |
    | ***MailTipsAccessLevel*** | Specifies the amount of detail returned to the requesting organization. Valid values are None: no MailTips access, Limited: only MailTips that could prevent a non-delivery report (NDR) or Auto Reply are returned, and All: all MailTips are returned, including Auto Reply, Custom MailTips, Large Audience MailTip, and more. |
    | ***MailTipsAccessScope*** | Specifies the scope of this Organization Relationship for sharing MailTips with the external organization. If this value is set, users in the external organization can only retrieve MailTips information from members of this group. |
    | ***TargetSharingEpr*** | Specifies the URL of Exchange Web Services for the external organization. If this value contains outlook.com, office365.com, or office365.us then the external organization is hosted in Microsoft 365. Other values may indicate the external organization is running on-premises Exchange. |
    | ***TargetAutodiscoverEpr*** | Specifies the URL of Autodiscover for the external organization. This value is only used if TargetSharingEpr is not set. If this value contains outlook.com, office365.com, or office365.us then the external organization is hosted in Microsoft 365. Other values may indicate the external organization is running on-premises Exchange. |
    | ***TargetApplicationUri*** | Specifies the URI of the external organization. If this value contains outlook.com or office365.us then the external organization is hosted in Microsoft 365. Other values may indicate the external organization is running on-premises Exchange. |
3. For each Organization Relationship that configures Free/Busy or MailTips sharing, confirm that the external organization is hosted in Microsoft 365 and has a corresponding Organization Relationship configured. If so, migrate the configuration to Microsoft 365 Cross-Tenant Access Policies.

Tip

If you are using the same Organization Relationship to configure additional features (for example, cross-tenant mailbox migration), you'll need to move these configurations to a new Organization Relationship before completing the migration for Free/Busy or MailTips.

### Review your Availability Address Space configurations

Availability Address Space configurations allow organizations to share Free/Busy information. Use the following steps to understand your existing configurations and decide which ones to migrate to Cross-Tenant Access Policies. Sharing Free/Busy with another organization hosted in Microsoft 365 via Availability Address Space does not depend on Exchange Web Services and is not impacted by EWS deprecation. However, you may still wish to migrate these configurations to Microsoft 365 Cross-Tenant Access Policy, which supports additional security features and more granular configuration options.

1. From Exchange Online PowerShell, run the following command to view all Availability Address Space configurations:

    ```PowerShell
    Get-AvailabilityAddressSpace | Format-List ForestName, AccessMethod, TargetAutodiscoverEpr, TargetServiceEpr, TargetTenantId
    ```
2. Review the output. If nothing is returned, you have no Availability Address Space configurations and can move on to review your Sharing Policy configurations. For each configured Availability Address Space, review the following values to understand how Free/Busy sharing is configured.

    | Parameter | Description |
    | --- | --- |
    | ***ForestName*** | The SMTP domain of the external organization. |
    | ***AccessMethod*** | Specifies authentication used to access free/busy information from the external organization. Only OrgWideFBToken is functional for sharing free/busy information between two Exchange Online tenants. If this parameter is any other value, you can't migrate the Availability Address Space to Microsoft 365 Cross-Tenant Access Policy. |
    | ***TargetAutodiscoverEpr*** | Specifies the URL of Autodiscover for the external organization. If this value contains outlook.com, outlook.cn, office365.com, or office365.us then the external organization is hosted in Microsoft 365. Other values may indicate the external organization is running on-premises Exchange. |
    | ***TargetServiceEpr*** | Specifies the Exchange Online address for the external organization and is required when using the OrgWideFBToken AccessMethod. If this value contains outlook.com, outlook.cn, office365.com, or office365.us then the external organization is hosted in Microsoft 365. |
    | ***TargetTenantId*** | Specifies the tenant ID for the external organization and is required when using the OrgWideFBToken AccessMethod. |
3. For each Availability Address Space configuration that uses AccessMethod OrgWideFBToken, consider migrating the configuration to Microsoft 365 Cross-Tenant Access Policies, which supports additional security features and more granular configuration options.

### Review your Sharing Policy configurations

Sharing Policy configurations control how your users share their calendars with people in other organizations. Use the following steps to understand your existing configurations and decide which ones to migrate to Cross-Tenant Access Policies.

1. From Exchange Online PowerShell, run the following command to view all Sharing Policies:

    ```PowerShell
    Get-SharingPolicy | Format-List Name, Enabled, Domains, Default
    ```
2. Review the output. If nothing is returned, you have no Sharing Policies configured. For each configured Sharing Policy, review the following values:

    | Parameter | Description |
    | --- | --- |
    | ***Name*** | A unique name for the Sharing Policy |
    | ***Enabled*** | Whether this Sharing Policy is enabled. If this value is False, the policy isn't functional for external calendar sharing. |
    | ***Domains*** | Describes the calendar sharing allowed with external domains. Contains one or more comma-separated entries in the format ***&lt;domain&gt;:&lt;access level&gt;***. A wildcard \* domain applies to all external organizations. An Anonymous entry controls calendar publishing to anonymous internet recipients via a published URL. The access level controls what external users in the domain can see:<br><br> Access level | What external users can see |    | CalendarSharingFreeBusySimple | Free/busy — time only |<br>    | CalendarSharingFreeBusyDetail | Free/busy — time, subject, and location |<br>    | CalendarSharingFreeBusyReviewer | Full calendar details | |
    | --- | --- |
    | ***Default*** | Whether this is the default policy applied to mailboxes that aren't explicitly assigned another policy. |
3. Run the following command to understand which sharing policies are assigned to mailboxes:

    ```PowerShell
    Get-EXOMailbox -ResultSize Unlimited -RecipientTypeDetails UserMailbox,SharedMailbox -Properties SharingPolicy | Group-Object SharingPolicy | Select-Object Name, Count
    ```
4. For each enabled Sharing Policy assigned to mailboxes, confirm that the external organization is hosted in Microsoft 365. If it is, migrate the configuration to Microsoft 365 Cross-Tenant Access Policies.

Important

Microsoft 365 Cross-Tenant Access Policy applies only to organizations hosted in Microsoft 365. If your organization is hybrid, or shares calendars or Free/Busy with organizations running on-premises Exchange, keep the existing Sharing Policies enabled. The new policy can't replace them, so disabling or removing them stops sharing with those organizations.

## Part 2 – Configure your new Microsoft 365 Cross-Tenant Access Policies

For each existing configuration for sharing Free/Busy, MailTips, or Calendar Sharing information, follow the steps in this section to create the corresponding Microsoft 365 Cross-Tenant Access Policy.

Important

Microsoft 365 Cross-Tenant Access Policy is an **inbound** setting. Each organization controls whether Free/Busy, MailTips, and Calendar Sharing information can be accessed by external users via the policy. For bidirectional sharing, **both** organizations must create complementary Microsoft 365 Cross-Tenant Access Policies.

### Prerequisites

Before continuing, ensure you have the following:

- Global Administrator privileges for your tenant
- The unique Microsoft Entra Tenant ID of the external organization. An administrator for the external organization can find this ID in their [Azure Portal under Microsoft Entra ID](/en-us/azure/azure-portal/get-subscription-tenant-id#find-your-microsoft-entra-tenant).
- [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation) installed
- For bidirectional sharing, ensure an administrator in the external organization is also migrating to Microsoft 365 Cross-Tenant Access Policy.

### Check your Entra Cross-Tenant Access Policy Trust Relationship

Microsoft 365 Cross-Tenant Access Policy builds on Entra Cross-Tenant Access Policy. Before sharing Free/Busy, Calendars, or MailTips using Microsoft 365 Cross-Tenant Access Policy, follow the steps in this section to enable the Microsoft 365 Collaboration trust level in Entra Cross-Tenant Access Policy for each external organization. In this guide, you enable the Microsoft 365 Collaboration trust level for all users in your organization. You can define narrower scopes in later steps to control effective access. Applying narrower scopes at the Microsoft 365 Collaboration trust level is supported but not covered in this guide. For more information, review the Microsoft 365 Cross-Tenant Access Policies documentation.

Note

Complete this step once for each external organization you want to share Free/Busy, Calendars, or MailTips with. Unlike previous configuration types, you don't need to add the external organization domain names in the configuration. Instead, use the Tenant ID to uniquely identify the external organization. All domain names are automatically included in the relationship.

1. Connect Microsoft Graph PowerShell SDK with the required scopes:

    ```PowerShell
    Connect-MgGraph -Scopes "Policy.Read.All,Policy.ReadWrite.CrossTenantAccess,Policy.ReadWrite.CrossTenantCapability" -ContextScope Process
    ```
2. For each external organization identified in Part 1, enable Microsoft 365 Collaboration trust by running the following commands:

    ```PowerShell
    $partnerId = "<partnerTenantId>"
    $body = @{
      tenantId = $partnerId
      m365CollaborationInbound = @{
        users = @{
          accessType = "allowed"
          targets = @(
              @{ target = "AllUsers"; targetType = "user" }
          )
        }
      }
    }
    
    New-MgPolicyCrossTenantAccessPolicyPartner -BodyParameter $body
    ```

### Create Microsoft 365 Cross-Tenant Access Policies for Free/Busy

For each existing Free/Busy configuration from Part 1, create the corresponding Microsoft 365 Cross-Tenant Access Policy. You need the following information:

- The unique Microsoft Entra Tenant ID of the external organization. An administrator for the external organization can find this ID in their [Azure Portal under Microsoft Entra ID](/en-us/azure/azure-portal/get-subscription-tenant-id#find-your-microsoft-entra-tenant).
- The correct capability for the desired Free/Busy access. Use the following table to determine the correct capability:

    | Capability | Effective Access | Replaces |
    | --- | --- | --- |
    | ***crossTenantCalendarAvailabilityBasic*** | Allows access to Free/Busy with Time information only. | Organization Relationships with FreeBusyAccessLevel set to AvailabilityOnly or Availability Address Spaces |
    | ***crossTenantCalendarAvailabilityLimitedDetails*** | Allows access to Free/Busy with Time, Subject, and Location information. | Organization Relationships with FreeBusyAccessLevel set to Limited Details |
- Optionally, a security group containing internal users whose Free/Busy information the external organization can retrieve. When you provide this group, users in the external organization can only retrieve Free/Busy information from internal users in this group.

Tip

While Global Admin privileges are required to create the Entra Cross-Tenant Access Policy Trust Relationship, you can use either Global Admin or Exchange Admin privileges to configure the Microsoft 365 Cross-Tenant Access Policies for Free/Busy.

1. For each Free/Busy sharing configuration identified in Part 1, enable the corresponding capability in the partner policy:

    ```PowerShell
    $partnerId = "<partnerTenantId>"
    $capability = "<capabilityName>"
    ```

    If you're using a security group to limit which users the external organization can retrieve Free/Busy information for, run:

    ```PowerShell
    $group = @{
      resourceId = "<groupId>"
      resourceType = "group"
    }
    ```

    Otherwise, run:

    ```PowerShell
    $group = @{
      resourceId = "All"
      resourceType = "user"
    }
    ```

    ```PowerShell
    $body = @{
      "@odata.type" = "microsoft.graph.$capability"
      inboundAccess = @{
        isAllowed = $true
        resourceScopes = @{
          included = @(
            $group
          )
          excluded = @(
            @{ }
          )
        }
      }
    }
    
    New-MgPolicyCrossTenantAccessPolicyPartnerM365Capability -CrossTenantAccessPolicyConfigurationPartnerTenantId $partnerId -BodyParameter $body
    ```

### Create Microsoft 365 Cross-Tenant Access Policies for MailTips

For each existing MailTips configuration from Part 1, create the corresponding Microsoft 365 Cross-Tenant Access Policy. You need the following information:

- The unique Microsoft Entra Tenant ID of the external organization. An administrator for the external organization can find this ID in their [Azure Portal under Microsoft Entra ID](/en-us/azure/azure-portal/get-subscription-tenant-id#find-your-microsoft-entra-tenant).
- The correct capability for the desired MailTips access. Use the following table to determine the correct capability:

| Capability | Effective Access | Replaces |
| --- | --- | --- |
| ***crossTenantMailTipsLimited*** | Allows access to MailTips with restricted subset of recipient information | Organization Relationships with MailTipsAccessLevel set to Limited |
| ***crossTenantMailTipsAll*** | Allows access to MailTips with out-of-office status, automatic replies, and all recipient-specific info | Organization Relationships with MailTipsAccessLevel set to All |

- Optionally, a security group containing internal users whose MailTips information the external organization can retrieve. When you provide this group, users in the external organization can only retrieve MailTips information from internal users in this group.

Tip

While Global Admin privileges are required to create the Entra Cross-Tenant Access Policy Trust Relationship, you can use either Global Admin or Exchange Admin privileges to configure the Microsoft 365 Cross-Tenant Access Policies for MailTips.

1. For each MailTips sharing configuration identified in Part 1, enable the corresponding capability in the partner policy:

    ```PowerShell
    $partnerId = "<partnerTenantId>"
    $capability = "<capabilityName>"
    ```

    If you're using a security group to limit which users the external organization can retrieve MailTips information for, run:

    ```PowerShell
    $group = @{
      resourceId = "<groupId>"
      resourceType = "group"
    }
    ```

    Otherwise, run:

    ```PowerShell
    $group = @{
      resourceId = "All"
      resourceType = "user"
    }
    ```

    ```PowerShell
    $body = @{
      "@odata.type" = "microsoft.graph.$capability"
      inboundAccess = @{
        isAllowed = $true
        resourceScopes = @{
          included = @(
            $group
          )
          excluded = @(
            @{ }
          )
        }
      }
    }
    
    New-MgPolicyCrossTenantAccessPolicyPartnerM365Capability -CrossTenantAccessPolicyConfigurationPartnerTenantId $partnerId -BodyParameter $body
    ```

### Create Microsoft 365 Cross-Tenant Access Policies for Calendar Sharing

For each existing Sharing Policy configuration from Part 1, create the corresponding Microsoft 365 Cross-Tenant Access Policy capability. You need the following information:

- For domain-specific Sharing Policies, the unique Microsoft Entra Tenant ID of the external organization. An administrator for the external organization can find this ID in their [Azure Portal under Microsoft Entra ID](/en-us/azure/azure-portal/get-subscription-tenant-id#find-your-microsoft-entra-tenant).
- The correct capability for the desired Calendar Sharing access. Use the following table to determine the correct capability:

| Capability | Effective Access | Replaces |
| --- | --- | --- |
| ***CrossTenantCalendarSharingFreeBusySimple*** | Calendar sharing - time only | Sharing Policies with CalendarSharingFreeBusySimple |
| ***CrossTenantCalendarSharingFreeBusyDetail*** | Calendar sharing - time, subject, and location | Sharing Policies with CalendarSharingFreeBusyDetail |
| ***CrossTenantCalendarSharingFreeBusyReviewer*** | Calendar sharing - full details | Sharing Policies with CalendarSharingFreeBusyReviewer |

- Capability names are case-sensitive. Use the values exactly as listed above.
- Optionally, a security group containing internal users whose calendar information the external organization can retrieve. When you provide this group, users in the external organization can only retrieve calendar information from internal users in this group. **For organizations with multiple existing Sharing Policies assigned to different mailboxes, you need to use security groups to create comparable Cross-Tenant Access Policies.**

Tip

While Global Admin privileges are required to create the Entra Cross-Tenant Access Policy Trust Relationship, you can use either Global Admin or Exchange Admin privileges to configure the Microsoft 365 Cross-Tenant Access Policies for Calendar Sharing.

1. Create the corresponding wildcard (Domain: \*) policy. If your existing Sharing Policy didn't include a wildcard policy, you can skip to step 2.

    ```PowerShell
    $capability = "<capabilityName>"
    ```

    If you're using a security group to limit which users the external organizations can retrieve Calendar information from, run:

    ```PowerShell
    $group = @{
      resourceId = "<groupId>"
      resourceType = "group"
    }
    ```

    Otherwise, run:

    ```PowerShell
    $group = @{
      resourceId = "All"
      resourceType = "group"
    }
    ```

    ```PowerShell
    $body = @{
      "@odata.type" = "#microsoft.graph.$capability"
      inboundAccess = @{
        isAllowed = $true
        resourceScopes = @{
          included = @(
            $group
          )
          excluded = @(
           @{ }
          )
        }
      }
    }
    
    New-MgPolicyCrossTenantAccessPolicyDefaultM365Capability -BodyParameter $body
    ```
2. Create the corresponding Anonymous policy. If your existing Sharing Policy didn't include an Anonymous policy, you can skip to step 3.

    Note

    Anonymous calendar publishing doesn't depend on EWS and keeps working after EWS deprecation, as long as the existing Sharing Policy stays enabled. It stops working when you disable or remove that existing Sharing Policy. To avoid this, create the matching Anonymous capability before you disable the policy. We recommend moving Anonymous publishing to Cross-Tenant Access Policy too, so all sharing settings are managed in one place.

    Anonymous capabilities are set in the default Microsoft 365 Cross-Tenant Access Policy only. It is not possible to set an anonymous policy for a specific partner Tenant ID.

    | Capability | Effective Access | Replaces |
    | --- | --- | --- |
    | ***AnonymousCalendarSharingFreeBusySimple*** | Calendar sharing - time only | Anonymous Sharing Policies with CalendarSharingFreeBusySimple |
    | ***AnonymousCalendarSharingFreeBusyDetail*** | Calendar sharing - time, subject, and location | Anonymous Sharing Policies with CalendarSharingFreeBusyDetail |
    | ***AnonymousCalendarSharingFreeBusyReviewer*** | Calendar sharing - full details | Anonymous Sharing Policies with CalendarSharingFreeBusyReviewer |

    ```PowerShell
    $capability = "<capabilityName>"
    ```

    If you're using a security group to limit which users can publish their calendars anonymously, run:

    ```PowerShell
    $group = @{
      resourceId = "<groupId>"
      resourceType = "group"
    }
    ```

    Otherwise, run:

    ```PowerShell
    $group = @{
      resourceId = "All"
      resourceType = "group"
    }
    ```

    ```PowerShell
    $body = @{
      "@odata.type" = "#microsoft.graph.$capability"
      inboundAccess = @{
        isAllowed = $true
        resourceScopes = @{
          included = @(
            $group
          )
           excluded = @(
           @{ }
          )
        }
      }
    }
    
    New-MgPolicyCrossTenantAccessPolicyDefaultM365Capability -BodyParameter $body
    ```
3. Create the corresponding domain specific policies. For each partner tenant associated with the domains in your existing Sharing Policy, run:

    ```PowerShell
    $partnerId = "<partnerTenantId>"
    $capability = "<capabilityName>"
    ```

    If you are using a security group to limit which users Calendar information may be retrieved by the external organization, run:

    ```PowerShell
    $group = @{
      resourceId = "<groupId>"
      resourceType = "group"
    }
    ```

    Otherwise, run:

    ```PowerShell
    $group = @{
      resourceId = "All"
      resourceType = "group"
    }
    ```

    ```PowerShell
    $body = @{
      "@odata.type" = "#microsoft.graph.$capability"
      inboundAccess = @{
        isAllowed = $true
        resourceScopes = @{
          included = @(
            $group
          )
           excluded = @(
           @{ }
          )
        }
      }
    }
    
    New-MgPolicyCrossTenantAccessPolicyPartnerM365Capability -CrossTenantAccessPolicyConfigurationPartnerTenantId $partnerId -BodyParameter $body
    ```

## Part 3 – Test functionality

Existing Organization Relationships and Availability Address Spaces take precedence over Microsoft 365 Cross-Tenant Access Policies. Before verifying that the new Free/Busy and MailTips policies work as expected, disable these configurations. You need to coordinate with an administrator in the external organization to disable the old configurations and complete testing at the same time.

Calendar sharing works differently. Microsoft 365 Cross-Tenant Access Policy takes precedence over Sharing Policies. For each external organization, if a calendar sharing capability applies, it's used and the Sharing Policy is ignored. If no capability applies, the Sharing Policy is used. You can test calendar sharing while your Sharing Policies remain enabled.

Important

If a Sharing Policy has an Anonymous entry with a higher access level than your new calendar sharing capability, the Anonymous entry can still apply. Create the Anonymous capability before you test.

Keep Sharing Policies enabled if you share calendars with on-premises or hybrid Exchange organizations. Microsoft 365 Cross-Tenant Access Policy doesn't apply to them, so they continue to use the Sharing Policy.

1. In both organizations, disable existing Organization Relationships, Availability Address Spaces, and Sharing Policies:

    For each migrated Organization Relationship, run:

    ```PowerShell
    Set-OrganizationRelationship -Identity "<RelationshipName>" -Enabled $False  
    ```

    You can't temporarily disable Availability Address Spaces. Instead, back up migrated Availability Address Space configurations and then remove them.

    ```PowerShell
    Get-AvailabilityAddressSpace <ForestName> | Export-CliXML .\AvailabilityAddressSpaceBackup_<ForestName>.xml  
    Remove-AvailabilityAddressSpace <ForestName>
    ```

    For each migrated Sharing Policy, run: (Skip this step for any Sharing Policy still needed for on-premises or hybrid organizations.)

    ```PowerShell
    Set-SharingPolicy -Identity "<PolicyName>" -Enabled $False
    ```
2. Coordinate with an administrator in each external organization to validate that sharing Free/Busy, MailTips, and calendars is working as expected. If it is, continue to Part 4 to clean up the old configurations.
3. If needed, re-enable existing Organization Relationships, Availability Address Spaces, and Sharing Policies:

    For each Organization Relationship, run:

    ```PowerShell
    Set-OrganizationRelationship -Identity "<RelationshipName>" -Enabled $True  
    ```

    Restore Availability Address Spaces from your backup file(s):

    ```PowerShell
    Import-Clixml .\AvailabilityAddressSpaceBackup_<ForestName>.xml | ForEach-Object {
      $p = @{ ForestName = $_.ForestName; AccessMethod = $_.AccessMethod }
      foreach ($n in 'ProxyUrl', 'TargetAutodiscoverEpr', 'TargetServiceEpr', 'TargetTenantId') {
        if (-not [string]::IsNullOrEmpty($_.$n)) {
          $p[$n] = $_.$n
        }
      }
      Add-AvailabilityAddressSpace @p
    }
    ```

    For each Sharing Policy, run:

    ```PowerShell
    Set-SharingPolicy -Identity "<PolicyName>" -Enabled $True
    ```

## Part 4 – Clean up old configurations

After you migrate your Free/Busy, MailTips, and Calendar Sharing configurations to Microsoft 365 Cross-Tenant Access Policies, remove the old configurations.

1. Remove unused Organization Relationships.

    ```PowerShell
    Remove-OrganizationRelationship -Identity "<RelationshipName>"
    ```
2. Remove Availability Address Space.

    ```PowerShell
    Remove-AvailabilityAddressSpace <ForestName>
    ```
3. Remove unused Calendar Sharing policies.

    ```PowerShell
    Remove-SharingPolicy -Identity "<PolicyName>"
    ```

Important

Don't remove a Sharing Policy that is still needed for calendar sharing with on-premises or hybrid Exchange organizations, which Microsoft 365 Cross-Tenant Access Policy doesn't cover, or for anonymous calendar publishing that you haven't yet moved to an Anonymous capability.

## References

Working with Entra Cross-Tenant Access Policies:

- [Overview: Cross-tenant access with Microsoft Entra External ID](/en-us/entra/external-id/cross-tenant-access-overview)

Working with Microsoft 365 Cross-Tenant Access Policies:

- [Microsoft 365 cross-tenant access policy Microsoft Graph API overview](/en-us/graph/api/resources/m365-cross-tenant-access-policy-overview)
- Microsoft 365 cross-tenant access policy Microsoft Graph PowerShell cmdlets (Coming Soon)

Working with Organization Relationships:

- [Organization Relationships](/en-us/exchange/sharing/organization-relationships/organization-relationships)
- [Set-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/set-organizationrelationship)

Working with Availability Address Space:

- [Get-AvailabilityAddressSpace](/en-us/powershell/module/exchangepowershell/get-availabilityaddressspace)

Working with Sharing Policies:

- [Sharing policies in Exchange Online](/en-us/exchange/sharing/sharing-policies/sharing-policies)