---
layout: Conceptual
title: Create migration endpoints with OAuth authentication | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/oauth-migration-endpoint
Manager: aleeming
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: The OAuth token exchange described here will allow the Microsoft 365 Mailbox Replication Service to authenticate with the organization’s on-premises Exchange environment using Oauth. This is a secure replacement for the use of basic auth (username and password) credentials of a user who is a member of privileged role groups in the on-premises Active Directory.
ms.date: 2026-11-10T00:00:00.0000000Z
ms.service: exchange-server-it-pro
ms.topic: how-to
author: soropeza1
ms.author: sahernan
locale: en-us
document_id: 4811174a-41e8-0f41-bdfc-21ab3f8abf8a
document_version_independent_id: f3f7a9fd-1123-7a67-3566-c88f6855df84
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/oauth-migration-endpoint.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/oauth-migration-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/oauth-migration-endpoint.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 11e652a9-eebf-9f7d-4238-d74336a7ce6a
---

# Create migration endpoints with OAuth authentication | Microsoft Learn

Historically, the Microsoft 365 (M365) Mailbox Replication Service (MRS) has not allowed customers to authenticate using OAuth when migrating mailboxes between Microsoft 365 and an on-premises Exchange environment. That ability is now available. OAuth offers a secure alternative to using a privileged on-premises Active Directory user’s Basic authentication credentials (username and password). You can use the OAuth method for authentication in hybrid and non-hybrid organizations to migrate mailboxes.

The new OAuth for mailbox migration solution is not the [Hybrid Modern Auth](/en-us/microsoft-365/enterprise/configure-exchange-server-for-hybrid-modern-authentication) solution used to authenticate user access. Instead, it uses a separate application-base authorization model which provides:

- A well-defined application identity representing MRS.
- Clear separation between migration authorization and other Exchange hybrid workloads.
- Tenant-specific authorization using the Service Principal Object ID (OID), rather than a shared application ID.

Once OAuth for MRS is configured, tenant administrators will be able to create an OAuth endpoint to use in migration batches or onboarding/offboarding move jobs.

Important

The new OAuth method is available to:

- Microsoft 365 multi-tenant (WW) environments only.
- On-premises organizations running the October 2026 or newer version of Exchange Server Subscription Edition (SE) or Exchange Server 2019 CU15 with the latest Exchange Security Update (October 2026).

## Prerequisites

1. To configure a tenant to use OAuth for MRS, the tenant administrator must be able to access Microsoft Entra ID.
2. The tenant administrator must configure the on-premises domain to be used for migration.

## Register the on-premises API in Microsoft Entra ID

