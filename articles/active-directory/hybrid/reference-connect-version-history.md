---
title: 'Azure AD Connect: Version release history | Microsoft Docs'
description: This article lists all releases of Azure AD Connect and Azure AD Sync.
services: active-directory
author: billmath
manager: daveba
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.topic: reference
ms.workload: identity
ms.date: 09/15/2021
ms.subservice: hybrid
ms.author: rodejo
ms.custom: has-adal-ref

ms.collection: M365-identity-device-management
---
# Azure AD Connect: Version release history
The Azure Active Directory (Azure AD) team regularly updates Azure AD Connect with new features and functionality. Not all additions are applicable to all audiences.

This article is designed to help you keep track of the versions that have been released, and to understand what the changes are in the latest version.

This table is a list of related topics:

Topic |  Details
--------- | --------- |
Steps to upgrade from Azure AD Connect | Different methods to [upgrade from a previous version to the latest](how-to-upgrade-previous-version.md) Azure AD Connect release.
Required permissions | For permissions required to apply an update, see [accounts and permissions](reference-connect-accounts-permissions.md#upgrade).


>[!IMPORTANT]
> **On 31 August 2022, all 1.x versions of Azure Active Directory (Azure AD) Connect will be retired because they include SQL Server 2012 components that will no longer be supported.** Either upgrade to the most recent version of Azure AD Connect (2.x version) by that date, or [evaluate and switch to Azure AD cloud sync](../cloud-sync/what-is-cloud-sync.md).
> 
> You need to make sure you are running a recent version of Azure AD Connect to receive an optimal support experience. 
> 
> If you run a retired version of Azure AD Connect it may unexpectedly stop working and you may not have the latest security fixes, performance improvements, troubleshooting and diagnostic tools and service enhancements. Moreover, if you require support we may not be able to provide you with the level of service your organization needs.
> 
> Go to this article to learn more about [Azure Active Directory Connect V2.0](whatis-azure-ad-connect-v2.md), what has changed in V2.0 and how this change impacts you.
>
> Please refer to [this article](./how-to-upgrade-previous-version.md) to learn more about how to upgrade Azure AD Connect to the latest version.
>
> For version history information on retired versions, see [Azure AD Connect version release history archive](reference-connect-version-history-archive.md)

>[!NOTE]
>Releasing a new version of Azure AD Connect is a process that requires several quality control step to ensure the operation functionality of the service, and while we go through this process the version number of a new release as well as the release status will be updated to reflect the most recent state.
Not all releases of Azure AD Connect will be made available for auto upgrade. The release status will indicate whether a release is made available for auto upgrade or for download only. If auto upgrade was enabled on your Azure AD Connect server then that server will automatically upgrade to the latest version of Azure AD Connect that is released for auto upgrade. Note that not all Azure AD Connect configurations are eligible for auto upgrade. 

>To clarify the use of Auto Upgrade, it is meant to push all important updates and critical fixes to you. This is not necessarily the latest version because not all versions will require/include a fix to a critical security issue (just one example of many). Critical issues would usually be addressed with a new version provided via Auto Upgrade. If there are no such issues, there are no updates pushed out using Auto Upgrade, and in general if you are using the latest auto upgrade version you should be good.
However, if you’d like all the latest features and updates, the best way to see if there are any is to check this page and install them as you see fit. 

>Please follow this link to read more about [auto upgrade](how-to-connect-install-automatic-upgrade.md)


## Download links
 - If you are using Windows Server 2016 or newer you should use Azure AD Connect V2.0. You can download the latest version of Azure AD Connect 2.0 using [this link](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
 - If you are still using an older version of Windows Server you should use Azure AD Connect V1.6. You can download the latest version of Azure AD Connect V1 using [this link](https://www.microsoft.com/download/details.aspx?id=103336). 
 - We are only applying critical changes to the V1 versions going forward, and you may not find some of the features and fixes for V2 in the V1 releases - so you should upgrade to the V2 version as soon as possible.

## 2.0.25.1

>[!NOTE] 
> This is a hotfix update release of Azure AD Connect. This release requires Windows Server 2016 or newer and fixes a security issue that is present in version 2.0 of Azure AD Connect, as well as some other bug fixes.

### Release status
9/14/2021: Released for download only, not available for auto upgrade.

### Bug fixes

 - We fixed a security issue where an unquoted path was used to point to the Azure AD Connect service. This path is now a quoted path.
 - Fixing an import config issue with writeback enabled when using the existing AD connector account.
 - We fixed an issue in Set-ADSyncExchangeHybridPermissions and other related cmdlets, which were broken from 1.6 due to an invalid inheritance type.
 - The cmdlet we published in a previous release to set the TLS version had an issue where it overwrites the keys, destroying any values that were in them. We fixed this by only creating a new key if one does not already exist. A warning is also added to let users know the TLS registry changes are not exclusive to Azure AD Connect and may impact other applications on the same server as well.
 - We added a check to enforce auto upgrade for V2.0 to require Windows Server 2016 or newer.
 - We added 'Replicating Directory Changes' permission in the Set-ADSyncBasicReadPermissions cmdlet.
 - We made a change to prevent UseExistingDatabase and import configuration from being used together since these could contain conflicting configuration settings.
 - We made a change to allow a user with the Application Admin role to change the App Proxy service configuration.
 - We removed the '(Preview)' label from the labels of Import/Export settings - this functionality has been in General Availability for some time now.
 - We change some labels that still refered to "Company Administrator" - we now use the role name "Global Administrator".
 - We created new AAD Kerberos PowerShell cmdlets "\*-AADKerberosServer" to add a Claims Transform rule to the AAD Service Principal.

### Functional changes
 - We added the latest versions of MIM Connectors (1.1.1610.0). More information can be found at [the release history page of the MiM connectors](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-version-history#1116100-september-2021)
 - We have added a configuration option to disable the Soft Matching feature in Azure AD Connect. We advise customers to disable soft matching unless they need it to take over cloud only accounts. This [article](https://docs.microsoft.com/powershell/module/msonline/set-msoldirsyncfeature?view=azureadps-1.0) shows how to disable Soft Matching.

## 2.0.10.0

### Release status
8/19/2021: Released for download only, not available for auto upgrade.

>[!NOTE] 
>This is a hotfix update release of Azure AD Connect. This release requires Windows Server 2016 or newer. This hotfix addresses an issue that is present in version 2.0 as well as in Azure AD Connect version 1.6. If you are running Azure AD Connect on an older Windows Server you should install the [1.6.13.0](#16130) build instead.

### Release status
8/19/2021: Released for download only, not available for auto upgrade.

### Known issues
 - Under certain circumstances the installer for this version will display an error mentioning that TLS 1.2 is not enabled and will stop the installation. This is due to an error in the code that verifies the registry setting for TLS 1.2. We will correct this in a future release. Customers who see this issue should follow the instructions for enabling TLS 1.2 that can be found in the article "[TLS 1.2 enforcement for Azure AD Connect](reference-connect-tls-enforcement.md)".

### Bug fixes

 - We fixed a bug where, when a domain is renamed, Password Hash Sync would fail with an error indicating "a specified cast is not valid" in the Event log. This is a regression from earlier builds.

## 1.6.13.0
>[!NOTE] 
>This is a hotfix update release of Azure AD Connect. This release is intended for customers who are running Azure AD Connect on a server with Windows Server 2012 or 2012 R2.

8/19/2021: Released for download only, not available for auto upgrade.

### Bug fixes

 - We fixed a bug where, when a domain is renamed, Password Hash Sync would fail with an error indicating "a specified cast is not valid" in the Event log. This is a regression from earlier builds.

### Functional changes
There are no functional changes in this release

## 2.0.9.0

### Release status
8/17/2021: Released for download only, not available for auto upgrade.

### Bug fixes
>[!NOTE] 
>This is a hotfix update release of Azure AD Connect. This release requires Windows Server 2016 or newer. This release addresses an issue that is present in version 2.0.8.0, this issue is not present in Azure AD Connect version 1.6

 - We fixed a bug where, when syncing a large number of Password Hash Sync transactions, the Event log entry length would exceed the maximum allowed length for a Password Hash Sync event entry. We now split the lengthy log entry into multiple entries.

## 2.0.8.0
>[!NOTE] 
>This is a security update release of Azure AD Connect. This release requires Windows Server 2016 or newer. If you are using an older version of Windows Server, please use [version 1.6.11.3](#16113).
>This release addresses a vulnerability as documented in [this CVE](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-36949). For more information about this vulnerability please refer to the CVE.
>You can download the latest version of Azure AD Connect 2.0 using [this link](https://www.microsoft.com/en-us/download/details.aspx?id=47594).

### Release status
8/10/2021: Released for download only, not available for auto upgrade. 

### Functional changes
There are no functional changes in this release

## 1.6.11.3 
>[!NOTE] 
>This is security update release of Azure AD Connect. This version is intended to be used by customers are running an older version of Windows Server and cannot upgrade their server to Windows Server 2016 or newer as this time. You cannot use this version to update an Azure AD Connect V2.0 server.
>This release addresses a vulnerability as documented in [this CVE](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-36949). For more information about this vulnerability please refer to the CVE.
>You can download the latest version of Azure AD Connect 1.6 using [this link](https://www.microsoft.com/download/details.aspx?id=103336)

### Release status
8/10/2021: Released for download only, not available for auto upgrade.

### Functional changes
There are no functional changes in this release

## 2.0.3.0
>[!NOTE] 
>This is a major release of Azure AD Connect. Please refer to the [Azure Active Directory V2.0 article](whatis-azure-ad-connect-v2.md) for more details.

### Release status
7/20/2021: Released for download only, not available for auto upgrade
### Functional changes
 - We have upgraded the LocalDB components of SQL Server to SQL 2019. 
 - This release requires Windows Server 2016 or newer, due to the requirements of SQL Server 2019. Note that an in-place upgrade of Windows Server on an Azure AD Connect server is not supported, so you may need to use a [swing migration](how-to-upgrade-previous-version.md#swing-migration).
 -	In this release we enforce the use of TLS 1.2. If you have enabled your Windows Server for TLS 1.2, AADConnect will use this protocol. If TLS 1.2 is not enabled on the server you will see an error message when attempting to install AADConnect and the installation will not continue until you have enabled TLS 1.2. Note that you can use the new “Set-ADSyncToolsTls12” cmdlets to enable TLS 1.2 on your server.
 -	With this release, you can use a user with the user role “Hybrid Identity Administrator” to authenticate when you install Azure AD Connect. You no longer need the Global Administrator role for this.
 - We have upgraded the Visual C++ runtime library to version 14 as a prerequisite for SQL Server 2019	
 -	This release uses the MSAL library for authentication, and we have removed the older ADAL library, which will be retired in 2022.	
 -	We no longer apply permissions on the AdminSDHolders, following Windows security guidance. We changed the parameter "SkipAdminSdHolders" to "IncludeAdminSdHolders" in the ADSyncConfig.psm1 module.
 -	Passwords will now be reevaluated when an expired password is "unexpired", regardless of whether the password itself is changed. If for a user the password is set to “Must change password at next logon”, and this flag is cleared (thus "unexpiring" the password) then the "unexpired" status and the password hash are synced to Azure AD, and when the user attempts to sign in in Azure AD they can use the unexpired password.
To sync an expired password from Active Directory to Azure Active Directory please use the [Synchronizing temporary passwords](how-to-connect-password-hash-synchronization.md#synchronizing-temporary-passwords-and-force-password-change-on-next-logon)	feature in Azure AD Connect. Note that you will need to enable password writeback to use this feature, so the password the use updates is written back to Active Directory too.
 - We have added two new cmdlets to the ADSyncTools module to enable or retrieve TLS 1.2 settings from the Windows Server. 
   - Get-ADSyncToolsTls12
   - Set-ADSyncToolsTls12
   
You can use these cmdlets to retrieve the TLS 1.2 enablement status, or set it as needed. Note that TLS 1.2 must be enabled on the server for the installation or AADConnect to succeed.

 -	We have revamped ADSyncTools with several new and improved cmdlets. The [ADSyncTools article](reference-connect-adsynctools.md) has more details about these cmdlets. 
  The following cmdlets have been added or updated 
    - Clear-ADSyncToolsMsDsConsistencyGuid	
    - ConvertFrom-ADSyncToolsAadDistinguishedName	
    - ConvertFrom-ADSyncToolsImmutableID	
    - ConvertTo-ADSyncToolsAadDistinguishedName	
    - ConvertTo-ADSyncToolsCloudAnchor	
    - ConvertTo-ADSyncToolsImmutableID	
    - Export-ADSyncToolsAadDisconnectors	
    - Export-ADSyncToolsObjects	
    - Export-ADSyncToolsRunHistory	
    - Get-ADSyncToolsAadObject	
    - Get-ADSyncToolsMsDsConsistencyGuid	
    - Import-ADSyncToolsObjects	
    - Import-ADSyncToolsRunHistory	
    - Remove-ADSyncToolsAadObject	
    - Search-ADSyncToolsADobject	
    - Set-ADSyncToolsMsDsConsistencyGuid	
    - Trace-ADSyncToolsADImport	
    - Trace-ADSyncToolsLdapQuery	
-	We now use the V2 endpoint for import and export and we fixed issue in the Get-ADSyncAADConnectorExportApiVersion cmdlet. You can read more about the V2 endpoint in the [Azure AD Connect sync V2 endpoint article](how-to-connect-sync-endpoint-api-v2.md).
-	We have added the following new user properties to sync from on-prem AD to Azure AD	
    - employeeType	
    - employeeHireDate	
-	This release requires PowerShell version 5.0 or newer to be installed on the Windows Server. Note that this version is part of Windows Server 2016 and newer.	
-	We increased the Group sync membership limits to 250k with the new V2 endpoint.
-	We have updated the Generic LDAP connector and the Generic SQL Connector to the latest versions. Read more about these connectors here:
    - [Generic LDAP Connector reference documentation](/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericldap)
    - [Generic SQL Connector reference documentation](/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericsql)
-	In the M365 Admin Center, we now report the AADConnect client version whenever there is export activity to Azure AD. This ensures that the M365 Admin Center always has the most up to date AADConnect client version, and that it can detect when you’re using an outdated version

### Bug fixes
- We fixed an accessibility bug where the screen reader is announcing an incorrect role of the 'Learn More' link.
-	We fixed a bug where sync rules with large precedence values (i.e. 387163089) cause an upgrade to fail. We updated the sproc 'mms_UpdateSyncRulePrecedence' to cast the precedence number as an integer prior to incrementing the value.
-	We fixed a bug where group writeback permissions are not set on the sync account if a group writeback configuration is imported. We now set the group writeback permissions if group writeback is enabled on the imported configuration.
-	We updated the Azure AD Connect Health agent version to 3.1.110.0 to fix an installation failure.
-	We are seeing an issue with non-default attributes from exported configurations where directory extension attributes are configured. When importing these configurations to a new server/installation, the attribute inclusion list is overridden by the directory extension configuration step, so after import only default and directory extension attributes are selected in the sync service manager (non-default attributes are not included in the installation, so the user must manually reenable them from the sync service manager if they want their imported sync rules to work). We now refresh the AAD Connector before configuring directory extension to keep existing attributes from the attribute inclusion list.
-	We fixed an accessibility issues where the page header's font weight is set as "Light". Font weight is now set to "Bold" for the page title, which applies to the header of all pages.
-	The function Get-AdObject in ADSyncSingleObjectSync.ps1 has been renamed to Get-AdDirectoryObject to prevent ambiguity with the AD cmdlet.
-	The SQL function 'mms_CheckSynchronizationRuleHasUniquePrecedence' allow duplicates precedence	on outbound sync rules on different connectors. We removed the condition that allows duplicate rule precedence.
-	We fixed a bug where the Single Object Sync cmdlet fails if the attribute flow data is null i.e. on exporting delete operation	
-	We fixed a bug where the installation fails because the ADSync bootstrap service cannot be started. We now add Sync Service Account to the Local Builtin User Group before starting the bootstrap service.
-	We fixed an accessibility issue where the active tab on AAD Connect wizard is not showing correct color on High Contrast theme. The selected color code was being overwritten due to missing condition in normal color code configuration.
-	We addressed an issue where users were allowed to deselect objects and attributes used in sync rules using the UI and PowerShell. We now show friendly error message if you try to deselect any attribute or object that is used in any sync rules.
-	We made some updates to the “migrate settings code” to check  and fix backward compatibility issue when the script is ran on an older version of Azure AD Connect.	
-	Fixed a bug where, when PHS tries to look up an incomplete object, it does not use the same algorithm to resolve the DC as it used originally to fetch the passwords. In particular, it is ignoring affinitized DC information. The Incomplete object lookup should use the same logic to locate the DC in both instances.
-	We fixed a bug where AADConnect cannot read Application Proxy items using Microsoft Graph due to a permissions issue with calling Microsoft Graph directly based on AAD Connect client id. To fix this, we removed the dependency on Microsoft Graph and instead use AAD PowerShell to work with the App Proxy Application objects.
-	We removed the writeback member limit from 'Out to AD - Group SOAInAAD Exchange' sync rule	
-	We fixed a bug where, when changing connector account permissions, if an object comes in scope that has not changed since the last delta import, a delta import will not import it. We now display warning alerting user of the issue.
-	We fixed an accessibility issue where the screen reader is not reading radio button position. We added added positional text to the radio button accessibility text field.
-	We updated the Pass-Thru Authentication Agent bundle. The older bundle did not have correct reply URL for HIP's first party application in US Gov.	
-	We fixed a bug where there is a ‘stopped-extension-dll-exception’ on AAD connector export after clean installing AADConnect version 1.6.X.X, which defaults to using DirSyncWebServices API V2, using an existing database.	Previously the setting export version to v2 was only being done for upgrade, we changed so that it is set on clean install as well.
-	The “ADSyncPrep.psm1” module is no longer used and is removed from the installation.

### Known issues
-	The AADConnect wizard shows the “Import Synchronization Settings” option as “Preview”, while this feature is generally Available.
-	Some Active Directory connectors may be installed in a different order when using the output of the migrate settings script to install the product. 
-	The User Sign In options page in the Azure AD Connect wizard mentions “Company Administrator”. This term is no longer used and needs to be replace by “Global Administrator”.
-	The “Export settings” option is broken when the Sign In option has been configured to use PingFederate.
-	While Azure AD Connect can now be deployed using the Hybrid Identity Administrator role, configuring Self Service Password Reset will still require user with the Global Administrator role.
-	When importing the AADConnect configuration while deploying to connect with a different tenant than the original AADConnect configuration, directory extension attributes are not configured correctly.

## 1.6.4.0

>[!NOTE]
> The Azure AD Connect sync V2 endpoint API is now available in these Azure environments:
> - Azure Commercial
> - Azure China cloud
> - Azure US Government cloud
> - This release will not be made available in the Azure German cloud

### Release status
3/31/2021: Released for download only, not available for auto upgrade

### Bug fixes
- This release fixes a bug in version 1.6.2.4 where, after upgrade to that release, the Azure AD Connect Health feature was not registered correctly and did not work. Customers who have deployed build 1.6.2.4 are requested to update their Azure AD Connect server with this build, which will correctly register the Health feature. 

## 1.6.2.4
>[!IMPORTANT]
> Update per March 30, 2021: we have discovered an issue in this build. After installation of this build, the Health services are not registered. We recommend not installing this build. We will release a hotfix shortly.
> If you already installed this build, you can manually register the Health services by using the cmdlet as shown in [this article](./how-to-connect-health-agent-install.md#manually-register-azure-ad-connect-health-for-sync)

>[!NOTE]
> - This release will be made available for download only.
> - The upgrade to this release will require a full synchronization due to sync rule changes.
> - This release defaults the AADConnect server to the new V2 end point. Note that this end point is not supported in the German national cloud and if you need to deploy this version in this environment you need to follow [these instructions](./how-to-connect-sync-endpoint-api-v2.md#rollback) to switch back to the V1 end point. Failure to do so will result in errors in synchronization.

### Release status
3/19/2021: Released for download, not available for auto upgrade

### Functional changes

 - Updated default sync rules to limit membership in written back groups to 50k members.
   - Added new default sync rules for limiting membership count in group writeback (Out to AD - Group Writeback Member Limit) and group sync to Azure Active Directory (Out to AAD - Group Writeup Member Limit) groups.
   - Added member attribute to the 'Out to AD - Group SOAInAAD - Exchange' rule to limit members in written back groups to 50k
 - Updated Sync Rules to support Group Writeback v2
   -If the “In from AAD - Group SOAInAAD” rule is cloned and AADConnect is upgraded.
     - The updated rule will be disabled by default and so the targetWritebackType will be null.
     - AADConnect will writeback all Cloud Groups (including Azure Active Directory Security Groups enabled for writeback) as Distribution Groups.
   -If the “Out to AD - Group SOAInAAD” rule is cloned and AADConnect is upgraded.
     - The updated rule will be disabled by default. However, a new sync rule “Out to AD - Group SOAInAAD - Exchange” which is added will be enabled.
     - Depending on the Cloned Custom Sync Rule's precedence, AADConnect will flow the Mail and Exchange attributes.
     - If the Cloned Custom Sync Rule does not flow some Mail and Exchange attributes, then new Exchange Sync Rule will add those attributes.
     - Note that Group Writeback V2 is in private preview at this moment and not publicly available.
 - Added support for [Selective Password hash Synchronization](./how-to-connect-selective-password-hash-synchronization.md)
 - Added the new [Single Object Sync cmdlet](./how-to-connect-single-object-sync.md). Use this cmdlet to troubleshoot your Azure AD Connect sync configuration. 
 -  Azure AD Connect now supports the Hybrid Identity Administrator role for configuring the service.
 - Updated AADConnectHealth agent to 3.1.83.0
 - New version of the [ADSyncTools PowerShell module](./reference-connect-adsynctools.md), which has several new or improved cmdlets. 
 
   - Clear-ADSyncToolsMsDsConsistencyGuid
   - ConvertFrom-ADSyncToolsAadDistinguishedName
   - ConvertFrom-ADSyncToolsImmutableID
   - ConvertTo-ADSyncToolsAadDistinguishedName
   - ConvertTo-ADSyncToolsCloudAnchor
   - ConvertTo-ADSyncToolsImmutableID
   - Export-ADSyncToolsAadDisconnectors
   - Export-ADSyncToolsObjects
   - Export-ADSyncToolsRunHistory
   - Get-ADSyncToolsAadObject
   - Get-ADSyncToolsMsDsConsistencyGuid
   - Import-ADSyncToolsObjects
   - Import-ADSyncToolsRunHistory
   - Remove-ADSyncToolsAadObject
   - Search-ADSyncToolsADobject
   - Set-ADSyncToolsMsDsConsistencyGuid
   - Trace-ADSyncToolsADImport
   - Trace-ADSyncToolsLdapQuery

 - Updated error logging for token acquisition failures.
 - Updated 'Learn more' links on the configuration page to give more detail on the linked information.
 - Removed Explicit column from CS Search page in the Old Sync UI
 - Additional UI has been added to the Group Writeback flow to prompt the user for credentials or to configure their own permissions using the ADSyncConfig module if credentials have not already been provided in an earlier step.
 - Auto-create MSA for ADSync Service Account on a DC. 
 - 	Added ability to set and get Azure Active Directory DirSync feature Group Writeback V2 in the existing cmdlets:
    - Set-ADSyncAADCompanyFeature
    - Get-ADSyncAADCompanyFeature
 - Added 2 cmdlets to read AWS API version
    - Get-ADSyncAADConnectorImportApiVersion - to get import AWS API version
    - Get-ADSyncAADConnectorExportApiVersion - to get export AWS API version

 - Changes made to synchronization rules are now tracked to assist troubleshooting changes in the service. The cmdlet "Get-ADSyncRuleAudit" will retrieve tracked changes.
 - Updated the Add-ADSyncADDSConnectorAccount cmdlet in the [ADSyncConfig PowerShell module](./how-to-connect-configure-ad-ds-connector-account.md#using-the-adsyncconfig-powershell-module) to allow a user in ADSyncAdmin group to change the AD DS Connector account. 

### Bug fixes
 - Updated disabled foreground color to satisfy luminosity requirements on a white background. Added additional conditions for navigation tree to set foreground text color to white when a disabled page is selected to satisfy luminosity requirements.
 - Increase granularity for Set-ADSyncPasswordHashSyncPermissions cmdlet - Updated PHS permissions script (Set-ADSyncPasswordHashSyncPermissions) to include an optional "ADobjectDN" parameter. 
 - Accessibility bug fix. The screen reader would now describe the UX element that holds the list of forests as "**Forests list**" instead of "**Forest List list**"
 - Updated screen reader output for some items in the Azure AD Connect wizard. Updated button hover color to satisfy contrast requirements. Updated Synchronization Service Manager title color to satisfy contrast requirements.
 - Fixed an issue with installing AADConnect from exported configuration having custom extension attributes - Added a condition to skip checking for extension attributes in the target schema while applying the sync rule.
 - Appropriate permissions are added on install if the Group Writeback feature is enabled.
 - Fix duplicate default sync rule precedence on import
 - Fixed an issue that caused a staging error during V2 API delta import for a conflicting object that was repaired via the health portal.
 - Fixed an issue in the sync engine that caused CS objects to have an inconsistent link state
 - Added import counters to Get-ADSyncConnectorStatistics output.
 - Fixed unreachable domain de-selection(selected previously) issue in some corner cases during pass2 wizard.
 - Modified policy import and export to fail if custom rule has duplicate precedence 
 - Fixed a bug in the domain selection logic.
 - Fixes an issue with build 1.5.18.0 if you use mS-DS-ConsistencyGuid as the source anchor and have clone the In from AD - Group Join rule.
 - Fresh AADConnect installs will use the Export Deletion Threshold stored in the cloud if there is one available and there is not a different one passed in.
 - Fixed issue where AADConnect does not read AD displayName changes of hybrid-joined devices

## 1.5.45.0

### Release status
07/29/2020: Released for download

### Functional changes
This is a bug fix release. There are no functional changes in this release.

### Fixed issues

- Fixed an issue where admin can’t enable “Seamless Single Sign On” if AZUREADSSOACC computer account is already present in the “Active Directory”.
- Fixed an issue that caused a staging error during V2 API delta import for a conflicting object that was repaired via the health portal.
- Fixed an issue in the import/export configuration where disabled custom rule was imported as enabled.

## 1.5.42.0

### Release status
07/10/2020: Released for download

### Functional changes
This release includes a public preview of the functionality to export the configuration of an existing Azure AD Connect server into a .JSON file which can then be used when installing a new Azure AD Connect server to create a copy of the original server.

A detailed description of this new feature can be found in [this article](./how-to-connect-import-export-config.md)

### Fixed issues
- Fixed a bug where there would be a false warning about the local DB size on the localized builds during upgrade.
- Fixed a bug where there would be a false error in the app events for the account name/domain name swap.
- Fixed an error where Azure AD Connect would fail to install on a DC, giving error "member not found".


## 1.5.30.0

### Release status
05/07/2020: Released for download

### Fixed issues
This hotfix build fixes an issue where unselected domains were getting incorrectly selected from the wizard UI if only grandchild containers were selected.


>[!NOTE]
>This version includes the new Azure AD Connect sync V2 endpoint API.  This new V2 endpoint is currently in public preview.  This version or later is required to use the new V2 endpoint API.  However, simply installing this version does not enable the V2 endpoint. You will continue to use the V1 endpoint unless you enable the V2 endpoint.  You need to follow the steps under [Azure AD Connect sync V2 endpoint API (public preview)](how-to-connect-sync-endpoint-api-v2.md) in order to enable it and opt-in to the public preview.  

## 1.5.29.0

### Release status
04/23/2020: Released for download

### Fixed issues
This hotfix build fixes an issue introduced in build 1.5.20.0 where a tenant administrator with MFA was not able to enable DSSO.

## 1.5.22.0

### Release status
04/20/2020: Released for download

### Fixed issues
This hotfix build fixes an issue in build 1.5.20.0 if you have cloned the **In from AD - Group Join** rule and have not cloned the **In from AD - Group Common** rule.

## 1.5.20.0

### Release status
04/09/2020: Released for download

### Fixed issues
- This hotfix build fixes an issue with build 1.5.18.0 if you have the Group Filtering feature enabled and use mS-DS-ConsistencyGuid as the source anchor.
- Fixed an issue in the ADSyncConfig PowerShell module, where invoking DSACLS command used in all the Set-ADSync* Permissions cmdlets would cause one of the following errors:
     - `GrantAclsNoInheritance : The parameter is incorrect.   The command failed to complete successfully.`
     - `GrantAcls : No GUID Found for computer …`

> [!IMPORTANT]
> If you have cloned the **In from AD - Group Join** sync rule and have not cloned the **In from AD - Group Common** sync rule and plan to upgrade, complete the following steps as part of the upgrade:
> 1. During Upgrade, uncheck the option **Start the synchronization process when configuration completes**.
> 2. Edit the cloned join sync rule and add the following two transformations:
>     - Set direct flow `objectGUID` to `sourceAnchorBinary`.
>     - Set expression flow `ConvertToBase64([objectGUID])` to `sourceAnchor`.     
> 3. Enable the scheduler using `Set-ADSyncScheduler -SyncCycleEnabled $true`.



## 1.5.18.0

### Release status
04/02/2020: Released for download

### Functional changes ADSyncAutoUpgrade 

- Added support for the mS-DS-ConsistencyGuid feature for group objects. This allows you to move groups between forests or reconnect groups in AD to Azure AD where the AD group objectID has changed, e.g. when an AD server is rebuilt after a calamity. For more information see [Moving groups between forests](how-to-connect-migrate-groups.md).
- The mS-DS-ConsistencyGuid attribute is automatically set on all synced groups and you do not have to do anything to enable this feature. 
- Removed the Get-ADSyncRunProfile because it is no longer in use. 
- Changed the warning you see when attempting to use an Enterprise Admin or Domain Admin account for the AD DS connector account to provide more context. 
- Added a new cmdlet to remove objects from the connector space the old CSDelete.exe tool is removed, and it is replaced with the new Remove-ADSyncCSObject cmdlet. The Remove-ADSyncCSObject cmdlet takes a CsObject as input. This object can be retrieved by using the Get-ADSyncCSObject cmdlet.

>[!NOTE]
>The old CSDelete.exe tool has been removed and replaced with the new Remove-ADSyncCSObject cmdlet 

### Fixed issues

- Fixed a bug in the group writeback forest/OU selector on rerunning the Azure AD Connect wizard after disabling the feature. 
- Introduced a new error page that will be displayed if the required DCOM registry values are missing with a new help link. Information is also written to log files. 
- Fixed an issue with the creation of the Azure Active Directory synchronization account where enabling Directory Extensions or PHS may fail because the account has not propagated across all service replicas before attempted use. 
- Fixed a bug in the sync errors compression utility that was not handling surrogate characters correctly. 
- Fixed a bug in the auto upgrade which left the server in the scheduler suspended state. 

## 1.4.38.0
### Release status
12/9/2019: Release for download. Not available through auto-upgrade.
### New features and improvements
- We updated Password Hash Sync for Azure AD Domain Services to properly account for padding in Kerberos hashes.  This will provide a performance improvement during password synchronization from Azure AD to Azure AD Domain Services.
- We added support for reliable sessions between the authentication agent and service bus.
- We added a DNS cache for websocket connections between authentication agent and cloud services.
- We added the ability to target specific agent from cloud to test for agent connectivity.

### Fixed issues
- Release 1.4.18.0 had a bug where the PowerShell cmdlet for DSSO was using the login windows credentials instead of the admin credentials provided while running ps. As a result of which it was not possible to enable DSSO in multiple forest through the Azure AD Connect user interface. 
- A fix was made to enable DSSO simultaneously in all forest through the Azure AD Connect user interface

## 1.4.32.0
### Release status
11/08/2019: Released for download. Not available through auto-upgrade.

>[!IMPORTANT]
>Due to an internal schema change in this release of Azure AD Connect, if you manage AD FS trust relationship configuration settings using MSOnline PowerShell then you must update your MSOnline PowerShell module to version 1.1.183.57 or higher

### Fixed issues

This version fixes an issue with existing Hybrid Azure AD joined devices. This release contains a new device sync rule that corrects this issue.
Note that this rule change may cause deletion of obsolete devices from Azure AD. This is not a cause for concern, as these device objects are not used by Azure AD during Conditional Access authorization. For some customers, the number of devices that will be deleted through this rule change can exceed the deletion threshold. If you see the deletion of device objects in Azure AD exceeding the Export Deletion Threshold, it is advised to allow the deletions to go through. [How to allow deletes to flow when they exceed the deletion threshold](how-to-connect-sync-feature-prevent-accidental-deletes.md)

## 1.4.25.0

### Release status
9/28/2019: Released for auto-upgrade to select tenants. Not available for download.

This version fixes a bug where some servers that were auto-upgraded from a previous version to 1.4.18.0 and experienced issues with Self-service password reset (SSPR) and Password Writeback.

### Fixed issues

Under certain circumstances, servers that were auto upgraded to version 1.4.18.0 did not re-enable Self-service password reset and Password Writeback after the upgrade was completed. This auto upgrade release fixes that issue and re-enables Self-service password reset and Password Writeback.

We fixed a bug in the sync errors compression utility that was not handling surrogate characters correctly.

## 1.4.18.0

>[!WARNING]
>We are investigating an incident where some customers are experiencing an issue with existing Hybrid Azure AD joined devices after upgrading to this version of Azure AD Connect. We advise customers who have deployed Hybrid Azure AD join to postpone upgrading to this version until the root cause of these issues are fully understood and mitigated. More information will be provided as soon as possible.

>[!IMPORTANT]
>With this version of Azure AD Connect some customers may see some or all of their Windows devices disappear from Azure AD. This is not a cause for concern, as these device identities are not used by Azure AD during Conditional Access authorization. For more information see [Understanding Azure AD Connect 1.4.xx.x device disappearnce](/troubleshoot/azure/active-directory/reference-connect-device-disappearance)


### Release status
9/25/2019: Released for auto-upgrade only.

### New features and improvements
- New troubleshooting tooling helps troubleshoot "user not syncing", "group not syncing" or "group member not syncing" scenarios.
- Add support for national clouds in Azure AD Connect troubleshooting script.
- Customers should be informed that the deprecated WMI endpoints for MIIS_Service have now been removed. Any WMI operations should now be done via PS cmdlets.
- Security improvement by resetting constrained delegation on AZUREADSSOACC object.
- When adding/editing a sync rule, if there are any attributes used in the rule that are in the connector schema but not added to the connector, the attributes automatically added to the connector. The same is true for the object type the rule affects. If anything is added to the connector, the connector will be marked for full import on the next sync cycle.
- Using an Enterprise or Domain admin as the connector account is no longer supported in new Azure AD Connect Deployments. Current Azure AD Connect deployments using an Enterprise or Domain admin as the connector account will not be affected by this release.
- In the Synchronization Manager a full sync is run on rule creation/edit/deletion. A popup will appear on any rule change notifying the user if full import or full sync is going to be run.
- Added mitigation steps for password errors to 'connectors > properties > connectivity' page.
- Added a deprecation warning for the sync service manager on the connector properties page. This warning notifies the user that changes should be made through the Azure AD Connect wizard.
- Added new error for issues with a user's password policy.
- Prevent misconfiguration of  group filtering by domain and OU filters. Group filtering will show an error when the domain/OU of the entered group is already filtered out and keep the user from moving forward until the issue is resolved.
- Users can no longer create a connector for Active Directory Domain Services or Windows Azure Active Directory in the Synchronization Service Manager UI.
- Fixed accessibility of custom UI controls in the Synchronization Service Manager.
- Enabled six federation management tasks for all sign-in methods in Azure AD Connect.  (Previously, only the “Update AD FS TLS/SSL certificate” task was available for all sign-ins.)
- Added a warning when changing the sign-in method from federation to PHS or PTA that all Azure AD domains and users will be converted to managed authentication.
- Removed token-signing certificates from the “Reset Azure AD and AD FS trust” task and added a separate sub-task to update these certificates.
- Added a new federation management task called “Manage certificates” which has sub-tasks to update the TLS or token-signing certificates for the AD FS farm.
- Added a new federation management sub-task called “Specify primary server” which allows administrators to specify a new primary server for the AD FS farm.
- Added a new federation management task called “Manage servers” which has sub-tasks to deploy an AD FS server, deploy a Web Application Proxy server, and specify primary server.
- Added a new federation management task called “View federation configuration” that displays the current AD FS settings.  (Because of this addition, AD FS settings have been removed from the “Review your solution” page.)

### Fixed issues
- Resolved sync error issue for the scenario where a user object taking over its corresponding contact object has a self-reference (e.g. user is their own manager).
- Help popups now show on keyboard focus.
- For Auto upgrade, if any conflicting app is running from 6 hours, kill it and continue with upgrade.
- Limit the number of attributes a customer can select to 100 per object when selecting directory extensions. This will prevent the error from occurring during export as Azure has a maximum of 100 extension attributes per object.
- Fixed a bug to make the AD Connectivity script more robust.
- Fixed a bug to make Azure AD Connect install on a machine using an existing Named Pipes WCF service more robust.
- Improved diagnostics and troubleshooting around group policies that do not allow the ADSync service to start when initially installed.
- Fixed a bug where display name for a Windows computer was written incorrectly.
- Fix a bug where OS type for a Windows computer was written incorrectly.
- Fixed a bug where non-Windows 10 computers were syncing unexpectedly. Note that the effect of this change is that non-Windows-10 computers that were previously synced will now be deleted. This does not affect any features as the sync of Windows computers is only used for Hybrid Azure AD domain join, which only works for Windows-10 devices.
- Added several new (internal) cmdlets to the ADSync PowerShell module.


## 1.3.21.0
>[!IMPORTANT]
>There is a known issue with upgrading Azure AD Connect from an earlier version to 1.3.21.0 where the Microsoft 365 portal does not reflect the updated version even though Azure AD Connect upgraded successfully.
>
> To resolve this, you need to import the **AdSync** module and then run the `Set-ADSyncDirSyncConfiguration` PowerShell cmdlet on the Azure AD Connect server.  You can use the following steps:
>
>1.	Open PowerShell in administrator mode.
>2.	Run `Import-Module "ADSync"`.
>3.	Run `Set-ADSyncDirSyncConfiguration -AnchorAttribute ""`.
 
### Release status 

05/14/2019: Released for download

### Fixed issues 

- Fixed an elevation of privilege vulnerability that exists in Microsoft Azure Active Directory Connect build 1.3.20.0.  This vulnerability, under certain conditions, may allow an attacker to execute two PowerShell cmdlets in the context of a privileged account, and perform privileged actions.  This security update addresses the issue by disabling these cmdlets. For more information see [security update](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1000).


## Next steps
Learn more about [Integrating your on-premises identities with Azure Active Directory](whatis-hybrid-identity.md).
