---
external help file: GPv2_Cmdlets.xml
online version: 
schema: 2.0.0
ms.assetid: 0AEE3792-7D5C-49D8-A151-743375234451
---

# Remove-GPRegistryValue

## SYNOPSIS
Removes one or more registry-based policy settings from either Computer Configuration or User Configuration in a GPO.

## SYNTAX

### UNNAMED_PARAMETER_SET_1
```
Remove-GPRegistryValue [-Guid] <Guid> [-Key] <String> [[-ValueName] <String>] [[-Domain] <String>]
 [[-Server] <String>] [-Confirm] [-WhatIf]
```

### UNNAMED_PARAMETER_SET_2
```
Remove-GPRegistryValue [-Name] <String> [-Key] <String> [[-ValueName] <String>] [[-Domain] <String>]
 [[-Server] <String>] [-Confirm] [-WhatIf]
```

## DESCRIPTION
The Remove-GPRegistryValue cmdlet removes one or more registry-based policy settings from either Computer Configuration or User Configuration in a GPO.
You can specify the GPO by its display name or by its GUID.

You can specify either a key or a value:

--If you specify a key, registry-based policy settings that configure any of its (first-level) values are removed.
However, if there are registry-based policy settings that configure any subkeys or their values, an error occurs and no policy settings are removed (including those for first-level values of the key).
For a key, specify the Key parameter without the ValueName parameter.

--If you specify a value, the registry-based policy setting that configures that registry value is removed.
For a value, specify the Key parameter without the ValueName parameter.

This cmdlet can take input from the pipeline:

--You can pipe GPO objects to this cmdlet to remove a specified registry-based policy setting from one or more GPOs.

--You can pipe PolicyRegistrySetting objects to this cmdlet to remove one or more registry-based policy settings from a specified GPO.

## EXAMPLES

### -------------------------- EXAMPLE 1 --------------------------
```
C:\PS>Remove-GPRegistryValue -Name "TestGPO" -key "HKCU\Software\Policies\Microsoft\Windows\Control Panel\Desktop" -ValueName ScreenSaveTimeOut 

DisplayName      : TestGPO 
DomainName       : contoso.com 
Owner            : CONTOSO\Domain Admins 
Id               : 35c12ab3-956c-45d5-973b-46b17d225f47 
GpoStatus        : AllSettingsEnabled 
Description      : 
CreationTime     : 2/24/2009 4:41:03 PM 
ModificationTime : 2/25/2009 12:45:52 PM 
UserVersion      : AD Version: 4, SysVol Version: 4 
ComputerVersion  : AD Version: 34, SysVol Version: 34 
WmiFilter        :
```

Description

-----------

This command removes the registry-based policy setting for the registry value "HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Control Panel\Desktop ScreenSaveTimeout" from the "TestGPO" GPO.
The registry value is no longer modified when the GPO is applied on a client.
Removing a policy setting does not delete the registry value on a client.
To delete the registry value when the GPO is applied on a client, you must disable the policy setting by using the Set-GPRegistryValue cmdlet.

### -------------------------- EXAMPLE 2 --------------------------
```
C:\PS>Remove-GPRegistryValue -Name TestGPO -Key HKCU\Software\Policies\Microsoft\ExampleKey
```

Description

-----------

This command removes all the registry-based policy settings that configure (first-level) registry values under the key "HKEY_CURRENT_USER\Software\Policies\Microsoft\ExampleKey" from User Configuration in the "TestGPO" GPO.
If there are registry-based policy settings in User Configuration that configure registry values for any subkeys of this key, an error occurs and no (first-level) policy settings are removed.

## PARAMETERS

### -Domain
Specifies the domain for this cmdlet.
You must specify the fully qualified domain name (FQDN) of the domain (for example: sales.contoso.com).

For the Remove-GPRegistryValue cmdlet, the GPO from which to remove the registry-based policy setting must exist in this domain.

If you do not specify the Domain parameter, the domain of the user that is running the current session is used.
(If the cmdlet is being run from a computer startup or shutdown script, the domain of the computer is used.) For more information, see the Notes section in the full Help.