1. Open Microsoft Entra admin center, go to **App registrations** then select **New registration** to create a single-tenant registration with a recognizable name. Select **Single tenant only** option in the **Supported account types** dropdown and then select **Register**.
2. When the new app registration finishes, open it and select **Add an Application ID URI** from the right-hand column. Remove the default value and replace it with a new URI. **The entire URI must be in lowercase**. Use one of the following options to define this URI, and then select **Save**:

    - Reuse the existing endpoint URI that you configured for migration. It's okay if you're already using this URI for the configuration of existing migration endpoints.
    - Use the Application (client) ID in the URI so it looks like `https://[Application (client) ID].contoso.com/ews/mrsproxy.svc`. The "*contoso.com*" **must** be a domain name that you registered for use in your Microsoft Entra ID tenant.

    [![Screenshot that shows Registered App, add Application ID URI.](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-961b1b9f.png)](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-961b1b9f.png#lightbox)

    Note

    Using the **Application (client) ID** in the domain name portion of the URI is **optional but recommended**. The URI must be specific to the MRS proxy endpoint on-premises and using the ID ensures this. However, you can use any fully qualified name that's specific to the MRS proxy endpoint and part of a domain name that you registered for use in your Microsoft Entra ID tenant. When using the **Application (client) ID** you will need to create the corresponding DNS record for it and add it to the publicly trusted certificate as needed.
3. Add an app role to your application. Select **API permissions** on the left-hand column. Select the three dots to the right of Microsoft Graph and choose **Remove all permissions** to leave direct permissions empty.

    [![Screenshot that shows Registered App, remove default API permissions.](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-8f8c7cc9.png)](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-8f8c7cc9.png#lightbox)

    Next, select **App roles** on the left-hand column. Select **Create an app role** at the top. Fill in the **Create app role** form with the values below and then select **Apply**:

    - Set any short two- or three-word display name. Example: MRS Onprem Onboarding.
    - Set **Allowed member types** to **Applications**.
    - Set **Value** to the same as the display name. Example: `MRS.Onprem.Onboarding`.
    - Provide a suitable description.
    - Select the box to enable the app role.

    [![Screenshot that shows Registered App, API role creation.](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-a219849f.png)](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-a219849f.png#lightbox)
4. Select **Token Configuration** from the left-hand column. Select the **+** symbol to add an optional claim. This opens a pane.

    1. Select **Access** for the token type.
    2. In the claims list, locate and toggle **idtyp**.
    3. Select **Add** to close the pane.

    [![Screenshot that shows Registered App, token configuration, add optional claims.](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-c1a46b20.png)](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-c1a46b20.png#lightbox)
5. Select **Manifest** from the left-hand column. This opens a pane with the JSON configuration of the application. Locate the section labeled `accessToken` under `optionalClaims`, there should be an entry present with name `idtyp`.

```json
"optionalClaims": {
  "accessToken": [
   {
    "additionalProperties": [],
    "essential": false,
    "name": "idtyp",
    "source": null
   }
  ],
  "idToken": [],
  "saml2Token": []
}
```

Add the `xms_aud_guid` property to `optionalClaims` shown below and then select **Save**.

```json
{
   "additionalProperties": [],
   "essential": false,
   "name": "xms_aud_guid",
   "source": null
}
```

After this update, `accessToken` has 2 entries:

```json
"optionalClaims": {
   "accessToken": [
   {
     "additionalProperties": [],
     "essential": false,
     "name": "idtyp",
     "source": null
   },
   {
     "additionalProperties": [],
     "essential": false,
     "name": "xms_aud_guid",
     "source": null
   }
  ],
  "idToken": [],
  "saml2Token": []
},
```

### Register Microsoft 365 MRS service principal in Microsoft Entra ID

You need to register the service principal for the Mailbox Replication Service (MRS) in Microsoft 365 in the Microsoft Entra ID of the tenant that you're using for the migration. Perform the following steps on a computer where the [Microsoft Graph PowerShell module](/en-us/powershell/microsoftgraph) is installed.

1. Connect to Microsoft Graph. This command doesn't require any parameters; it will prompt you for the additional ReadWrite scopes as needed. If access prompts don't appear, ensure the Microsoft Graph PowerShell module is updated to the latest version.

    ```powershell
    Connect-MgGraph
    ```
2. Register the service principal for the MRS Microsoft Entra App.

    Note

    The app ID `dbcda063-249e-42b8-84a1-5c1b9298c1f3` corresponds to the Microsoft Mailbox Replication Service Microsoft Entra App ID.

    ```powershell
     $spn1P = New-MgServicePrincipal -AppId dbcda063-249e-42b8-84a1-5c1b9298c1f3
    ```
3. Validate that you registered the correct service principal.

    ```powershell
    $spn1P | fl DisplayName, AppDisplayName, AppId,Id, ServicePrincipalNames, ServicePrincipalType,AppOwnerOrganizationId
    
    DisplayName            : Mailbox Replication Service
    AppDisplayName         : Mailbox Replication Service
    AppId                  : dbcda063-249e-42b8-84a1-5c1b9298c1f3
    Id                     : d7cd2497-b3a4-4e76-a597-5a59a982f999
    ServicePrincipalNames  : {dbcda063-249e-42b8-84a1-5c1b9298c1f3}
    ServicePrincipalType   : Application
    AppOwnerOrganizationId : f8cdef31-a31e-4b4a-93e4-5f571e91255a
    ```

    Note

    - AppOwnerOrganizationId `f8cdef31-a31e-4b4a-93e4-5f571e91255a` is the [Microsoft cloud service's Microsoft Entra tenant ID](/en-us/troubleshoot/entra/entra-id/governance/verify-first-party-apps-sign-in).
    - `AppId``dbcda063-249e-42b8-84a1-5c1b9298c1f3` is the Microsoft Mailbox Replication Service Microsoft Entra App ID.
4. Assign an application role to the service principal definition.

    a. Open Microsoft Entra admin center and select **App registrations** on the left panel.

    b. Select **All applications**.

    c. Locate the on-premises MRS application you created earlier and copy the **Application (client) ID**.

    d. Select **App Roles** from the left menu. On the App Roles pane locate the app role you created earlier and copy its value.

    [![Screenshot that shows Registered App, app roles, the actual role value selected.](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-a9e71405.png)](../exchangehybrid/hybrid-deployment/media/oauth-migration-endpoint/pasted-image-a9e71405.png#lightbox)
5. In the PowerShell session where the Graph connection is loaded, set the values you selected earlier, then assign the necessary service principal roles to the app.

    ```powershell
    $appId = "Application (client) ID"
    $role = "App role Value"
    
    # on premise API Application
    $app = Get-MgApplication –Filter "AppId eq '$appId'"
    $appRole = $app.AppRoles | ?{$_.Value -eq $role}
    
    # Microsoft Mailbox Replication Service Entra App ID
    $spn1P = Get-MgServicePrincipalByAppId -AppId 'dbcda063-249e-42b8-84a1-5c1b9298c1f3'
    $spnApp = Get-MgServicePrincipalByAppId -AppId $appId
    
    $entry = New-MgServicePrincipalAppRoleAssignedTo -ResourceId $spnApp.Id -ServicePrincipalId $spnApp.Id -AppRoleId $appRole.Id -PrincipalId $spn1P.Id
    ```

    For any errors during entry creation, refer to [Microsoft Graph error responses and resource types](/en-us/graph/errors).
6. Confirm that you assigned the appropriate permission by expanding `$entry` and verifying that the `PrincipalDisplayName` is `Mailbox Replication Service`:

    ```powershell
    $entry | fl AppRoleId, PrincipalDisplayName, PrincipalId, PrincipalType, ResourceDisplayName, ResourceId
    AppRoleId            : 291429fd-19c0-459a-b698-3bbc43b98879
    PrincipalDisplayName : Mailbox Replication Service
    PrincipalId          : d7cd2497-b3a4-4e76-a597-5a59a982f999
    PrincipalType        : ServicePrincipal
    ResourceDisplayName  : Migration OnPrem API
    ResourceId           : 745ad0ce-1383-41f0-8c21-e53d96530e01
    ```

## Exchange on-premises configuration

To complete the OAuth setup, add settings to the Exchange on-premises server that functions as the Mailbox Replication Service (MRS) proxy.

Open a PowerShell window on any Exchange on-premises server that has the most recent Exchange server version installed. Run the following command to set the required settings:

1. Enable MRS OAuth support. Customize several values for your tenant. Separate each value in `AuthorizedEntries` with a pipe symbol (`|`).

    ```powershell
    New-SettingOverride -Name "OAuth MRS Settings" -Component "Mrs" -Section MRSProxyServiceOAuth -Parameters ("Enabled=true","AuthorizedEntries=TenantID|ObjectID|Audience|Role") -Reason "Enabling MRS Proxy OAuth"
    ```

- `TenantID` is the tenant GUID of the tenant where migrations take place. `Audience` is the full **application ID URI**, and it's case sensitive. Retrieve these values from the on-premises API Application you created earlier connect to Microsoft Graph again.

    ```powershell
      Connect-MgGraph
      $appId = "Application (client) ID"
      $app = Get-MgApplication –Filter "AppId eq '$appId'"
      $app | fl DisplayName, IdentifierUris
    
      DisplayName    : Migration OnPrem API
      IdentifierUris : {https://xxxxxxxxxxxx.com/ews/mrsproxy.svc}
    
      $spnApp = Get-MgServicePrincipalByAppId -AppId $appId
      $spnApp | fl DisplayName, AppOwnerOrganizationId
    
      DisplayName            : Migration OnPrem API
      AppOwnerOrganizationId : ebd0560e-XXXX-XXXX-XXXX-XXXXXXXXXXXX
    ```
- `ObjectID` is the service principal ID.

    ```powershell
    $spn1P = Get-MgServicePrincipalByAppId -AppId dbcda063-249e-42b8-84a1-5c1b9298c1f3
    $spn1P.Id
    
    d7cd2497-b3a4-4e76-a597-5a59a982f999
    ```
- `Role` is the role value from your on-premises API Application. This value is case sensitive.

    ```powershell
    $app.AppRoles.Value
    MRS.Onprem.Onboarding
    ```

    Below is the sample setting with the retrieved values:

    ```powershell
    $TenantID = "ebd0560e-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
    $Role = "MRS.Onprem.Onboarding"
    $Audience = "https://xxxxxxxxxxxx.com/ews/mrsproxy.svc"
    $ObjectID = "d7cd2497-b3a4-4e76-a597-5a59a982f999" 
    New-SettingOverride -Name "OAuth MRS Settings" -Component "Mrs" -Section MRSProxyServiceOAuth -Parameters ("Enabled=true","AuthorizedEntries=$TenantID|$ObjectID|$Audience|$Role") -Reason "Enabling MRS Proxy OAuth"
    ```

    Note

    `AuthorizedEntries` accepts multiple comma-separated entries when an additional tenant, object, audience, or role combination is required. In the case of multiple configurations for different tenants, use the following command: `New-SettingOverride -Name "OAuth MRS Settings" -Component "Mrs" -Section MRSProxyServiceOAuth -Parameters ("Enabled=true","AuthorizedEntries=TenantID|ObjectID|Audience|Role, SecondTenantID|SecondObjectID|SecondAudience|SecondRole") -Reason "Enabling MRS Proxy OAuth"` Tenant admins must ensure that `Audience` is unique across each value in `AuthorizedEntries`, and `Audience` is case sensitive.

1. Check to see if any values exist for audience GUID verification.

    ```powershell
    Get-SettingOverride -Component OAuth -Name AudGuidValidation
    ```
2. Enable verification of the audience GUID. Ensure you include any existing values when running this command. Separate multiple values with commas.

    ```powershell
    New-SettingOverride -Name AudGuidValidation -Parameters @("Enabled=true", "AdditionalApplicationIds=[existing value(s) separated by comma],[Application (client) ID]") -Component OAuth -Section "AppIdBasedAudienceValidation" -Reason "Allowing MRS API App"
    ```
3. Enable OAuth for MRS Proxy Service on the front-end servers.

    ```powershell
    New-SettingOverride -Name "Enable CAFE MRS OAuth" -Component Cafe -Section "OAuthAuthorizationInCAT" -Reason "Enable CAFE MRS OAuth" -Parameters "Enabled=true"
    ```

For more information, see [New-SettingOverride](/en-us/powershell/module/exchange/new-settingoverride), [Set-SettingOverride](/en-us/powershell/module/exchange/set-settingoverride), and [Remove-SettingOverride](/en-us/powershell/module/exchange/remove-settingoverride).

### Logging and diagnostics

When you set up OAuth for MRS, enable logging during early migration of mailboxes to help with troubleshooting.

To configure OAuth log settings run this PowerShell command on an on-premises Exchange server to enable OAuth logging in the MRS component:

```powershell
New-SettingOverride -Name "MRS OAuthLogging Settings" -Component "Mrs" -Section MRSProxyAuthLogging -Parameters ("Enabled=true") -Reason "Enabling MRS Proxy OAuth Logging"
```

Set multiple properties to enable the logging you want. When you enable logging, the system writes the log to a file in the **Logging** directory inside the Exchange Server installation directory. By default, this path is `C:\Program Files\Microsoft\Exchange Server\V15\Logging\MrsProxyAuthorization`.

Use some or all of these properties in a `SettingOverride` command to enable or disable logging:

- **Enabled**: Enable basic OAuth logging in MRS. Set this value to `true` to write other detailed logging.
- **LogEventData**: Write these claim values, AppOnly, Tenant ID, Object ID, Application ID, and Audience, when available, to the log.
- **LogExceptionMessage**: Write any exception messages encountered during processing to the log.
- **LogExceptionCallStack**: Write the full call stack of any exceptions encountered to the log.

### Modifying or disabling settings

After you create a setting by using `New-SettingOverride`, use the `Set-SettingOverride` command to modify the settings for logging. For example:

```powershell
Set-SettingOverride -Identity "MRS OAuthLogging Settings" -Parameters ("Enabled=true","LogEventData=true","LogExceptionMessage=true","LogExceptionCallStack=true")
```

Important

`Set-SettingOverride` overwrites any previous settings. Ensure that you retain all previously enabled or disabled settings in new executions of this command. Use `Get-SettingOverride` to check for existing parameters. For example: `Get-SettingOverride -Identity "OAuthLogging Settings" | fl`

To disable a setting, modify the setting `Enabled` value to `false`:

```powershell
Set-SettingOverride "OAuth MRS Settings" -Parameters ("Enabled=false")
```

Or remove the setting entirely:

```powershell
Remove-SettingOverride to remove the entire named setting.  
```

For more information, see [New-SettingOverride](/en-us/powershell/module/exchange/new-settingoverride), [Set-SettingOverride](/en-us/powershell/module/exchange/set-settingoverride), and [Remove-SettingOverride](/en-us/powershell/module/exchange/remove-settingoverride).

### Important logs in on-premises

- Café performs the first layer of OAuth validation. Find relevant logs in `C:\Program Files\Microsoft\Exchange Server\V15\Logging\HttpProxy\Ews`.
- MRS performs the second layer of validation. Find relevant logs in `C:\Program Files\Microsoft\Exchange Server\V15\Logging\MrsProxyAuthorization`.

### Enable session affinity in the load balancer

This is only required if you are using Exchange Server Subscription Edition (SE). Use cookie-based session affinity for the load balancer configuration. For more information see **Scenario C Single namespace with session affinity, Layer 7** in [Load balancing in Exchange Server](/en-us/exchange/architecture/client-access/load-balancing).

## Configuration in Microsoft 365 Exchange

Now that the configuration is completed, you can create an Oauth endpoint that can be used in migration batches or in remote moves.

1. Connect to Exchange Online PowerShell. Start PowerShell as administrator and [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

    ```powershell
    Connect-ExchangeOnline
    ```
2. Create the migration endpoint. Specify the `-UseOauth` parameter when you create the migration endpoint. The `-RemoteServer` parameter must match the host part of the **Application ID URI** in the on-premises API. For more optional configuration parameters, see [New-MigrationEndpoint](/en-us/powershell/module/exchangepowershell/new-migrationendpoint).

    Note

    If you used `https://[Application (client) ID].contoso.com/ews/mrsproxy.svc` in the **Application ID URI** configuration then `RemoteServer` value is `[Application (client) ID].contoso.com`.

    If you used a different URI, for example `https://mail.contoso.com/ews/mrsproxy.svc` then the value to use is `mail.contoso.com`.

    ```powershell
    $remoteServer = "Application ID URI host value"
    New-MigrationEndpoint -UseOAuth -Name "OAuthEndpoint" -RemoteServer $remoteServer -ExchangeRemoteMove
    ```
3. After you create the migration endpoint, run `Test-MigrationServerAvailability`, which gets an OAuth token.

    ```powershell
    Test-MigrationServerAvailability -Endpoint "OAuthEndpoint"
    
    Result           : Success
    Message          : This test only validates retrieving the OAuth token based on the endpoint configuration. It does not attempt to connect to the remote host.
    SupportsCutover  : False
    ErrorDetail      :
    StructuredResult :
    TestedEndpoint   : OAuthEndpoint
    IsValid          : True
    Identity         :
    ObjectState      : New
    
    ```

### Create move requests or migration batches

Use the newly created migration endpoint to configure remote moves by using the `New-MoveRequest` cmdlet. The `-RemoteHostName` value must match the host path of the on-premises application URI as explained in the previous section. Also, specify `-ArchiveDomain` to ensure the cmdlet resolves the correct parameter set:

```powershell
$remoteServer = "Application ID URI host value"
New-MoveRequest -Identity "user@contoso.com" -SourceEndpoint "OAuthEndpoint" -RemoteHostName $remoteServer -Remote -TargetDeliveryDomain "contoso.com" -ArchiveDomain "contoso.com"
```

Here is an example for an offboarding move:

```powershell
$remoteServer = "Application ID URI host value"
New-MoveRequest -Identity "user@contoso.com" -SourceEndpoint "OAuthEndpoint" -Outbound -RemoteHostName $remoteServer -TargetDeliveryDomain "contoso.com" -RemoteTargetDatabase "your target database"
```

For more parameters, see [New-MoveRequest](/en-us/powershell/module/exchangepowershell/new-moverequest).

For migration batch creation, treat the OAuth endpoint the same as any other endpoint type. For more parameters for onboarding, see [New-MigrationBatch](/en-us/powershell/module/exchangepowershell/new-migrationbatch).

```powershell
New-Migrationbatch -Name MyBatch -SourceEndpoint "OAuthEndpoint" 
```