---
external help file: Pester-help.xml
online version: 
schema: 2.0.0
---

# InModuleScope

## SYNOPSIS
Allows you to execute parts of a test script within the
scope of a PowerShell script module.

## SYNTAX

```
InModuleScope [-ModuleName] <String> [-ScriptBlock] <ScriptBlock>
```

## DESCRIPTION
By injecting some test code into the scope of a PowerShell
script module, you can use non-exported functions, aliases
and variables inside that module, to perform unit tests on
its internal implementation.

InModuleScope may be used anywhere inside a Pester script,
either inside or outside a Describe block.

## EXAMPLES

### -------------------------- EXAMPLE 1 --------------------------
```
# The script module:
```

function PublicFunction
{
    # Does something
}

function PrivateFunction
{
    return $true
}

Export-ModuleMember -Function PublicFunction

# The test script:

Import-Module MyModule

InModuleScope MyModule {
    Describe 'Testing MyModule' {
        It 'Tests the Private function' {
            PrivateFunction | Should Be $true
        }
    }
}

Normally you would not be able to access "PrivateFunction" from
the powershell session, because the module only exported
"PublicFunction". 
Using InModuleScope allowed this call to
"PrivateFunction" to work successfully.

## PARAMETERS

### -ModuleName
The name of the module into which the test code should be
injected.
This module must already be loaded into the current
PowerShell session.

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

### -ScriptBlock
The code to be executed within the script module.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: 

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

