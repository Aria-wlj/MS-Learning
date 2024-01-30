# Resources & Docus

##### PowerShell Book (recommended by MS)

https://learn.microsoft.com/en-us/powershell/scripting/learn/ps101/appendix-a?view=powershell-7.4

##### PowerShell Docu (in GitHub)

https://github.com/MicrosoftDocs/PowerShell-Docs/blob/main/README.md

##### Azure Cloud Shell (Ms Learning)

https://learn.microsoft.com/en-us/azure/cloud-shell/overview

##### Azure PowerShell Docu (MS Learning)

https://learn.microsoft.com/en-us/powershell/azure/?view=azps-11.2.0

##### Azure CLI (MS Learning)

https://learn.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest

##### Azure PowerShell (MS Learning)

https://learn.microsoft.com/en-us/powershell/azure/get-started-azureps?view=azps-11.1.0



------

# PowerShell Basic

to start PowerShell: 

```
pwsh
```

#### Connect Azure in PowerShell

Install AZ module in local PowerShell

```
Connect-AzAccount
```



### Get Info

#### Commonly used

##### Help

```powershell
Get-Help get-service -detailed
Get-Help -[command]
```

```powershell
[[command]] -WhatIf
```

```
[[command]] -Confirm
```

##### Get command

```
get-Process
```

##### Get properties

```
___ | Get-Member
```

##### Select property

```
Get-Process | Where-Object Name -eq 'name_of-_process'
```

​	or using built-in filter:

```
Get-Process -Name 'name_of_process'
```

##### Filter & Sorting

```
___ | Select-Object
```



##### ISE, command add-on

To bring up the GUI console

```
ise
```

- Open command add-on in menu



##### Output

- Pipe formatting

```
get-service | format-list *
```

```
get-service | format-table displayname, status
```

```
get-service | sort-object -property status| format-table displayname, status
```

- Pipe Output

```
get-service | out-file c:\file_name.txt
```

- list view

```
get-service | format-list *
```

- Grid view

```
get-service | out-gridview
```

```
get-service | select-object displayname | out-gridview
```

format-table means giving output to command window

out-gridview means giving output to grid view



##### Run remotely

```
Get-service -ComputerName webserver |sort-
```

To operate another computer remotely: open up a remote tab in the menu (New Remote PowerShell tab), open up the script in that device



#### Cmdlet

- install features

```
Get-Windowsfeature -Name web-server | Install-WindowsFeature
```

- backup

(with variables: 

```
$policy = ....
Start-WBBackup -policy $BUpolicy
```



### File

​	create and edit:

```
New-Item fileName.ps1
code .\fileName.ps1
```

​	run:

```
. .\fileName.ps1
```

##### variable

```
$varName = "string"
```

##### prompt

```
$varName = Read-Host "question"
```

##### Output

```
Write-Output "there is a $varName"
```



## Scripting

https://learn.microsoft.com/en-us/training/modules/script-with-powershell/2-introduction-scripting

### Fundamental

#### Variables

```
$varName = 3.14
```

- Single quotation marks: only printing

- Double quotation marks: does interpolating

  ```
  Write-Host "The number is $varName"
  Write-Host "The number plus 2 is $($varName + 2)"
  ```

### Parameters

Write the file Backup.ps1

```
Param(
  [string]$Path = './app',
  [string]$DestinationPath = './Backups'
)
```

Then run the file, with optional params

##### Required Param

```
[Parameter(Mandatory=$true)]
[Parameter(Mandatory)]
```

##### Switch Param

 If this parameter is present when the script is invoked, you perform the check on the content

```
[switch]$PathCheck
```



### Flow Control

```
$Value = 3
If ($Value -le 0) 
{
  Write-Host "Is negative"
} Else {
  Write-Host "Is Positive"
}
```



### Error, Try Catch

```
Try {
   # Do something with a file.
} Catch [System.IO.IOException] {
   Write-Host "Something went wrong"
}  Catch {
   # Catch all. It's not an IOException but something else.
} Finally {
   # Clean up resources.
}
```

### Raising errors

##### - Stop, ErrorAction

```
Try {
   Get-Content './file.txt' -ErrorAction Stop
} Catch {
   Write-Error "File can't be found"
}
```

##### - Should be stop, throw

```
Try {
   If ($Path -eq './forbidden') 
   {
     Throw "Path not allowed"
   }
   # Carry on.

} Catch {
   Write-Error "$($_.exception.message)" # Path not allowed.
}
```























