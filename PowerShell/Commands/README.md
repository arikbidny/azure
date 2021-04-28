# PowerShell

### Basic Commands

- Show PowerShell Version

```
$PSVersionTable
```

- Show MemberType with Get-Member

```
$PSVersionTable | Get-Member
```

- Comparison Operators

```
12 -eq 37 -> Equal Check -> False
12 -eq 12 -> Equal Check -> True
"a" -eq "A" -> Equal Check lower and upper case -> True
"a" -ceq "A" -> Equal Check lower and upper case with case sensitive -> False
12 -ne 37 -> Not Equal -> True
6 -gt 5   -> Greater then -> True
3 -lt 5   -> Less Then -> True
"Apple" -like "A*" -> Equality check for regexp -> True
"My Name is Arik" -match "Arik" -> Find in a String -> True
"My Name is Arik" -cmatch "ARIK" -> Find in a String with case sensitivity -> FALSE
```

- Write to Host

```
write-host "Hello World"
```

- Aliases

```
PS C:\WINDOWS\system32> Get-Alias ls

CommandType     Name                                               Version    Source
-----------     ----                                               -------
Alias           ls -> Get-ChildItem

Set-Alias blah Get-Process -> For setting the aliases

```

- Getting Help

```
help dir ### Get help for dir command
help Get-ChildItem -online ## Goes online to the command
```

- Objects ( Everything in powershell is an objects )

- Sorting

```
Get-ChildItem | Sort-Object ## Sort folder by name
$files | sort -propery length ## Sort by length
```

- Filtering

```
$files | where length -gt 50000
```

- Filtering using loops

```
$files | where {($_.length -gt 50000) -and ($_.Name -like "g*")}
```

- Foreach Loop

```
PS C:\WINDOWS\system32> 1..10 |foreach {$_*2}
2
4
6
8
10
12
14
16
18
20


PS C:\WINDOWS\system32> 1..10 |foreach {if($_%2){"$_ is odd"}}
1 is odd
3 is odd
5 is odd
7 is odd
9 is odd
```

- Arrays

```
PS C:\WINDOWS\system32> $strComputers = @("Server1","Server2","Server3")
PS C:\WINDOWS\system32> $strComputers
Server1
Server2
Server3
PS C:\WINDOWS\system32> $strComputers[0]
Server1
PS C:\WINDOWS\system32> $strComputers[2] = "Server4"
PS C:\WINDOWS\system32> $strComputers.length
3
PS C:\WINDOWS\system32> $strComputers2 = $("Server10")
PS C:\WINDOWS\system32> $strComputers + $strComputers2
Server1
Server2
Server4
Server10
PS C:\WINDOWS\system32> $strComputers | foreach {$_}
Server1
Server2
Server4
```

- Hash Tables

```
PS C:\WINDOWS\system32> $empNumbers = @{"John Doe" = 11123; "Bob James" = 2131321}
PS C:\WINDOWS\system32> $empNumbers

Name                           Value
----                           -----
John Doe                       11123
Bob James                      2131321


PS C:\WINDOWS\system32> $empNumbers["Gohn Doe"]
PS C:\WINDOWS\system32> $empNumbers["John Doe"]
11123
```

- Formatting Output

```
$files | format-list -Property name, length
get-process | sort -property company | format-table -property path.name,id -groupby company
```

- Saving Output

```
Get-Process | Out-file c:\temp\processes.txt
Get-Process | ConvertTo-HTML | Out-file c:\temp\processes.html
invoke-expression c:\temp\processes.html ### find a program that fites to html and run
Get-Process | export-csv c:\temp\process.csv
```

- Importing Data

```
invoke-expression .\temp.csv
$names = Import-csv .\temp.csv
$names | format-table
```

- Functions

```
function Add-Numbers
{
    param([int]$num1, [int]$num2)
    $num1 + $num2
}

Add-Numbers -num1 123 -num2 456
```

- Iterate over Object

```
$subnetList = @{"sub1" = "10.0.0.0/24"; "sub2" = "10.0.1.0/24"}

$subnetList.GetEnumerator() | ForEach-Object {
    $_.Key
    $_.Value
}
```

- Convert to Json

```
(Get-UICulture).Calendar | ConvertTo-Json

{
  "MinSupportedDateTime": "0001-01-01T00:00:00",
  "MaxSupportedDateTime": "9999-12-31T23:59:59.9999999",
  "AlgorithmType": 1,
  "CalendarType": 1,
  "Eras": [
    1
  ],
  "TwoDigitYearMax": 2029,
  "IsReadOnly": true
}
```

- Convert From Json

```
Get-Content JsonFile.JSON | ConvertFrom-Json
```