If you specify a domain that is different from the domain of the user that is running the current session (or, for a startup or shutdown script, the computer), a trust must exist between that domain and the domain of the user (or the computer).

You can also refer to the Domain parameter by its built-in alias, "domainname".
For more information, see about_Aliases.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 4
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Guid
Specifies the GPO from which to remove the registry-based policy setting by its globally unique identifier (GUID).
The GUID uniquely identifies the GPO.

You can also refer to the Guid parameter by its built-in alias, "id".
For more information, see about_Aliases.

```yaml
Type: Guid
Parameter Sets: UNNAMED_PARAMETER_SET_1
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Key
Specifies a registry key for which to remove one or more registry-based policy settings (for example: HKLM\Software\Policies\Microsoft\WindowsNT\DNSClient\UseDomainNameDevolution).

The key must be in one of the two following registry hives:

- HKEY_LOCAL_MACHINE (HKLM) for a registry-based policy setting in Computer Configuration.

- HKEY_CURRENT_USER (HKCU) for a registry-based policy setting in User Configuration.

The Key parameter can be specified with or without the ValueName parameter:

--If the ValueName parameter is specified, the registry-based policy setting that configures that registry value is removed.

--If the ValueName parameter is not specified, all registry-based policy settings that configure any of the (first-level) values of the registry key are removed.
If there are registry-based policy settings that configure any subkeys or their values, an error occurs.

You can also refer to the Key parameter by its built-in alias, "FullKeyPath".
For more information, see about_Aliases.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: 2
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Name
Specifies the GPO from which to remove the registry-based policy setting by its display name.

The display name is not guaranteed to be unique in the domain.
If another GPO with the same display name exists in the domain an error occurs.
You can use the Guid parameter to uniquely identify a GPO.

You can also refer to the Name parameter by its built-in alias, "displayname".
For more information, see about_Aliases.

```yaml
Type: String
Parameter Sets: UNNAMED_PARAMETER_SET_2
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Server
Specifies the name of the domain controller that this cmdlet contacts to complete the operation.
You can specify either the fully qualified domain name (FQDN) or the host name.
For example:

FQDN: DomainController1.sales.contoso.com

Host Name: DomainController1

If you do not specify the name by using the Server parameter, the PDC emulator is contacted.

You can also refer to the Server parameter by its built-in alias, "dc".
For more information, see about_Aliases.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ValueName
Specifies the name of the registry value for which to remove the registry-based policy setting (for example: UseDomainNameDevolution).
If you specify the ValueName parameter, you must also specify the Key parameter.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 3
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### Microsoft.GroupPolicy.Gpo, Microsoft.GroupPolicy.PolicyRegistrySetting
A GPO (from which to remove a registry-based policy setting), or a PolicyRegistrySetting object that represents a registry-based policy setting (to remove from a specified GPO).
Collections that contain GPOs from different domains are not supported.

## OUTPUTS

### Microsoft.GroupPolicy.Gpo
Remove-GPRegistryValue returns the GPO from which the registry-based policy setting (or settings) has been removed.

## NOTES
* The hive of the registry key that you specify -- HKEY_LOCAL_MACHINE (HKLM) or HKEY_CURRENT_USER (HKCU) indicates whether the registry-based policy setting is removed from Computer Configuration or User Configuration.

  If a value for the registry key cannot be located (the registry key is not configured) or if subkeys are present, an error occurs and a corresponding error message is displayed.

  You can use the Domain parameter to explicitly specify the domain for this cmdlet.

  If you do not explicitly specify the domain, the cmdlet uses a default domain.
The default domain is the domain that is used to access network resources by the security context under which the current session is running.
This domain is typically the domain of the user that is running the session.
For example, the domain of the user who started the session by opening Windows PowerShell from the Program Files menu, or the domain of a user that is specified in a runas command.
However, computer startup and shutdown scripts run under the context of the LocalSystem account.
The LocalSystem account is a built-in local account, and it accesses network resources under the context of the computer account.
Therefore, when this cmdlet is run from a startup or shutdown script, the default domain is the domain to which the computer is joined.

## RELATED LINKS

[Get-GPRegistryValue](./Get-GPRegistryValue.md)

[Set-GPRegistryValue](./Set-GPRegistryValue.md)
