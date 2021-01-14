﻿---
external help file: d365fo.integrations-help.xml
Module Name: d365fo.integrations
online version:
schema: 2.0.0
---

# Update-D365ODataEntityBatchMode

## SYNOPSIS
Update a set of Data Entities in Dynamics 365 Finance & Operations

## SYNTAX

```
Update-D365ODataEntityBatchMode [-EntityName] <String> [-Payload] <PSObject[]> [[-PayloadCharset] <String>]
 [-CrossCompany] [[-Tenant] <String>] [[-URL] <String>] [[-ClientId] <String>] [[-ClientSecret] <String>]
 [-RawOutput] [[-Token] <String>] [-EnableException] [<CommonParameters>]
```

## DESCRIPTION
Updates a set of Data Entities, defined as a json payloads, using the OData endpoint of the Dynamics 365 Finance & Operations

The entire payload will be batched into a single request against the OData endpoint

## EXAMPLES

### EXAMPLE 1
```
$payload = '{"SalesTaxGroup":"DK"}'
```

PS C:\\\> $updates = @(\[PSCustomObject\]@{Key = "dataAreaId='USMF',CustomerAccount='Customer1'"; Payload = $payload})
PS C:\\\> $updates += \[PSCustomObject\]@{Key = "dataAreaId='USMF',CustomerAccount='Customer2'"; Payload = $payload}
PS C:\\\> Update-D365ODataEntityBatchMode -EntityName "CustomersV3" -Payload $($updates.ToArray())

This will update a set of Data Entities in Dynamics 365 Finance & Operations using the OData endpoint.
The payload that needs to be updated for all entities is saved in the $payload variable.
The desired customers that needs to be updated are saved into the $updates, with their unique key and the payload.
The $updates variable is passed to the cmdlet.

It will use the default OData configuration details that are stored in the configuration store.

### EXAMPLE 2
```
$token = Get-D365ODataToken
```

PS C:\\\> $payload = '{"SalesTaxGroup":"DK"}'
PS C:\\\> $updates = @(\[PSCustomObject\]@{Key = "dataAreaId='USMF',CustomerAccount='Customer1'"; Payload = $payload})
PS C:\\\> $updates += \[PSCustomObject\]@{Key = "dataAreaId='USMF',CustomerAccount='Customer2'"; Payload = $payload}
PS C:\\\> Update-D365ODataEntityBatchMode -EntityName "CustomersV3" -Payload $($updates.ToArray()) -Token $token

This will update a set of Data Entities in Dynamics 365 Finance & Operations using the OData endpoint.
It will get a fresh token, saved it into the token variable and pass it to the cmdlet.
The payload that needs to be updated for all entities is saved in the $payload variable.
The desired customers that needs to be updated are saved into the $updates, with their unique key and the payload.
The $updates variable is passed to the cmdlet.

It will use the default OData configuration details that are stored in the configuration store.

## PARAMETERS

### -EntityName
Name of the Data Entity you want to work against

The parameter is Case Sensitive, because the OData endpoint in D365FO is Case Sensitive

Remember that most Data Entities in a D365FO environment is named by its singular name, but most be retrieve using the plural name

E.g.
The version 3 of the customers Data Entity is named CustomerV3, but can only be retrieving using CustomersV3

Look at the Get-D365ODataPublicEntity cmdlet to help you obtain the correct name

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Payload
The array of PSCustomObjects that you want to update in the D365FO environment

Each PSCustomObject needs to have a Key and a Payload property

The Key must be a string
The Payload must be a json string

```yaml
Type: PSObject[]
Parameter Sets: (All)
Aliases:

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PayloadCharset
The charset / encoding that you want the cmdlet to use while updating the odata entity

The default value is: "UTF8"

The charset has to be a valid http charset like: ASCII, ANSI, ISO-8859-1, UTF-8

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: UTF-8
Accept pipeline input: False
Accept wildcard characters: False
```

### -CrossCompany
Instruct the cmdlet / function to ensure the request against the OData endpoint will work across all companies

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

### -Tenant
Azure Active Directory (AAD) tenant id (Guid) that the D365FO environment is connected to, that you want to access through OData

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: $Script:ODataTenant
Accept pipeline input: False
Accept wildcard characters: False
```

### -URL
URL / URI for the D365FO environment you want to access through OData

```yaml
Type: String
Parameter Sets: (All)
Aliases: URI

Required: False
Position: 5
Default value: $Script:ODataUrl
Accept pipeline input: False
Accept wildcard characters: False
```

### -ClientId
The ClientId obtained from the Azure Portal when you created a Registered Application

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: $Script:ODataClientId
Accept pipeline input: False
Accept wildcard characters: False
```

### -ClientSecret
The ClientSecret obtained from the Azure Portal when you created a Registered Application

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 7
Default value: $Script:ODataClientSecret
Accept pipeline input: False
Accept wildcard characters: False
```

### -RawOutput
Instructs the cmdlet to output the raw json string directly

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

### -Token
Pass a bearer token string that you want to use for while working against the endpoint

This can improve performance if you are iterating over a large collection/array

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 8
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -EnableException
This parameters disables user-friendly warnings and enables the throwing of exceptions
This is less user friendly, but allows catching exceptions in calling scripts

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

### System.String
## NOTES
Tags: OData, Data, Entity, Update, Upload, Batch

Author: Mötz Jensen (@Splaxi)

## RELATED LINKS