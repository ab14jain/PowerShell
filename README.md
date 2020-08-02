# PowerShell
PowerShell Cheatsheet

PowerShell for beginners
===================
----------
`This document is getting updated time-to-time. Become a watcher to get updates.`

PowerShell is a windows command-line shell designed especially for system administrators.  It was built on top of the .NET Framework common language runtime (CLR) and the .NET Framework. So,  it accepts and returns .NET Framework objects.
	
PowerShell works in both **INTERACTIVE** mode and **SCRIPT** mode. It possesses **cmdlet** (pronounced "command-let") for doing pre-defined tasks.


## 1. Why Should  I Learn Another Language?


_There wont be much gain, without any pain._ I would recommend learning powershell because of the **advantages** that it offers. 
> **Advantages:**

> - Ease in accessing file systems
> - Ability to access other data stores, such as registry and digital signature certificate stores.
> - Open-source and increasing community base
> - Apart from windows, it is extending support for Linux from next release.
> - As PowerShell is tightly coupled with .NET framework. So, .NET objects can be used. 
> - Ease in working with all Microsoft products (Office suite, Client OS, Server OS, IIS, Databases, Visual Studio Suite, etc.) 
> - Ability to connect to existing windows administrative functionality: 
>  - WMI
>  - Microsoft .NET framework
>  - COM (Component Object Model)
>  - ADSI (Active Directory Services Interface)
>  - Can be used to automate almost any administrative task

## 2. About PowerShell
### 2.1 PowerShell History
Initially, when windows was launched for the first time, it came with the **MS-DOS**. Later, in 1981, batch script (CMD) was introduced, followed by **VBScript** in 1996 and **PowerShell** in 2006. 
PowerShell script have **.ps1** as the file extension. Here, the '1' in '.ps1' doesn't refer to the powerShell version; rather refers to the version of the engine, which runs the powerShell. 

### 2.2 PowerShell Versions
> **PowerShell 1.0**
> - Installed but not enabled on windows Vista and Server 2008

> **PowerShell 2.0**
> - Installed by default on Windows 7 and Server 2008 R2
> - The PowerShell ISE is installed by default on Windows 7
> - Can be installed on Windows XP and Server 2003 or Higher

> **PowerShell 3.0**
> - Installed by default on Windows 8 and Server 2012
> - ISE is installed by default on Windows 8 and Server 2012 GUI
> - Can be installed on Windows 7 and Server 2008 or Higher
> - PowerShell Remoting is enabled by default on Server 2012

There exists [some differences](https://4sysops.com/wiki/differences-between-powershell-versions/) between these versions, and the  latest version of PowerShell is **6.0**. 
The suitable PowerShell version for windows servers is:

|PowerShell Version	| Release Date	| Default Windows Versions	| Available Windows Versions|
| --- | --- | --- | ---|
|PowerShell 1.0	| November 2006	| Windows Server 2008 (*)	| Windows XP SP2|
| | | |Windows XP SP3
| | | |Windows Server 2003 SP1
| | | |Windows Server 2003 SP2
| | | |Windows Server 2003 R2
| | | |Windows Vista
| | | |Windows Vista SP2
| PowerShell 2.0	| October 2009	| Windows 7|
| | | |Windows Server 2008 R2 (**)	Windows XP SP3
| | | |Windows Server 2003 SP2
| | | |Windows Vista SP1
| | | |Windows Vista SP2
| | | |Windows Server 2008 SP1
| | | |Windows Server 2008 SP2
|PowerShell 3.0	| September 2012	| Windows 8|
| | | |Windows Server 2012	Windows 7 SP1
| | | |Windows Server 2008 SP2
| | | |Windows Server 2008 R2 SP1
|PowerShell 4.0	| October 2013	| Windows 8.1|
| | | |Windows Server 2012 R2	Windows 7 SP1
| | | |Windows Server 2008 R2 SP1
| | | |Windows Server 2012
|PowerShell 5.0	|February 2016	|Windows 10	|Windows 8.1|
| | | |Windows Server 2012 R2

Go to windows menu, and type `Windows PowerShell` (don't choose `Windows PowerShell ISE`) and open it. 

### 2.3 PowerShell Environment
To get the PowerShell version installed on the machine, type
```bash
PS C:\> $PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.0.10586.672
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
BuildVersion                   10.0.10586.672
CLRVersion                     4.0.30319.42000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```
Observe that the `PSVersion` which is `5.0` in this case.

To get the Host details,
```
PS C:\> Get-Host

Name             : ConsoleHost
Version          : 5.0.10586.672
InstanceId       : 7756acf5-225d-40b7-ac79-173bf20eadda
UI               : System.Management.Automation.Internal.Host.InternalHostUserInterface
CurrentCulture   : en-US
CurrentUICulture : en-US
PrivateData      : Microsoft.PowerShell.ConsoleHost+ConsoleColorProxy
DebuggerEnabled  : True
IsRunspacePushed : False
Runspace         : System.Management.Automation.Runspaces.LocalRunspace
```
`$env` is a predefined variable in powershell. It will store the complete windows environment information. 

Printing it barely doesn't result in any information.
```
PS C:\> $env 

PS C:\> 
```
The `$env` variable must be accompanied by the other corresponding variable. 
```
PS C:\> $env:COMPUTERNAME
UDHAYPC

PS C:\> $env:USERNAME
UDHAY

PS C:\> $env:USERDNSDOMAIN
prakash.COM

PS C:\> $env:USERPROFILE
C:\Users\UDHAY

PS C:\> $env:ALLUSERSPROFILE
C:\ProgramData

PS C:\> $env:ComSpec
C:\Windows\system32\cmd.exe

PS C:\> $env:HOMEPATH
\Users\UDHAY

PS C:\> $env:HOMEDRIVE
C:

PS C:\> $env:ProgramFiles
C:\Program Files

```
__NOTE:__ If you dont know all the variables part of it, after `:` type `tab` key to all those variables one-by-one.

### 2.4 Support for Other Microsoft languages
PowerShell used a concept called `Aliases` to support commonly used commands in other Microsoft languages like Batch Script (CMD), VBScript, etc. 

Commonly used Batch Script (CMD) commands such as _dir_, _ls_, _cls_, .... are supported in PowerShell.

```bash
PS C:\> Clear-Host   # same as cls in CMD; clears the screen
```
But, they doesn't support those commands extensively. For example, ```dir ``` will work; but not ```dir /A:D```.

To _explicitly_ run the commands and/or scripts of other language in powershell,
```
 $command = @'
cmd.exe /C dir /A:D
'@

Invoke-Expression -Command:$command
```
But, let's ignore this until we understood this language syntax and semantics. 

### 2.5 Command Structure in PowerShell
PowerShell possesses light-weight commands, called _cmdlets_, to do some specific tasks.  

They use a consistent verb-noun structure, where the verb represents the action and the noun represents the object to operate on.

PowerShell cmdlets follow consistent naming patterns, ensuring that construction of a command is easy if you know the object that you want to work with.

All command categories take parameters and arguments. A parameter starts with a hyphen and is used to control the behavior of the command. An argument is a data value consumed by the command.

A simple PowerShell command has the following syntax:

```
command -parameter1 -parameter2 argument1, argument2
```

To get the list of `approved verbs`,
```
PS C:\> Get-Verb

Verb          Group                                                                      
----          -----                                                                      
Add           Common                                                                     
Clear         Common                                                                     
Close         Common                                                                     
Copy          Common                                                                     
Enter         Common                                                                     
Exit          Common                                                                     
Find          Common                                                                     
Format        Common                                                                     
Get           Common                                                                     
Hide          Common                                                                     
Join          Common                                                                     
Lock          Common                                                                     
Move          Common                                                                     
New           Common                                                                     
Open          Common                                                                     
....
[Tailored the list]
```
The Grouping is done based on their common use. 

Each Windows PowerShell verb is assigned to one of the following groups.
- `Common`: Define generic actions that can apply to almost any cmdlet, such as Add.
- `Communications`:  Define actions that apply to communications, such as Connect.
- `Data`:  Define actions that apply to data handling, such as Backup.
- `Diagnostic`: Define actions that apply to diagnostics, such as Debug.
- `Lifecycle`: Define actions that apply to the lifecycle of a cmdlet, such as Complete.
- `Security`: Define actions that apply to security, such as Revoke.
- `Other`: Define other types of actions.


To get the list of all `nouns`, 
```
PS C:\> Get-Command –Noun * 

CommandType     Name                                               ModuleName                                                                          
-----------     ----                                               ----------     
Function        Clear-Host                                                                                                                             
Function        Disable-PSTrace                                    PSDiagnostics                                                                       
Function        Disable-PSWSManCombinedTrace                       PSDiagnostics                                                                       
Function        Disable-WSManTrace                                 PSDiagnostics                                                                       
Function        Enable-PSTrace                                     PSDiagnostics                                                                       
Function        Enable-PSWSManCombinedTrace                        PSDiagnostics                                                                       
Function        Enable-WSManTrace                                  PSDiagnostics                                                                       
Function        Get-DscConfiguration                               PSDesiredStateConfiguration                                                         
Function        Get-DscLocalConfigurationManager                   PSDesiredStateConfiguration                                                         
Function        Get-DscResource                                    PSDesiredStateConfiguration                                                         
Function        Get-FileHash                                       Microsoft.PowerShell.Utility                                                        
Function        Get-IseSnippet                                     ISE                                                                                 
Function        Get-LogProperties                                  PSDiagnostics                                                                       
Function        Get-Verb                                                         
...
[Tailored the list]
```
Observe that `Get-Verb` too is a noun. 

Also, there is another command named `Get-Command` to get a particular set of commands. 

To get all the command in the current user scope in a particular windows machine, 
```
PS C:\> Get-Command -All

CommandType     Name                                               ModuleName                                                                          
-----------     ----                                               ----------                                                                          
Alias           cat -> Get-Content                                                                                                                     
Alias           cd -> Set-Location                                                                                                                     
Alias           chdir -> Set-Location                                                                                                                  
Alias           clc -> Clear-Content                                                                                                                   
Alias           clear -> Clear-Host                                                                                                                    
Alias           clhy -> Clear-History                                                                                                                  
Alias           history -> Get-History                                                                                                                 
Alias           icim ->                                            CimCmdlets                                                                          
Function        Get-IseSnippet                                     ISE                                                                                 
Function        Get-LogProperties                                  PSDiagnostics                                                                       
Function        Get-User                                           Carbon                                                                              
Function        Get-Verb                                                                                                                               
Function        Invoke-AsWorkflow                                  PSWorkflowUtility                                                                   
Function        New-IseSnippet                                     ISE                                                                                 
Filter          more                                                                                                                                   
Cmdlet          Set-ADAccountControl                               ActiveDirectory                                                                     
Cmdlet          Set-Alias                                          Microsoft.PowerShell.Utility                                                        
Cmdlet          Set-AppLockerPolicy                                AppLocker                                                                           
Cmdlet          Set-CimInstance                                    CimCmdlets                                                                          
Cmdlet          Set-ExecutionPolicy                                Microsoft.PowerShell.Security                                                       
Cmdlet          Set-JobTrigger                                     PSScheduledJob                                                                      
Cmdlet          Set-MsolAdministrativeUnit                         MSonline                                                                            
Cmdlet          Set-MsolAdministrativeUnit                         MSOnlineExtended                                                                    
Cmdlet          Start-BitsTransfer                                 BitsTransfer                                                                        
Cmdlet          Start-DscConfiguration                             PSDesiredStateConfiguration                                                         
Cmdlet          Test-PSSessionConfigurationFile                    Microsoft.PowerShell.Core                                                           
Cmdlet          Test-WSMan                                         Microsoft.WSMan.Management                                                          
Cmdlet          Unlock-ADAccount                                   ActiveDirectory                                                                     
Cmdlet          Write-EventLog                                     Microsoft.Powershell.Management                                                     
Cmdlet          Write-Host                                         Microsoft.PowerShell.Utility 
...
[Tailored the list]
```
Also, the commands can be retrieved in terms of `Name`, `Verb`, `Noun`, `Module`,...

PowerShell also possesses a strong and unique feature called `piping`, which we can discuss under the `piping` section.

### 2.6 Getting Help in PowerShell
Once the command to work is known using `Get-Command`, the usage and syntax of that particular cmdlet can be learned using `Get-Help`. 

To get the help for a particular cmdlet, say `clear-Host`, 
```
PS C:\> Get-Help -Name clear-Host 

NAME
    Clear-Host
    
SYNOPSIS
    Clears the display in the host program.
    
    
SYNTAX
    Clear-Host [<CommonParameters>]
    
    
DESCRIPTION
    The Clear-Host function removes all text from the current display, including commands and output that might have accumulated. When complete, it 
    displays the command prompt. You can use the function name or its alias, CLS.
    
    Clear-Host affects only the current display. It does not delete saved results or remove any items from the session. Session-specific items, such 
    as variables and functions, are not affected by this function.
    
    Because the behavior of the Clear-Host function is determined by the host program, Clear-Host might work differently in different host programs.
    

RELATED LINKS
    Online version: http://technet.microsoft.com/library/hh852689(v=wps.630).aspx
    Get-Host 
    Out-Host 
    Read-Host. Write-Host 

REMARKS
    To see the examples, type: "get-help Clear-Host -examples".
    For more information, type: "get-help Clear-Host -detailed".
    For technical information, type: "get-help Clear-Host -full".
    For online help, type: "get-help Clear-Host -online"

```
Observe the  6 fields (`Name`, `Synopsis`, `syntax`, `Description`, `Related Links`, `Remarks`). These are common for all the results of `get-Help`

If usage by example is needed, 
```
PS C:\> Get-Help -Name clear-Host -Examples

NAME
    Clear-Host
    
SYNOPSIS
    Clears the display in the host program.
    
    -------------------------- EXAMPLE 1 --------------------------
    
    C:\PS>cls
    
    # Before
    
    PS C:\>Get-Process
    
    Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
    -------  ------    -----      ----- -----   ------     -- -----------
        843      33    14428      22556    99    17.41   1688 CcmExec
         44       6     2196       4964    52     0.23    692 conhost
        646      12     2332       4896    49     1.12    388 csrss
        189      11     2860       7084   114     0.66   2896 csrss
         78      11     1876       4008    42     0.22   4000 csrss
         76       7     1848       5064    54     0.08   1028 dwm
        610      41    23952      44048   208     4.40   2080 explorer
          0       0        0         24     0               0 Idle
        182      32     7692      15980    91     0.23   3056 LogonUI
        186      25     7832      16068    91     0.27   3996 LogonUI
       1272      32    11512      20432    58    25.07    548 lsass
        267      10     3536       6736    34     0.80    556 lsm
        137      17     3520       7472    61     0.05   1220 msdtc
        447      31    70316      84476   201 1,429.67    836 MsMpEng
        265      18     7136      15628   134     2.20   3544 msseces
        248      16     6476       4076    76     0.22   1592 NisSrv
        368      25    61312      65508   614     1.78    848 powershell
        101       8     2304       6624    70     0.64   3648 rdpclip
        258      15     6804      12156    50     2.65    536 services
    ...
    
    PS C:\> cls
    #After
    
    PS C:>
    
    
    Description
    
    -----------
    
    This command uses the CLS alias of Clear-Host to clear the current display.
```
To update the help (ensure proper internet connect, as it downloads from PowerShell site), 
```
PS C:\> Update-Help

PS C:\> 

```
### 2.7 Importance of Execution Policy
By default, the `Execution Policy` is set to 'Restricted'. It is recommended to change it to `Resmote Signed`.

|Execution Policy | It's importance	|
| --- | --- |
|Restricted	| You can run commands, but you can't run scripts	|
|All Signed	| You can run commands, but you can only run digitally signed scripts|
|Remote Signed | You can run commands, local scripts and only scripts downloaded from the internet if they are digitally signed|
|Unrestricted | You can run commands and scripts with or without digital signatures|
|Bypass | Nothing is blocked and there are no warnings or prompts|

In windows menu, type `Windows PowerShell`, right-click on it and click `Run as Administrator`. Then type the below command to the `ExecutionPolicy` on that machine for that user. 
```
PS C:\> Get-ExecutionPolicy
Restricted
```
By default, it will give the execution policy associated with the user who executed this command.
```
PS C:\> Get-ExecutionPolicy -Scope CurrentUser
Restricted
```
Also, replace the `CurrentUser` in the above command with a specific username on that machine, to know the execution policy associated with that user.

To Change the execution policy, to say `unrestricted`,  
```
PS C:\> Set-ExecutionPolicy -ExecutionPolicy "unrestricted" -Scope CurrentUser

Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
http://go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
PS C:\>

```
## 3. Working with PowerShell
### 3.1 Getting Started
As it is customary to start with 'Hello world' when learning any language, Lets start with it.

```bash

PS C:\> Write-Host "Hello World!"
Hello World!
PS C:\> Write-Host 'Hello World!'
Hello World!
PS C:\> 'Hello World!'
Hello World!
```
Observe that the string 'Hello World!' is printed on the console in three ways. But, single (') and double(") quotes won't work exactly same in all cases. we can discuss about it in later section. 

Single-line comment
```bash
PS C:\> # Comments begin with a # (aka hashtag or pound sign)
PS C:\>
```
Multi-line comment
```
PS C:\> <#
>>   Comment blocks use angle brackets with comment sign
>>   They can be multiline
>> #>
PS C:\>
```
Regions are not logical, but representational blocks of code. 

__NOTE:__ Regions have their importance in powershell ISE only. They are used to divide the script into logical code blocks. 

```
PS C:\> #region
PS C:\>   # Put your code here
PS C:\> #endregion
PS C:\>
```
These regions can also be named.
```
PS C:\> #region The Region Title is Optional
PS C:\>
PS C:\> # some code here
PS C:\>
PS C:\> #endregion The Region Title is Optional
PS C:\>
```

**Special Characters in PowerShell**

|Special Character	| Meaning|
| --- | --- |
|" | The beginning( or end) of quoted text. Used to represent strings |
|' | The beginning( or end) of quoted text. Used to represent strings. special characters lose their significance within single quotes|
|# | The beginning of a comment   | 
|$ | The beginning of a variable  | 
|& | Reserved for future use  | 
|()| Parentheses used for subexpressions| 
|{}| Script block | 
|; | Statement Separator  |
|&#124; | Pipeline seperator|
|` |  Escape Character|
|? |  Alias operator for Where-Object|
|% |  Alias Operator for for-loop|

All variables start with a $.
```
PS C:\> $hi = "Hello World"
```
Printing the value in variable
```
PS C:\> $hi
Hello World
```
This is a shortcut to Write-Host
```
PS C:\> Write-Host $hi
Hello World
```
Variables are objects, and to get their data type, 
```
PS C:\> $hi.GetType()

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     True     String                                   System.Object
```

__GetType()__ is one method, applicable on '$hi' object

To display all the members of this variable (object)
```
PS C:\> $hi | Get-Member


   TypeName: System.String

Name             MemberType            Definition
----             ----------            ----------
Clone            Method                System.Object Clone(), System.Object ICloneable.Clone()
CompareTo        Method                int CompareTo(System.Object value), int CompareTo(string strB), int IComparab...
Contains         Method                bool Contains(string value)
CopyTo           Method                void CopyTo(int sourceIndex, char[] destination, int destinationIndex, int co...
EndsWith         Method                bool EndsWith(string value), bool EndsWith(string value, System.StringCompari...
Equals           Method                bool Equals(System.Object obj), bool Equals(string value), bool Equals(string...
GetEnumerator    Method                System.CharEnumerator GetEnumerator(), System.Collections.IEnumerator IEnumer...
GetHashCode      Method                int GetHashCode()
GetType          Method                type GetType()
GetTypeCode      Method                System.TypeCode GetTypeCode(), System.TypeCode IConvertible.GetTypeCode()
IndexOf          Method                int IndexOf(char value), int IndexOf(char value, int startIndex), int IndexOf...
IndexOfAny       Method                int IndexOfAny(char[] anyOf), int IndexOfAny(char[] anyOf, int startIndex), i...
Insert           Method                string Insert(int startIndex, string value)
IsNormalized     Method                bool IsNormalized(), bool IsNormalized(System.Text.NormalizationForm normaliz...
LastIndexOf      Method                int LastIndexOf(char value), int LastIndexOf(char value, int startIndex), int...
LastIndexOfAny   Method                int LastIndexOfAny(char[] anyOf), int LastIndexOfAny(char[] anyOf, int startI...
Normalize        Method                string Normalize(), string Normalize(System.Text.NormalizationForm normalizat...
PadLeft          Method                string PadLeft(int totalWidth), string PadLeft(int totalWidth, char paddingChar)
PadRight         Method                string PadRight(int totalWidth), string PadRight(int totalWidth, char padding...
Remove           Method                string Remove(int startIndex, int count), string Remove(int startIndex)
Replace          Method                string Replace(char oldChar, char newChar), string Replace(string oldValue, s...
Split            Method                string[] Split(Params char[] separator), string[] Split(char[] separator, int...
StartsWith       Method                bool StartsWith(string value), bool StartsWith(string value, System.StringCom...
Substring        Method                string Substring(int startIndex), string Substring(int startIndex, int length)
ToBoolean        Method                bool IConvertible.ToBoolean(System.IFormatProvider provider)
ToByte           Method                byte IConvertible.ToByte(System.IFormatProvider provider)
ToChar           Method                char IConvertible.ToChar(System.IFormatProvider provider)
ToCharArray      Method                char[] ToCharArray(), char[] ToCharArray(int startIndex, int length)
ToDateTime       Method                datetime IConvertible.ToDateTime(System.IFormatProvider provider)
ToDecimal        Method                decimal IConvertible.ToDecimal(System.IFormatProvider provider)
ToDouble         Method                double IConvertible.ToDouble(System.IFormatProvider provider)
ToInt16          Method                int16 IConvertible.ToInt16(System.IFormatProvider provider)
ToInt32          Method                int IConvertible.ToInt32(System.IFormatProvider provider)
ToInt64          Method                long IConvertible.ToInt64(System.IFormatProvider provider)
ToLower          Method                string ToLower(), string ToLower(cultureinfo culture)
ToLowerInvariant Method                string ToLowerInvariant()
ToSByte          Method                sbyte IConvertible.ToSByte(System.IFormatProvider provider)
ToSingle         Method                float IConvertible.ToSingle(System.IFormatProvider provider)
ToString         Method                string ToString(), string ToString(System.IFormatProvider provider), string I...
ToType           Method                System.Object IConvertible.ToType(type conversionType, System.IFormatProvider...
ToUInt16         Method                uint16 IConvertible.ToUInt16(System.IFormatProvider provider)
ToUInt32         Method                uint32 IConvertible.ToUInt32(System.IFormatProvider provider)
ToUInt64         Method                uint64 IConvertible.ToUInt64(System.IFormatProvider provider)
ToUpper          Method                string ToUpper(), string ToUpper(cultureinfo culture)
ToUpperInvariant Method                string ToUpperInvariant()
Trim             Method                string Trim(Params char[] trimChars), string Trim()
TrimEnd          Method                string TrimEnd(Params char[] trimChars)
TrimStart        Method                string TrimStart(Params char[] trimChars)
Chars            ParameterizedProperty char Chars(int index) {get;}
Length           Property              int Length {get;}
```
Using some of those members
```
PS C:\> $hi.ToLower()
hello world

PS C:\> $hi.ToUpper()
HELLO WORLD

PS C:\> $hi.Length # No () as it is Property; not method
11

PS C:\> $hi.Replace("World", "PowerShell")
Hello PowerShell

```
Types are mutable. Their data types can also be changed
```

PS C:\> $hi = 5

PS C:\> $hi.GetType()

IsPublic IsSerial Name                                     BaseType                                                         
-------- -------- ----                                     --------                                                         
True     True     Int32                                    System.ValueType                                                 
PS C:\> $hi | Get-Member


   TypeName: System.Int32

Name        MemberType Definition                                                                                           
----        ---------- ----------                                                                                           
CompareTo   Method     int CompareTo(System.Object value), int CompareTo(int value), int IComparable.CompareTo(System.Obj...
Equals      Method     bool Equals(System.Object obj), bool Equals(int obj), bool IEquatable[int].Equals(int other)         
GetHashCode Method     int GetHashCode()                                                                                    
GetType     Method     type GetType()                                                                                       
GetTypeCode Method     System.TypeCode GetTypeCode(), System.TypeCode IConvertible.GetTypeCode()                            
ToBoolean   Method     bool IConvertible.ToBoolean(System.IFormatProvider provider)                                         
ToByte      Method     byte IConvertible.ToByte(System.IFormatProvider provider)                                            
ToChar      Method     char IConvertible.ToChar(System.IFormatProvider provider)                                            
ToDateTime  Method     datetime IConvertible.ToDateTime(System.IFormatProvider provider)                                    
ToDecimal   Method     decimal IConvertible.ToDecimal(System.IFormatProvider provider)                                      
ToDouble    Method     double IConvertible.ToDouble(System.IFormatProvider provider)                                        
ToInt16     Method     int16 IConvertible.ToInt16(System.IFormatProvider provider)                                          
ToInt32     Method     int IConvertible.ToInt32(System.IFormatProvider provider)                                            
ToInt64     Method     long IConvertible.ToInt64(System.IFormatProvider provider)                                           
ToSByte     Method     sbyte IConvertible.ToSByte(System.IFormatProvider provider)                                          
ToSingle    Method     float IConvertible.ToSingle(System.IFormatProvider provider)                                         
ToString    Method     string ToString(), string ToString(string format), string ToString(System.IFormatProvider provider...
ToType      Method     System.Object IConvertible.ToType(type conversionType, System.IFormatProvider provider)              
ToUInt16    Method     uint16 IConvertible.ToUInt16(System.IFormatProvider provider)                                        
ToUInt32    Method     uint32 IConvertible.ToUInt32(System.IFormatProvider provider)                                        
ToUInt64    Method     uint64 IConvertible.ToUInt64(System.IFormatProvider provider)                                        
```
Variables can also be **strongly-typed**. 
```
PS C:\> [System.Int32]$myint = 42  

PS C:\> $myint
42

PS C:\> $myint.GetType()

IsPublic IsSerial Name                                     BaseType                                                         
-------- -------- ----                                     --------                                                         
True     True     Int32                                    System.ValueType                                                 
PS C:\> $myint = "This won't work"
Cannot convert value "This won't work" to type "System.Int32". Error: "Input string was not in a correct format."
At line:1 char:1
+ $myint = "This won't work"
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : MetadataError: (:) [], ArgumentTransformationMetadataException
    + FullyQualifiedErrorId : RuntimeException
```
There are shortcuts for most .NET data types.
```
PS C:\> [int] $myotherint = 42

PS C:\> $myotherint.GetType()

IsPublic IsSerial Name                                     BaseType                                                         
-------- -------- ----                                     --------                                                         
True     True     Int32                                    System.ValueType                                                 
PS C:\> [string] $mystring="PowerShell"

PS C:\> $mystring.GetType()

IsPublic IsSerial Name                                     BaseType                                                         
-------- -------- ----                                     --------                                                         
True     True     String                                   System.Object                                                    
```
Others include short, float, decimal, single, bool, byte, etc.

Not just variables have types - so do static values.
```
PS C:\> "PowerShell Rocks".GetType()

IsPublic IsSerial Name                                     BaseType                                                         
-------- -------- ----                                     --------                                                         
True     True     String                                   System.Object                                                    

```
Accessing methods on objects
```
PS C:\> "PowerShell Rocks".ToUpper()
POWERSHELL ROCKS

PS C:\> "PowerShell Rocks".Contains("PowerShell")
True
```
For non-strings you need to wrap in () so PS will evaluate as an object.
```
PS C:\> (33).GetType()  

IsPublic IsSerial Name                                     BaseType                                                         
-------- -------- ----                                     --------                                                         
True     True     Int32                                    System.ValueType                                                 

```
#### Logical Operations

|Operator	| Importance	|
| --- | --- |
| -eq	| Equal to	|
| -ne	| Not equal to|
| -lt   |     Less Than|
| -gt   |     Greater then|
| -le   |     Less than or equal to|
| -ge   |     Greater then or equal to|
|
| -in   |     See if value in an array|
| -Like |     Like wildcard pattern matching|
| -NotLike |  Not Like |
| -Match   |  Matches based on regular expressions|
| -NotMatch | Non-Matches based on regular expressions|
```
PS C:\> $var = 33

PS C:\> $var -gt 30
True

PS C:\> $var -lt 30
False

PS C:\> $var -eq 33
True
```
Calculations are like any other language.
```
PS C:\> $var = 3 * 11  # Also uses +, -, and / 

PS C:\> $var 
33
```
Supports post unary operators ++ and --
```
PS C:\> $var++ 

PS C:\> $var
34
```
And pre unary operators as well
```
PS C:\> ++$var 

PS C:\> $var
35

PS C:\> $var = 33

PS C:\> $post = $var++

PS C:\> write-Host $post, $var
33 34

PS C:\> 
PS C:\> $var = 33

PS C:\> $pre = ++$var

PS C:\> write-Host $pre, $var 
34 34
```
Be __cautious__ of __Implicit__ Type Conversions
```
PS C:\> "42" -eq 42
True

PS C:\> 42 -eq "42"
True
```
Whatever is on the right is converted to the data type on the left can lead to some odd conversions.
```
PS C:\> 42 -eq "042"   # True because the string on the right is coverted to an int
True

PS C:\> "042" -eq 42   # False because int on the right is converted to a string
False 
```
#### Built in variables
```bash
PS C:\> # Booleans ( False and true)

PS C:\> $false
False

PS C:\> $true
True

PS C:\> $NULL # null type

PS C:\> Write-Host $NuLL
```
Observe that nothing is display; even methods like GetType() doesn't work on this object.

To get the current working directory, 
```
PS C:\> $pwd

Path
----
C:\ 
```
To get the Users Home Directory,
```
PS C:\> $Home  
C:\Users\praud01
```
Information about a users scripting environment
```
PS C:\> $host  # It is alias for Get-Host


Name             : Windows PowerShell ISE Host
Version          : 5.0.10586.672
InstanceId       : 4e61fcaa-4155-4b95-aaa9-1b9c3186ed82
UI               : System.Management.Automation.Internal.Host.InternalHostUserInterface
CurrentCulture   : en-US
CurrentUICulture : en-US
PrivateData      : Microsoft.PowerShell.Host.ISE.ISEOptions
DebuggerEnabled  : True
IsRunspacePushed : False
Runspace         : System.Management.Automation.Runspaces.LocalRunspace

PS C:\> 

PS C:\> $PID     # It results the process ID
12844
```
Info about the current version of Powershell
```
PS C:\> $PSVersionTable

Name                           Value                                                                                        
----                           -----                                                                                        
PSVersion                      5.0.10586.672                                                                                
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}                                                                      
BuildVersion                   10.0.10586.672                                                                               
CLRVersion                     4.0.30319.42000                                                                              
WSManStackVersion              3.0                                                                                          
PSRemotingProtocolVersion      2.3                                                                                          
SerializationVersion           1.1.0.1                                                                                      



PS C:\> $_   # Current Object; Used in loops to get the iterating object.

PS C:\> # Useful, mainly, in loops and exceptions

PS C:\> Set-Location "C:\Python27\Scripts"

PS C:\Python27\Scripts> # set-Location works in the same way as chdir

PS C:\Python27\Scripts> Get-ChildItem | Where-Object {$_.Name -like "*.cmd"}


    Directory: C:\Python27\Scripts


Mode                LastWriteTime         Length Name                                                                       
----                -------------         ------ ----                                                                       
-a----        08-Mar-17   4:00 AM           1432 aws.cmd                                                                    
-a----        08-Mar-17   4:05 AM             24 hjson.cmd                                                                  
-a----        24-Jan-17   5:59 PM            151 wmitest.cmd                                                                



PS C:\Python27\Scripts> set-location c:\ 

PS C:\> 
```
#### Using the *-Variable cmdlets
```bash
PS C:\> # Normal variable usage

PS C:\> $normal = 33

PS C:\> $normal
33

PS C:\> $text = "In The Morning"

PS C:\> $text 
In The Morning

PS C:\> # Long version of $var1 = 33

PS C:\> New-Variable -Name var1 -Value 33

PS C:\> $var1
33
```
__NOTE:__ If you try to use New-Variable and it already exists, you get an error.

Try again with $var1 already existing.
```
PS C:\> New-Variable -Name var1 -Value 99
New-Variable : A variable with name 'var1' already exists.
At line:1 char:1
+ New-Variable -Name var1 -Value 99
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ResourceExists: (var1:String) [New-Variable], SessionStateException
    + FullyQualifiedErrorId : VariableAlreadyExists,Microsoft.PowerShell.Commands.NewVariableCommand
 

PS C:\> $var1
33

PS C:\> # Displays the variable and it's value

PS C:\> Get-Variable var -valueonly
34

PS C:\> Get-Variable var

Name                           Value                                                                                        
----                           -----                                                                                        
var                            34                                                                                           

PS C:\> Get-Variable   # Without params it shows all variables

Name                           Value                                                                                        
----                           -----                                                                                        
$                              var                                                                                          
?                              True                                                                                         
^                              Get-Variable                                                                                 
APM_DATAPOINT_SOURCE           public class APM_DATAPOINT_CLASS {...                                                        
args                           {}                                                                                           
ATC_BASIC_ATTRIB_LIST          {name, applicationName, backendName, components...}                                          
ATC_DO_NOT_PUBLISH_ATTRIB_LIST {name, applicationName, backendName, components...}                                          
AWS_APM_XML_FILE               \DefaultValues.xml                                                                           
AWS_GLOBAL_VAR_FILE            \AWSGlobalVariables.ps1                                                                      
btn                            System.Windows.Forms.Button, Text:                                                           
CLWORKSTATION_JAR_PATH         \CLWorkstation.jar                                                                           
CONFIG_CLASS_SOURCE            public class CONFIG_CLASS {...                                                               
ConfirmPreference              High                                                                                         
ConsoleFileName                                                                                                             
CW_ALARM_SOURCE                public class CW_ALARM_CLASS {...                                                             
CW_METRIC_SOURCE               public class CW_METRIC_CLASS {...                                                            
DebugPreference                SilentlyContinue                                                                             
EC2_CLASS_SOURCE               public class EC2_CLASS {...                                                                  
Error                          {A variable with name 'var1' already exists., A variable with name 'var' already exists., ...
ErrorActionPreference          Continue                                                                                     
ErrorView                      NormalView                                                                                   
ExecutionContext               System.Management.Automation.EngineIntrinsics                                                
false                          False                                                                                        
foreach                                                                                                                     
form                           System.Windows.Forms.Form, Text:                                                             
FormatEnumerationLimit         4                                                                                            
hi                             5                                                                                            
HOME                           C:\Users\praud01                                                                             
Host                           System.Management.Automation.Internal.Host.InternalHost                                      
i                              22                                                                                           
InformationPreference          SilentlyContinue                                                                             
input                          System.Collections.ArrayList+ArrayListEnumeratorSimple                                       
Matches                        {0}                                                                                          
MaximumAliasCount              4096                                                                                         
MaximumDriveCount              4096                                                                                         
MaximumErrorCount              256                                                                                          
MaximumFunctionCount           4096                                                                                         
MaximumHistoryCount            4096                                                                                         
MaximumVariableCount           4096                                                                                         
myint                          42                                                                                           
MyInvocation                   System.Management.Automation.InvocationInfo                                                  
myotherint                     42                                                                                           
mystring                       PowerShell                                                                                   
NestedPromptLevel              0                                                                                            
normal                         33                                                                                           
null                                                                                                                        
OutputEncoding                 System.Text.SBCSCodePageEncoding                                                             
path                                                                                                                        
PID                            12844                                                                                        
Playlisturl                    https://www.youtube.com/watch?v=yKstEJKdc4o                                                  
post                           33                                                                                           
pre                            34                                                                                           
processName                                                                                                                 
profile                        C:\Users\praud01\Documents\WindowsPowerShell\Microsoft.PowerShellISE_profile.ps1             
ProgressPreference             Continue                                                                                     
PSBoundParameters              {}                                                                                           
PSCommandPath                                                                                                               
PSCulture                      en-US                                                                                        
PSDefaultParameterValues       {}                                                                                           
PSEmailServer                                                                                                               
PSHOME                         C:\Windows\System32\WindowsPowerShell\v1.0                                                   
psISE                          Microsoft.PowerShell.Host.ISE.ObjectModelRoot                                                
PSScriptRoot                                                                                                                
PSSessionApplicationName       wsman                                                                                        
PSSessionConfigurationName     http://schemas.microsoft.com/powershell/Microsoft.PowerShell                                 
PSSessionOption                System.Management.Automation.Remoting.PSSessionOption                                        
PSUICulture                    en-US                                                                                        
psUnsupportedConsoleApplica... {wmic, wmic.exe, cmd, cmd.exe...}                                                            
PSVersionTable                 {PSVersion, PSCompatibleVersions, BuildVersion, CLRVersion...}                               
PWD                            C:\                                                                                          
ShellId                        Microsoft.PowerShell                                                                         
StackTrace                        at CallSite.Target(Closure , CallSite , Object )...                                       
talkIt                         System.__ComObject                                                                           
text                           In The Morning                                                                               
true                           True                                                                                         
var                            34                                                                                           
var1                           33                                                                                           
VerbosePreference              SilentlyContinue                                                                             
video                          @{innerText=9:53; URL=http://www.youtube.com/watch?v=6VK4TN6Umfk}                            
VideoUrls                      {@{innerText=5:08; URL=http://www.youtube.com/watch?v=GpLUAhoj9XQ}, @{innerText=4:19; URL=...
WarningPreference              Continue                                                                                     
WhatIfPreference               False                                                                                        
XML_CONFIG_OBJECT              CONFIG_CLASS                                                                                 
```
Assigning a new value to an existing variable

Method 1:
```
PS C:\> $var1 = "In The Morning"
```
Method 2:
```
PS C:\> Set-Variable -Name var1 -Value "In The Morning"

PS C:\> $var1
In The Morning

PS C:\> Set-Variable -Name var99 -Value "In The Morning"
```
Observe that set-variable works on objects that aren't created yet.

To clear the contents of a variable,
```
PS C:\> Clear-Variable -Name var1  # Same as $var1 = $null

PS C:\> $var1

PS C:\> 

```
To set the variable to null object,
```
PS C:\> $var1 -eq $null
True

```
Even though the object contains null, it still exists.
```
PS C:\> Get-Variable var1

Name                           Value                                                                                        
----                           -----                                                                                        
var1                                                                                                                        

```
## 4. Working with Strings
String Quoting
```bash
PS C:\> "This is a string"
This is a string
PS C:\> 'This is a string too!'
This is a string too!
```
Mixed quoted
```
PS C:\> 'I just wanted to say "Hello World", OK?'
I just wanted to say "Hello World", OK?
PS C:\> "I can't believe how cool Powershell is!"
I can't believe how cool Powershell is!
```
You can also double quote to get quotes in strings
```
PS C:\> "I just wanted to say ""Hello World"", OK?"
I just wanted to say "Hello World", OK?
PS C:\> 'I can''t believe how cool Powershell is!'
I can't believe how cool Powershell is!
```
Escape Sequences - use the backtick `

backspace `b (does not work in ISE, only the regular script window)
```
PS C:\> "Power`bShell"
PoweShell
```
newline `n
```
PS C:\> "Power`nShell"
Power
Shell
```
carriage return `r (doesn't really show anything)
```
PS C:\> "Power`rShell"
Shell
```
crlf `r`n
```
PS C:\> "Power`r`nShell"
Power
Shell
```
tabs
```
PS C:\> "Power`tShell"
Power   Shell
```
.Replace is case-sensitive
```
PS C:\> 'Hello wOrld'.Replace('o', '1')
Hell1 wOrld
```
-Replace is case-insentive
```
PS C:\> 'Hello wOrld' -Replace 'o', '1'
Hell1 w1rld
```
But, we need to be careful when working with special characters.
```
PS C:\> 'Hello wOrld.'.Replace('.', '1')                    # Replaces only the dot(.) character
Hello wOrld1
PS C:\> 'Hello wOrld.' -Replace '.', '1'                    # Replaced the complete string. Assumes '.'  as regex character
111111111111
PS C:\>
PS C:\> 'Hello wOrld.' -Replace [Regex]::Escape('.'), '1'   # To escape a regex character
Hello wOrld1
PS C:\> 'Hello wOrld.' -Replace '\.', '1'                   # Regex characters can also be escaped with '\'
Hello wOrld1
PS C:\> 'Hello wOrld\' -Replace '\\', '1'                   # '\' character will be escaped with another '\'
Hello wOrld1
```
`Here Strings` are used when working with large blocks of text.
```
PS C:\> $heretext = @"
>> Some text here
>> Some more here
>>      a bit more
>>
>> a blank line above
>> "@
PS C:\> $heretext
Some text here
Some more here
     a bit more

a blank line above
```
The @ and quote must be last on starting line then first on ending line, also works with single quotes.
```
PS C:\> $moreheretext = @'
>> Here we go again
>> another line here
>>    let's indent this
>>
>> a blank line above
>> '@
```
Note how the nested ' is handled OK, no double quoting needed.
```
PS C:\> $moreheretext
Here we go again
another line here
   let's indent this

a blank line above
PS C:\>
```
To understand the importance of here strings, lets work with a multiple line string.

Without here strings
```
PS C:\> $sql = 'SELECT col1' `
>>      + '     , col2' `
>>      + '     , col3' `
>>      + '  FROM someTable ' `
>>      + ' WHERE col1 = ''a value'' '
PS C:\>
PS C:\> $sql
SELECT col1     , col2     , col3  FROM someTable  WHERE col1 = 'a value'
```
With here strings
```
PS C:\> $sql = @'
>> SELECT col1
>>      , col2
>>      , col3
>>   FROM someTable
>>  WHERE col1 = 'a value'
>> '@
PS C:\> $sql
SELECT col1
     , col2
     , col3
  FROM someTable
 WHERE col1 = 'a value'
```
#### String Interpolation
```
PS C:\> Set-Location C:\Python27\Scripts\
```
Take the output of Get-ChildItem, which is an object, and gets that objects count property.
```
PS C:\Python27\Scripts> $items = (Get-ChildItem).Count
PS C:\Python27\Scripts> $items
207
```
Take the output of Get-Location and store it in a variable.
```
PS C:\Python27\Scripts> $loc = Get-Location
PS C:\Python27\Scripts> $loc

Path
----
C:\Python27\Scripts

```
Use these variables in a string
```
PS C:\Python27\Scripts> "There are $items items are in the folder $loc."
There are 207 items are in the folder C:\Python27\Scripts.
```
To actually display the variable, escape it with a backtick, 
```
PS C:\Python27\Scripts> "There are `$items items are in the folder `$loc."
There are $items items are in the folder $loc.
```
String interpolation only works with double quotes
```
PS C:\Python27\Scripts> 'There are $items items are in the folder $loc.'
There are $items items are in the folder $loc.
```
String Interpolation works with here strings
```
PS C:\Python27\Scripts> $hereinterpolation = @"
>> Items`tFolder
>> -----`t----------------------
>> $items`t`t$loc
>>
>> "@
PS C:\Python27\Scripts> $hereinterpolation
Items   Folder
-----   ----------------------
207             C:\Python27\Scripts

PS C:\Python27\Scripts> $hereinterpolation = @'
>> Items`tFolder
>> -----`t----------------------
>> $items`t`t$loc
>>
>> '@
PS C:\Python27\Scripts>
PS C:\Python27\Scripts> $hereinterpolation
Items`tFolder
-----`t----------------------
$items`t`t$loc

```
Observe that it didn't work for here strings defined with single quotes.

Expressions used within strings, need to be wrapped in $().
```
PS C:\Python27\Scripts> "There are $((Get-ChildItem).Count) items are in the folder $(Get-Location)."
There are 207 items are in the folder C:\Python27\Scripts.

PS C:\Python27\Scripts> "Today is $(Get-Date). Be well."
Today is 05/03/2017 12:43:17. Be well.

PS C:\Python27\Scripts> "The 15% tip of a 33.33 dollar bill is $(33.33 * 0.15) dollars"
The 15% tip of a 33.33 dollar bill is 4.9995 dollars
```
String Formatting - C# like syntax is supported. In C# you'd use:
```
PS C:\Python27\Scripts> [string]::Format("There are {0} items.", $items)
There are 207 items.
```
Powershell shortcut
```
PS C:\Python27\Scripts> "There are {0} items." -f $items
There are 207 items.

PS C:\Python27\Scripts> "There are {0} items in the location {1}." -f $items, $loc
There are 207 items in the location C:\Python27\Scripts.

PS C:\Python27\Scripts> "There are {0} items in the location {1}. Wow, {0} is a lot of items!" -f $items, $loc
There are 207 items in the location C:\Python27\Scripts. Wow, 207 is a lot of items!

```
#### Pre-defined formats
>- N - Numbers
>- C - Currency
>- P - Percentage
>- X - Hex
>- D - Decimal

`N - Number`
```
PS C:\> "N0 {0:N0} formatted" -f 12345678.119
N0 12,345,678 formatted
PS C:\> "N1 {0:N1} formatted" -f 12345678.119
N1 12,345,678.1 formatted
PS C:\> "N2 {0:N2} formatted" -f 12345678.119
N2 12,345,678.12 formatted
PS C:\> "N2 {0:N9} formatted" -f 12345678.119
N2 12,345,678.119000000 formatted
PS C:\> "N0 {0:N0} formatted"   -f 123.119
N0 123 formatted
PS C:\> "N0 {0,8:N0} formatted" -f 123.119
N0      123 formatted
```
`C - Currency`
```
PS C:\> "C0 {0:C0} formatted" -f 12345678.1234
C0 $12,345,678 formatted
PS C:\> "C1 {0:C1} formatted" -f 12345678.1234
C1 $12,345,678.1 formatted
PS C:\> "C2 {0:C2} formatted" -f 12345678.1234
C2 $12,345,678.12 formatted
```
`P - Percentage`
```
PS C:\> "P0 {0:P0} formatted" -f 0.1234
P0 12 % formatted
PS C:\> "P2 {0:P2} formatted" -f 0.1234
P2 12.34 % formatted
```
`X - Hex`
```
PS C:\> "X0 0x{0:X0} formatted" -f 1234
X0 0x4D2 formatted
PS C:\> "X0 0x{0:X0} formatted" -f 0x4D2
X0 0x4D2 formatted
```
`D - Decimal`
```
PS C:\> "D0 {0:D0} formatted"   -f 12345678
D0 12345678 formatted
PS C:\> "D8 {0:D8} formatted"   -f 123
D8 00000123 formatted
PS C:\> "D0 {0:D0} formatted"   -f 123
D0 123 formatted
PS C:\> "D0 {0,8:D0} formatted" -f 123
D0      123 formatted
```
Note, decimal only supports ints. This causes an error:
```
PS C:\> "D0 {0:D0} formatted"   -f 123.1
Error formatting a string: Format specifier was invalid..
At line:1 char:1
+ "D0 {0:D0} formatted"   -f 123.1
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (D0 {0:D0} formatted:String) [], RuntimeExcep
    + FullyQualifiedErrorId : FormatError
```
#### Custom formatting
```
PS C:\> $items = 1234
PS C:\> "There are {0:#,#0} items." -f $items
There are 1,234 items.
PS C:\> "Custom 0, 25 $#,##0.0000  = {0,25:$ #,##0.0000} " -f 123456789.012000005
Custom 0, 25 $#,##0.0000  =        $ 123,456,789.0120
PS C:\> "Custom 0, 25 $#,##0.0000  = {0,25:$ #,##0.00} "   -f 123456789.012000005
Custom 0, 25 $#,##0.0000  =          $ 123,456,789.01
PS C:\> "Custom 0, 25 $#,##0.0000  = {0,25:$ #,##0.00} "   -f 123456789.012000005
Custom 0, 25 $#,##0.0000  =          $ 123,456,789.01

PS C:\> "Custom 0, 10 #,##0%    = {0,10:#,##0%} "    -f 0.125
Custom 0, 10 #,##0%    =        13%
PS C:\> "Custom 0, 10 #,##0.00% = {0,10:#,##0.00%} " -f 0.125
Custom 0, 10 #,##0.00% =     12.50%
PS C:\>
```
#### Date String Formatting
* MM - Month
* mm - minute 

Custom date formatting. Note MM is Month, mm is minute
```bash
PS C:\> "Today is {0:M/d/yyyy}. Be well."               -f $(Get-Date)              # Today is 3/13/2014. Be well.
Today is 5-3-2017. Be well.

PS C:\> "Today is {0,10:MM/dd/yyyy}. Be well."          -f $(Get-Date)              # Today is 03/13/2014. Be well.
Today is 05-03-2017. Be well.

PS C:\> "Today is {0,10:yyyyMMdd}. Be well."            -f $(Get-Date)              # Today is   20140313. Be well.
Today is   20170503. Be well.

PS C:\> "Today is {0,10:MM/dd/yyyy hh:mm:ss}. Be well." -f $(Get-Date)              # Today is 03/13/2014 12:21:19. Be well.
Today is 05-03-2017 03:51:54. Be well.

```
#### Other formatting

Calculations can be passed in as the item to be formatted 
```bash              
PS C:\> "The 20% tip of a 33.33 dollar bill is {0} dollars" -f (33.33 * 0.20)       # The 20% tip of a 33.33 dollar bill is 6.666 dollars
The 20% tip of a 33.33 dollar bill is 6.666 dollars

PS C:\> "The 20% tip of a 33.33 dollar bill is {0:0.00} dollars" -f (33.33 * 0.20)  # The 20% tip of a 33.33 dollar bill is 6.67 dollars
The 20% tip of a 33.33 dollar bill is 6.67 dollars

```
#### String operator -like
* It works using Wildcards
```bash
PS C:\> "PowerShell" -like "Power*"
True

PS C:\> "PowerShell" -like "Python*"
False

PS C:\> "PowerShell" -like "?owerShell"  # question marks work for single characters
True

PS C:\> "PowerShell" -like "Power*[s-v]" # ends in a char between s and v
False

PS C:\> "PowerShell" -like "Power*[a-c]" # ends in a char between a and c
False

```
#### String operator -match
* It works using Regular Expressions
```bash
PS C:\> "888-368-1240" -match "[0-9]{3}-[0-9]{3}-[0-9]{4}"  
True

PS C:\> "ZZZ-368-1240" -match "[0-9]{3}-[0-9]{3}-[0-9]{4}"  
False

PS C:\> "888.368.1240" -match "[0-9]{3}-[0-9]{3}-[0-9]{4}"  
False
```
## 5. Working with Arrays
#### 5.1 Simple Arrays
Creating Array(s)
```bash
PS C:\> $array = "Narendra", "Bhahubali"

PS C:\> $array
Narendra
Bhahubali

PS C:\> $array[0]
Narendra

PS C:\> $array[1]
Bhahubali

PS C:\> $array.GetType()

IsPublic IsSerial Name                                     BaseType                                                         
-------- -------- ----                                     --------                                                         
True     True     Object[]                                 System.Array  
```
Updating Array(s)
```
PS C:\> $array = "Barack", "Obama"

PS C:\> $array
Barack
Obama

PS C:\> $array[0] = "Power"

PS C:\> $array[1] = "Shell"

PS C:\> $array
Power
Shell
```
Formal Array Creation Syntax
```
PS C:\> $array = @("Power", "Shell")

PS C:\> $array
Power
Shell
```
Only way to create an empty array
```
PS C:\> $array = @()   

PS C:\> $array.Count
0

PS C:\> $array += "jeffrey"

PS C:\> $array += "snover"

PS C:\> $array.Count
2

PS C:\> $array
jeffrey
snover

PS C:\> $array = 1..5  # Can load arrays using numeric range notation

PS C:\> $array
1
2
3
4
5

PS C:\> 
PS C:\> # Check to see if an item exists

PS C:\> $numbers = 1, 42, 256

PS C:\> $numbers -contains 42
True

PS C:\> $numbers -notcontains 99
True

PS C:\> $numbers -notcontains 42
False
```
#### 5.2 Array of Arrays
Load four individual arrays
```bash
PS C:\> $a = 1..5

PS C:\> $b = 6..10

PS C:\> $c = 11..15

PS C:\> $d = 16..20

PS C:\> write-Host "`$a = $a `n`$b = $b `n`$c = $c `n`$d = $d"
$a = 1 2 3 4 5 
$b = 6 7 8 9 10 
$c = 11 12 13 14 15 
$d = 16 17 18 19 20

``` 
Now create an array from the four individual ones
```
PS C:\> $array = $a, $b, $c, $d

PS C:\> $array
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
```
Array will now look like
```
 Col      [0] [1] [2] [3] [4]
 Row [0]   1   2   3   4   5
 Row [1]   6   7   8   9  10
 Row [2]  11  12  13  14  15
 Row [3]  16  17  18  19  20
```
Reference the second item in the second array (remember arrays are 0 based)
```
PS C:\> $array[1][2] # Zero based array, go to 2nd row, 3rd item
8
```
Take the contents of the array and join them into a single string. 
```
PS C:\> $array[0] -join " "
1 2 3 4 5

PS C:\> $array[2] -join ” “
11 12 13 14 15

PS C:\> $array[3] -join ” “
16 17 18 19 20

PS C:\> $array[1][1]
7

PS C:\> $array[3][3]
19
```
## 6. Hash tables 
```bash
PS C:\> $hash = @{"Key"         = "Value"; 
          "PowerShell"  = "PowerShell.com"; 
          "jeffrey snover" = "PowerShell Inventor"}
          

PS C:\> $hash                  # Display all values

Name                           Value                                                                                        
----                           -----                                                                                        
PowerShell                     PowerShell.com                                                                               
Key                            Value                                                                                        
jeffrey snover                 PowerShell Inventor                                                                          
```
By default, the hashes doesn't store the keys in the order of assignment. 
If we need to retain the assigned order, 
```
PS C:\> $hash1 = [ordered]@{"Key"         = "Value";
>>           "PowerShell"  = "PowerShell.com";
>>           "jeffrey snover" = "PowerShell Inventor"}
>>
PS C:\> $hash1

Name                           Value
----                           -----
Key                            Value
PowerShell                     PowerShell.com
jeffrey snover                 PowerShell Inventor

```
Values from hash key can be retrieved in two ways:
```
PS C:\> $hash["PowerShell"]      # Get a single value from the key
PowerShell.com

PS C:\> $hash."jeffrey snover"    # Get single value using object syntax
PowerShell Inventor

```
You can use variables as keys
```
PS C:\> $mykey = "PowerShell"

PS C:\> $hash.$mykey         # Using variable as a property
PowerShell.com

PS C:\> $hash.$($mykey)      # Evaluating as an expression
PowerShell.com

PS C:\> $hash.$("Power" + "Shell")
PowerShell.com

```
Adding and removing values
```
PS C:\> $hash               # Here's what's there to start

Name                           Value                                                                                        
----                           -----                        
PowerShell                     PowerShell.com               
Key                            Value                        
jeffrey snover                 PowerShell Inventor                                                                       

PS C:\> $hash["aws"] = "Amazon Web Services"  # Add value using new key

PS C:\> $hash                # Show the additional row

Name                           Value                       
----                           -----                       
PowerShell                     PowerShell.com              
aws                            Amazon Web Services         
Key                            Value                       
jeffrey snover                 PowerShell Inventor                                                                      

PS C:\> $hash.Remove("jeffrey snover")        # Remove by passing in key

PS C:\> $hash

Name                           Value                                                                                      
----                           -----                                                                                      
PowerShell                     PowerShell.com                                                                            
aws                            Amazon Web Services                                                                        
Key                            Value                                                                                      

```
See if key exists
```
PS C:\> $hash.Contains("aws")                 # Should be there
True

PS C:\> $hash.Contains("jeffrey snover")      # Gone since we just removed it
False

```
See if value exists
```
PS C:\> $hash.ContainsValue("PowerShell.com")  # Will be there
True

PS C:\> $hash.ContainsValue("PowerShell Inventor")  # Not there since it was removed
False

``` 
List keys and values
```
PS C:\> $hash.Keys
PowerShell
aws
Key

PS C:\> $hash.Values
PowerShell.com
Amazon Web Services
Value

``` 
Find if a key or value is present
```
PS C:\> $hash.Keys -contains "PowerShell"
True

PS C:\> $hash.Values -contains "PowerShell.com"
True
```
## 7. Conditional Statements and Loops
#### 7.1 if/else condition
```bash
PS C:\> $var = 2
if ($var -eq 1)  # Be sure to use -eq instead of =
{
  "If branch"
}
else
{
  "else branch"
}
else branch
```
#### 7.2 elseif 
```bash
PS C:\> $var = 2
if ($var -eq 1)
{
  "If -eq 1 branch"
}
elseif ($var -eq 2)
{
  "ElseIf -eq 2 branch"
}
else
{
  "else branch"
}
ElseIf -eq 2 branch
```
#### 7.3 Switch case
```bash
PS C:\> # Switch statement for multiple conditions
$var = 42                   # Also test with 43 and 49
switch  ($var)
{
  41 {"Forty One"}
  42 {"Forty Two"}
  43 {"Forty Three"}
  default {"default"}
}
Forty Two

PS C:\> # Will match all lines that match

PS C:\> $var = 42
switch  ($var)
{
  42 {"Forty Two"}
  "42" {"Forty Two String"}
  default {"default"}
}
Forty Two
Forty Two String
```
__Note__ that type coercion will cause both 42 lines to have a match.

To stop processing once a block is found use break
```
PS C:\> $var = 42
switch  ($var)
{
  42 {"Forty Two"; break}
  "42" {"Forty Two String"; break}
  default {"default"}
}
Forty Two
```
__Note__, if you want to put multiple commands on a single line, use a ; to separate them

Switch works with collections, looping and executing for each match
```
PS C:\> switch (3,1,2,42)
{
  1 {"One"}
  2 {"Two"}
  3 {"Three"}
  default {"The default answer"}
}
Three
One
Two
The default answer

```
String compares are case insensitive by default
```
PS C:\> switch ("PowerShell")
{
  "powershell" {"lowercase"}
  "POWERSHELL" {"uppercase"}
  "PowerShell" {"mixedcase"}
}
lowercase
uppercase
mixedcase

```
Use the -casesenstive switch to make it so
```
PS C:\> switch -casesensitive ("PowerShell")
{
  "powershell" {"lowercase"}
  "POWERSHELL" {"uppercase"}
  "PowerShell" {"mixedcase"}
}
mixedcase

```
Supports wildcards
```
PS C:\> switch -Wildcard ("Pluralsight")
{
  "plural*" {"*"}
  "?luralsight" {"?"}
  "Pluralsi???" {"???"}
}
*
?
???

```
__Note__ that it will also support regex matches.

#### 7.4 While Loop
```bash
PS C:\> # While

$i = 1
while ($i -le 5)
{
  "`$i = $i"
  $i = $i + 1
}
$i = 1
$i = 2
$i = 3
$i = 4
$i = 5

PS C:\> # While won't execute if condition is already true

$i = 6
while ($i -le 5)
{
  "`$i = $i"
  $i = $i + 1
}

```
#### 7.5 do-While
```
PS C:\> # do-while
$i = 1
do
{
  "`$i = $i"
  $i++
} while($i -le 5)
$i = 1
$i = 2
$i = 3
$i = 4
$i = 5
```
Do will always execute at least once
```
$i = 6
do
{
  "`$i = $i"
  $i++
} while($i -le 5)
$i = 6
```
Use until to make the check more positive
```
$i = 1
do
{
  "`$i = $i"
  $i++
} until($i -gt 5)
$i = 1
$i = 2
$i = 3
$i = 4
$i = 5
```
#### 7.6 for loop
```bash

PS C:\> for ($f = 0; $f -le 5; $f++)
{
  "`$f = $f"
}

$f = 0
$f = 1
$f = 2
$f = 3
$f = 4
$f = 5
```
Note the initializer can be set seperately
```
PS C:\> $f = 2
for (; $f -le 5; $f++)
{
  "`$f = $f"
}

$f = 2
$f = 3
$f = 4
$f = 5
```
Iterating over a collection 1 by 1
```
PS C:\> $array = 11,12,13,14,15   # Simple Array
for ($i=0; $i -lt $array.Length; $i++)
{
  "`$array[$i]=" + $array[$i]
}
$array[0]=11
$array[1]=12
$array[2]=13
$array[3]=14
$array[4]=15
```

#### 7.7 foreach
foreach works on a collection
```
PS C:\> $array = 11,12,13,14,15   # Simple Array
foreach ($item in $array)
{
  "`$item = $item"
}

$item = 11
$item = 12
$item = 13
$item = 14
$item = 15

PS C:\> "1KB=$(1KB)"
1KB=1024
PS C:\> "1MB=$(1MB)"
1MB=1048576
PS C:\> "1GB=$(1GB)"
1GB=1073741824
PS C:\> "1TB=$(1TB)"
1TB=1099511627776
PS C:\> "1PB=$(1PB)"
1PB=1125899906842624

PS C:\> foreach($i in @('1KB', '1MB', '1GB', '1TB', '1PB')){Write-Host "$i =$($i)"}
1KB =1KB
1MB =1MB
1GB =1GB
1TB =1TB
1PB =1PB
```

foreach works with an array of objects
```
PS C:\> foreach ($file in Get-ChildItem -Path "C:\Python27")
{
  $file.Name
}
DLLs
Doc
etc
include
Lib
libs
Scripts
share
tcl
Tools
LICENSE.txt
NEWS.txt
python.exe
pythonw.exe
README.txt
w9xpopen.exe
```
Use break to get out of the loop
```
PS C:\> foreach ($file in Get-ChildItem  -Path "C:\Python27")
{
  if ($file.Name -like "*.exe")
  {
    $file.Name
    break  # exits the loop on first hit
  }
}
python.exe
```
Use continue to skip the rest of a loop but go onto the next iteration
```
PS C:\> foreach ($file in Get-ChildItem -Path "C:\Python27")
{
  if ($file.Name -like "*.exe")
  {
    $file.Name
    continue  # exits the loop on first hit
    "More code here"
  }
  "This isn't a executable file: $file"
}
This isn't a executable file: DLLs
This isn't a executable file: Doc
This isn't a executable file: etc
This isn't a executable file: include
This isn't a executable file: Lib
This isn't a executable file: libs
This isn't a executable file: Scripts
This isn't a executable file: share
This isn't a executable file: tcl
This isn't a executable file: Tools
This isn't a executable file: LICENSE.txt
This isn't a executable file: NEWS.txt
python.exe
pythonw.exe
This isn't a executable file: README.txt
w9xpopen.exe
```
When used in a nested loop, break exits to the outer loop
```
PS C:\> foreach ($outside in 1..3)
{
  "`$outside=$outside"
  foreach ($inside in 4..6)
  {
    "    `$inside = $inside"
    break
  }
}
$outside=1
    $inside = 4
$outside=2
    $inside = 4
$outside=3
    $inside = 4
```
Use loop labels to break to a certain loop
```
PS C:\> :outsideloop foreach ($outside in 1..3)
{
  "`$outside=$outside"
  foreach ($inside in 4..6)
  {
    "    `$inside = $inside"
    break outsideloop
  }
}
$outside=1
    $inside = 4
```
Using continue inside an inner loop
```
foreach ($outside in 1..3)
{
  "`$outside=$outside"
  foreach ($inside in 4..6)
  {
    "    `$inside = $inside"
    continue
    "this will never execute as continue goes back to start of inner for loop"
    # note, because we continue to the inside loop, the above line
    # will never run but it will go thru all iterations of the inner loop
  }
}
$outside=1
    $inside = 4
    $inside = 5
    $inside = 6
$outside=2
    $inside = 4
    $inside = 5
    $inside = 6
$outside=3
    $inside = 4
    $inside = 5
    $inside = 6

PS C:\> :outsideloop foreach ($outside in 1..3)
{
  "`$outside=$outside"
  foreach ($inside in 4..6)
  {
    "    `$inside = $inside"
    continue outsideloop
    "this will never execute as continue goes back to start of inner for loop"
    # here, because we break all the way to the outer loop the last two
    # iterations (5 and 6) never run
  }
  "some more stuff here that will never run"
}

$outside=1
    $inside = 4
$outside=2
    $inside = 4
$outside=3
    $inside = 4
```
###  7.8 Script Blocks

A basic script block is code inside {}. The for (as well as other loops) execute a script block.
```bash
PS C:\> for ($f = 0; $f -le 5; $f++)
{
  "`$f = $f"
}

$f = 0
$f = 1
$f = 2
$f = 3
$f = 4
$f = 5PS C:\> for ($f = 0; $f -le 5; $f++)
{
  "`$f = $f"
}

$f = 0
$f = 1
$f = 2
$f = 3
$f = 4
$f = 5
```

A script block can exist on its own.

__NOTE:__ To put multiple commands on a single line use the ;
```bash
PS C:\> {Clear-Host; "Powershell is cool."}
Clear-Host; "Powershell is cool."
```
Executing only shows the contents of the block, doesn't execute it. 

To actually run it, use an ampersand & in front.
```
PS C:\> &{Clear-Host; "Powershell is cool."}
Powershell is cool.
```
You can store script blocks inside a variable
```
PS C:\> $cool = {Clear-Host; "Powershell is cool."}
```
Just entering the variable though only shows the contents, doesn't run it.
```
PS C:\>Clear-Host; "Powershell is cool."

PS C:\> & $cool # To actually run it, use the & character
Powershell is cool.
```
Since scripts can be put in a variable, you can do interesting things.
```
PS C:\> $cool = {"Powershell is cool."; " So is jeffrey snover"}
for ($i=0;$i -lt 3; $i++)
{ 
  &$cool;
}
Powershell is cool.
 So is jeffrey snover
Powershell is cool.
 So is jeffrey snover
Powershell is cool.
 So is jeffrey snover
```
## 8. Functions
```bash
PS C:\> $hw = {
        "Hello World"
      }

PS C:\> & $hw
Hello World
```
Functions are basically script blocks with names.
```bash
PS C:\> function Write-HelloWorld()
{
  "Hello World"
}
```
Running the above simply places the function in memory for us to use. 
To use it, call it like you would a cmdlet.
```bash
PS C:\> Write-HelloWorld
Hello World

```
When writing functions, use an approved verb. To get the list of approved verbs,
```bash
PS C:\> Get-Verb

Verb        Group         
----        -----         
Add         Common        
Clear       Common        
Close       Common        
Copy        Common        
Enter       Common        
Exit        Common        
Find        Common        
Format      Common        
Get         Common        
Hide        Common        
Join        Common        
Lock        Common        
Move        Common        
New         Common        
Open        Common        
Optimize    Common        
Pop         Common        
Push        Common        
Redo        Common        
Remove      Common        
Rename      Common        
Reset       Common        
Resize      Common        
Search      Common        
Select      Common        
Set         Common        
Show        Common        
Skip        Common        
Split       Common        
Step        Common        
Switch      Common        
Undo        Common        
Unlock      Common        
Watch       Common        
Backup      Data          
Checkpoint  Data          
Compare     Data          
Compress    Data          
Convert     Data          
ConvertFrom Data          
ConvertTo   Data          
Dismount    Data          
Edit        Data          
Expand      Data          
Export      Data          
Group       Data          
Import      Data          
Initialize  Data          
Limit       Data          
Merge       Data          
Mount       Data          
Out         Data          
Publish     Data          
Restore     Data          
Save        Data          
Sync        Data          
Unpublish   Data          
Update      Data          
Approve     Lifecycle     
Assert      Lifecycle     
Complete    Lifecycle     
Confirm     Lifecycle     
Deny        Lifecycle     
Disable     Lifecycle     
Enable      Lifecycle     
Install     Lifecycle     
Invoke      Lifecycle     
Register    Lifecycle     
Request     Lifecycle     
Restart     Lifecycle     
Resume      Lifecycle     
Start       Lifecycle     
Stop        Lifecycle     
Submit      Lifecycle     
Suspend     Lifecycle     
Uninstall   Lifecycle     
Unregister  Lifecycle     
Wait        Lifecycle     
Debug       Diagnostic    
Measure     Diagnostic    
Ping        Diagnostic    
Repair      Diagnostic    
Resolve     Diagnostic    
Test        Diagnostic    
Trace       Diagnostic    
Connect     Communications
Disconnect  Communications
Read        Communications
Receive     Communications
Send        Communications
Write       Communications
Block       Security      
Grant       Security      
Protect     Security      
Revoke      Security      
Unblock     Security      
Unprotect   Security      
Use         Other 
```
Parameters can be passed in by placing them in parenthesis.
```bash
PS C:\> function Get-Fullname($firstName, $lastName)
{
  Write-Host ($firstName + " " + $lastName)
}
```
__Note:__ when calling the function with parameters, do not use commas or ().
```bash
PS C:\> function Get-Fullname($firstName, $lastName)
{
  Write-Host ($firstName + " " + $lastName)
}

PS C:\> Get-Fullname "jeffrey" "snover"
jeffrey snover

PS C:\> 
PS C:\> $myVar = "jeffrey"

PS C:\> Get-Fullname $myVar "snover"
jeffrey snover

PS C:\> Get-Fullname $("je" + "ffrey") "snover"
jeffrey snover
```
Any changes to a paramater inside a function are scoped to that function.
```bash
PS C:\> function Set-NonRefVar($myparam)
{
  $myparam = 33
  "Inside function `$myparam = $myparam"
}

PS C:\> $myparam = 42

PS C:\> "Prior to funciton `$myparam = $myparam"
Prior to funciton $myparam = 42

PS C:\> Set-NonRefVar($myparam)
Inside function $myparam = 33

PS C:\> "After funciton `$myparam = $myparam"
After funciton $myparam = 42
```
To change a value inside a funciton, use [ref]

Passing by reference simply requires a [ref] tag before the variable

__Note__ however it turns it into an object, thus requiring the .Value syntax.
```bash
PS C:\> function Set-RefVar([ref] $myparam)
{
  $myparam.Value = 33
  "Inside function `$myparam = $($myparam.Value)"
}

PS C:\> $myparam = 42

PS C:\> "Prior to funciton `$myparam = $myparam"
Prior to funciton $myparam = 42

PS C:\> Set-RefVar ([ref] $myparam) # Must add ref to call
Inside function $myparam = 33

PS C:\> "After funciton `$myparam = $myparam"
After funciton $myparam = 33
```
__NOTE:__ Altering the value of parameters is considered poor programming practice and should be avoided. Instead use return.

```bash
PS C:\> function Get-AValue($one, $two)
{
  return $one * $two
}


PS C:\> Get-AValue 33 42
1386

PS C:\> $returnValue = Get-AValue 33 42

PS C:\> "Returned value is $returnValue"
Returned value is 1386
```
Functions also support named parameters. Simply put the name of the parameter with a -
```bash
PS C:\> $returnValue = Get-AValue -one 33 -two 42

PS C:\> "Returned value is $returnValue"
Returned value is 1386

```
With named parameters, order is no longer important.
```bash
PS C:\> $returnValue = Get-AValue -two 42 -one 33 

PS C:\> "Returned value is $returnValue"
Returned value is 1386

```
It is possible to pipeline enable your functions. These are referred to as advanced functions.
```bash
PS C:\> function Get-EXEFiles ()
{
  # The begin block executes once at the start of the function
  begin  { $retval = "Here are some EXE files: `r`n" }

  # The process block is executed once for each object being
  # passed in from the pipe
  process { 
            if ($_.Name -like "*.exe")
            { 
              $retval += "`t$($_.Name)`r`n"
              # Note this line could also be rendered as
              # $retval = $retval + "`t" + $_.Name + "`r`n" 
              # `t     Tab Character
              # `r     Carriage Return
              # `n     Line Feed
              # $( )   Tells PS to evaute the expression in () first then return it
              # $_     The current object being passed in the pipeline
              # .Name  The name property of the current object 
            }
          }
  
  # The end block executes once, after the rest of the function
  end { return $retval }          
}

PS C:\> Get-ChildItem -Path "C:\Python27\" | Get-EXEFiles
Here are some EXE files: 
	python.exe
	pythonw.exe
	Removecx_Oracle.exe
	w9xpopen.exe


PS C:\> $output = Get-ChildItem | Get-EXEFiles

PS C:\> $output.GetType()

IsPublic IsSerial Name                                     BaseType            
-------- -------- ----                                     --------            
True     True     String                                   System.Object       

PS C:\> $i = 0
foreach($f in $output)
{
  $i++
  "$i : $f"
}
1 : Here are some EXE files: 

```
To pipeline the output, push the output in the process area.
```bash
PS C:\> function Get-EXEFiles ()
{
  begin  { }

  process { 
            if ($_.Name -like "*.exe")
            { 
              $retval = "`tEXE file is $($_.Name)"
              $retval  # This is the equivalent of: return $retval
            }
          }
  
  end { }          
}

PS C:\> $output = Get-ChildItem -Path "C:\Python27" | Get-EXEFiles

PS C:\> $output.GetType()

IsPublic IsSerial Name                                     BaseType            
-------- -------- ----                                     --------            
True     True     Object[]                                 System.Array        



PS C:\> $i = 0

PS C:\> foreach($f in $output)
{
  $i++
  "$i : $f"
}

1 : 	EXE file is python.exe
2 : 	EXE file is pythonw.exe
3 : 	EXE file is Removecx_Oracle.exe
4 : 	EXE file is w9xpopen.exe

PS C:\> 
PS C:\> function Write-SomeText ()
{
  # begin  { }

  process { 
            $retval = "Here is the output: $($_)"
            $retval
          }
  
  # end { }          
}



PS C:\> Get-ChildItem -Path "C:\Python27" | Get-EXEFiles | Write-SomeText
Here is the output: 	EXE file is python.exe
Here is the output: 	EXE file is pythonw.exe
Here is the output: 	EXE file is Removecx_Oracle.exe
Here is the output: 	EXE file is w9xpopen.exe
```
Similar to original function but truly pipelined.
```bash
PS C:\> "Here are some PowerShell files: `r`n"
Here are some PowerShell files: 


PS C:\> Get-ChildItem -Path "C:\Python27"| Get-PSFiles 
Here are some PowerShell files: 

```
Advanced functions also allow parameters with extra helping hints.
```bash
PS C:\> function Get-AValue ()
{
  [CmdletBinding()]   # Needed to indicate this is an advanced function
  param (  # Begin the parameter block
         [Parameter( Mandatory = $true,
                     HelpMessage = 'Please enter value one.'
                     )]
         [int] $one,
         # Note in the second we are strongly typing, and are providing a default value
         [Parameter( Mandatory = $false,
                     HelpMessage = 'Please enter value two.'
                     )]
         [int] $two = 42
        )  # End the parameter block

  begin { }

  process { 
            return $one * $two
          }

  end { }

}
```
Example 1: pass in values
```bash
PS C:\> Get-AValue -one 33 -two 42
1386
```
Example 2: pass in value for one, take default for two
```bash
PS C:\> Get-AValue -one 33 
1386
```
Example 3: no params, will prompt for one and take default for two
```bash
PS C:\> Get-AValue 
cmdlet Get-AValue at command pipeline position 1
Supply values for the following parameters:
(Type !? for Help.)
one: 33
1386
```
Example 4: use a string for one (generates error)
```bash
PS C:\> Get-AValue -one "x"
Get-AValue : Cannot process argument transformation on parameter 'one'. Cannot 
convert value "x" to type "System.Int32". Error: "Input string was not in a 
correct format."
At line:1 char:17
+ Get-AValue -one "x"
+                 ~~~
    + CategoryInfo          : InvalidData: (:) [Get-AValue], ParameterBindingA 
   rgumentTransformationException
    + FullyQualifiedErrorId : ParameterArgumentTransformationError,Get-AValue
```
### Adding Help to Your Functions

PowerShell is possessing a robust cmdlet for help
```bash
PS C:\> Get-Help Get-ChildItem

NAME
    Get-ChildItem
    
SYNTAX
    Get-ChildItem [[-Path] <string[]>] [[-Filter] <string>] [-Include 
    <string[]>] [-Exclude <string[]>] [-Recurse] [-Depth <uint32>] [-Force] 
    [-Name] [-UseTransaction] [-Attributes <FlagsExpression[FileAttributes]> 
    {ReadOnly | Hidden | System | Directory | Archive | Device | Normal | 
    Temporary | SparseFile | ReparsePoint | Compressed | Offline | 
    NotContentIndexed | Encrypted | IntegrityStream | NoScrubData}] 
    [-Directory] [-File] [-Hidden] [-ReadOnly] [-System]  [<CommonParameters>]
    
    Get-ChildItem [[-Filter] <string>] -LiteralPath <string[]> [-Include 
    <string[]>] [-Exclude <string[]>] [-Recurse] [-Depth <uint32>] [-Force] 
    [-Name] [-UseTransaction] [-Attributes <FlagsExpression[FileAttributes]> 
    {ReadOnly | Hidden | System | Directory | Archive | Device | Normal | 
    Temporary | SparseFile | ReparsePoint | Compressed | Offline | 
    NotContentIndexed | Encrypted | IntegrityStream | NoScrubData}] 
    [-Directory] [-File] [-Hidden] [-ReadOnly] [-System]  [<CommonParameters>]
    

ALIASES
    gci
    ls
    dir
    

REMARKS
    Get-Help cannot find the Help files for this cmdlet on this computer. It 
    is displaying only partial help.
        -- To download and install Help files for the module that includes 
    this cmdlet, use Update-Help.
        -- To view the Help topic for this cmdlet online, type: "Get-Help 
    Get-ChildItem -Online" or 
           go to http://go.microsoft.com/fwlink/?LinkID=113308.
```
`Help for our function`
```bash
PS C:\> function Get-ChildName ()
{
  Write-Output (Get-ChildItem | Select-Object "Name")
}


PS C:\> Get-Help Get-ChildName

NAME
    Get-ChildName
    
SYNTAX
    Get-ChildName  
    

ALIASES
    None
    

REMARKS
    None
```
Custom tags within a comment block that Get-Help will recognize
```
Note that not all of them are required
 .SYNOPSIS - A brief description of the command
 .DESCRIPTION - Detailed command description
 .PARAMETER name - Include one description for each parameter
 .EXAMPLE - Detailed examples on how to use the command
 .INPUTS - What pipeline inputs are supported
 .OUTPUTS - What this funciton outputs
 .NOTES - Any misc notes you haven't put anywhere else
 .LINK - A link to the URL for more help. Use one .LINK tag per URL
 Use "Get-Help about_comment_based_help" for full list and details
```
```bash
PS C:\> function Get-ChildName ()
{
<#
  .SYNOPSIS
  Returns a list of only the names for the child items in the current location.
  
  .DESCRIPTION
  This function is similar to Get-ChildItem, except that it returns only the name
  property. 
  
  .INPUTS
  None. 
  
  .OUTPUTS
  System.String. Sends a collection of strings out the pipeline. 
  
  .EXAMPLE
  Example 1 - Simple use
  Get-ChildName
  
  .EXAMPLE
  Example 2 - Passing to another object in the pipeline
  Get-ChildName | Where-Object {$_.Name -like "*.ps1"}

  .LINK
  Get-ChildItem 
  
#>

  Write-Output (Get-ChildItem | Select-Object "Name")
  
}
```
```bash
PS C:\> Get-Help Get-ChildName

NAME
    Get-ChildName
    
SYNOPSIS
    Returns a list of only the names for the child items in the current 
    location.
    
    
SYNTAX
    Get-ChildName [<CommonParameters>]
    
    
DESCRIPTION
    This function is similar to Get-ChildItem, except that it returns only the 
    name
    property.
    

RELATED LINKS
    Get-ChildItem 

REMARKS
    To see the examples, type: "get-help Get-ChildName -examples".
    For more information, type: "get-help Get-ChildName -detailed".
    For technical information, type: "get-help Get-ChildName -full".
    For online help, type: "get-help Get-ChildName -online"




PS C:\> Get-Help Get-ChildName -full

NAME
    Get-ChildName
    
SYNOPSIS
    Returns a list of only the names for the child items in the current 
    location.
    
SYNTAX
    Get-ChildName [<CommonParameters>]
    
    
DESCRIPTION
    This function is similar to Get-ChildItem, except that it returns only the 
    name
    property.
    

PARAMETERS
    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, 
    see 
        about_CommonParameters 
    (http://go.microsoft.com/fwlink/?LinkID=113216). 
    
INPUTS
    None.
        
    
    
    
OUTPUTS
    System.String. Sends a collection of strings out the pipeline.
        
    
    
    
    -------------------------- EXAMPLE 1 --------------------------
    
    PS C:\>Example 1 - Simple use
    
    
    Get-ChildName
    
    
    
    
    
    -------------------------- EXAMPLE 2 --------------------------
    
    PS C:\>Example 2 - Passing to another object in the pipeline
    
    
    Get-ChildName | Where-Object {$_.Name -like "*.ps1"}
    
    
    
    
    
    
RELATED LINKS
    Get-ChildItem 
```
## 7. Error Handling
Better Error handling is essential for managing the scripts. 
```bash
PS C:\> function divver($enum,$denom)
{   
  Write-Host "Divver begin."
  $result = $enum / $denom
  Write-Host "Result: $result"
  Write-Host "Divver done."    
}

PS C:\> divver 33 3   # No Error
Divver begin.
Result: 11
Divver done.

PS C:\> divver 33 0   # Generates Error
Divver begin.
Attempted to divide by zero.
At line:4 char:3
+   $result = $enum / $denom
+   ~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [], RuntimeException
    + FullyQualifiedErrorId : RuntimeException
 
Result: 
Divver done.
```
Handle errors using try/catch/finally
```bash
PS C:\> function divver($enum,$denom)
{   
  Write-Host "Divver begin."

  try
  {
    $result = $enum / $denom
    Write-Host "Result: $result"
  }
  catch
  {
    Write-Host "Oh NO! An error has occurred!!"
    Write-Host $_.ErrorID
    Write-Host $_.Exception.Message
    break  # With break, or omitting it, error bubbles up to parent
  }
  finally
  {
    Write-Host "Divver done."    
  }
}

PS C:\> divver 33 3   # No Error
Divver begin.
Result: 11
Divver done.

PS C:\> divver 33 0   # Generates Error
Divver begin.
Oh NO! An error has occurred!!

Attempted to divide by zero.
Divver done.
```
The errors that occur mainly falls under two categories:

    a. Terminating Errors halts the command (or script execution) completely.
        Ex: non-existent cmdlets, syntax errors that would prevent a cmdlet from running, or other fatal errors.
    b. Non-Terminating Errors allows execution to continue despite the failure. 
        Ex: operational errors such file not found, permissions problems, etc.
        
    
When either type of error occurs during execution, it is logged to a global variable called **$Error**.
This variable is a collection of PowerShell error objects with the most recent error at index 0. 
```bash
 C:\> $Error.GetType()

Public IsSerial Name                                     BaseType
------ -------- ----                                     --------
ue     True     ArrayList                                System.Object


 C:\> $Error.Count

 C:\> Some-Command
me-Command : The term 'Some-Command' is not recognized as the name of a cmdlet, function, script file, or operable
ogram. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
 line:1 char:1
Some-Command
~~~~~~~~~~~~
  + CategoryInfo          : ObjectNotFound: (Some-Command:String) [], CommandNotFoundException
  + FullyQualifiedErrorId : CommandNotFoundException

 C:\> $Error.Count

 C:\> $error[0]
me-Command : The term 'Some-Command' is not recognized as the name of a cmdlet, function, script file, or operable
ogram. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
 line:1 char:1
Some-Command
~~~~~~~~~~~~
  + CategoryInfo          : ObjectNotFound: (Some-Command:String) [], CommandNotFoundException
  + FullyQualifiedErrorId : CommandNotFoundException

 C:\> $error[0] | Get-Member


 TypeName: System.Management.Automation.ErrorRecord

me                  MemberType     Definition
--                  ----------     ----------
uals                Method         bool Equals(System.Object obj)
tHashCode           Method         int GetHashCode()
tObjectData         Method         void GetObjectData(System.Runtime.Serialization.SerializationInfo info, System....
tType               Method         type GetType()
String              Method         string ToString()
tegoryInfo          Property       System.Management.Automation.ErrorCategoryInfo CategoryInfo {get;}
rorDetails          Property       System.Management.Automation.ErrorDetails ErrorDetails {get;set;}
ception             Property       System.Exception Exception {get;}
llyQualifiedErrorId Property       string FullyQualifiedErrorId {get;}
vocationInfo        Property       System.Management.Automation.InvocationInfo InvocationInfo {get;}
pelineIterationInfo Property       System.Collections.ObjectModel.ReadOnlyCollection[int] PipelineIterationInfo {g...
riptStackTrace      Property       string ScriptStackTrace {get;}
rgetObject          Property       System.Object TargetObject {get;}
MessageDetails      ScriptProperty System.Object PSMessageDetails {get=& { Set-StrictMode -Version 1; $this.Except...


 C:\> $error[0].InvocationInfo


Command             :
undParameters       : {}
boundArguments      : {}
riptLineNumber      : 1
fsetInLine          : 1
storyId             : 5
riptName            :
ne                  : Some-Command
sitionMessage       : At line:1 char:1
                      + Some-Command
                      + ~~~~~~~~~~~~
ScriptRoot          :
CommandPath         :
vocationName        : Some-Command
pelineLength        : 0
pelinePosition      : 0
pectingInput        : False
mmandOrigin         : Internal
splayScriptPosition :



 C:\> $error[0].Exception
e term 'Some-Command' is not recognized as the name of a cmdlet, function, script file, or operable program. Check
e spelling of the name, or if a path was included, verify that the path is correct and try again.
 C:\>
 C:\> $error[0].Exception.StackTrace
 at System.Management.Automation.CommandDiscovery.LookupCommandInfo(String commandName, CommandTypes commandTypes, Sea
hResolutionOptions searchResolutionOptions, CommandOrigin commandOrigin, ExecutionContext context)
 at System.Management.Automation.CommandDiscovery.LookupCommandProcessor(String commandName, CommandOrigin commandOrig
, Nullable`1 useLocalScope)
 at System.Management.Automation.ExecutionContext.CreateCommand(String command, Boolean dotSource)
 at System.Management.Automation.PipelineOps.AddCommand(PipelineProcessor pipe, CommandParameterInternal[] commandElem
ts, CommandBaseAst commandBaseAst, CommandRedirection[] redirections, ExecutionContext context)
 at System.Management.Automation.PipelineOps.InvokePipeline(Object input, Boolean ignoreInput, CommandParameterInterna
][] pipeElements, CommandBaseAst[] pipeElementAsts, CommandRedirection[][] commandRedirections, FunctionContext funcCo
ext)
 at System.Management.Automation.Interpreter.ActionCallInstruction`6.Run(InterpretedFrame frame)
 at System.Management.Automation.Interpreter.EnterTryCatchFinallyInstruction.Run(InterpretedFrame frame)
 C:\>
```
#### Error Action Preference
PowerShell halts execution on terminating errors. Error Action Preference allows us to specify the desired behavior for a non-terminating error; it can be scoped at the command level or all the way up to the script level.
 
Available choices for error action preference:

* SilentlyContinue – error messages are suppressed and execution continues.
* Stop – forces execution to stop, behaving like a terminating error.
* Continue – the default option. Errors will display and execution will continue.
* Inquire – prompt the user for input to see if we should proceed.
* Ignore – (new in v3) – the error is ignored and not logged to the error stream. Has very restricted usage scenarios.
    
Example: Set the preference at the script scope to Stop, place the following near the top of the script file:
```bash
PS C:\> $ErrorActionPreference = “Stop”
```
Example: Set the preference at the cmdlet level to Inquire, add error action switch (or alias EA): 
```bash
PS C:\> Get-ChildItem "D:\No Such Directory" -ErrorAction "Inquire"

Confirm
Cannot find drive. A drive with the name 'D' does not exist.
[Y] Yes  [A] Yes to All  [H] Halt Command  [S] Suspend  [?] Help (default is "Y"): Y
Get-ChildItem : Cannot find drive. A drive with the name 'D' does not exist.
At line:1 char:1
+ Get-ChildItem "D:\No Such Directory" -ErrorAction "Inquire"
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (D:String) [Get-ChildItem], DriveNotFoundException
    + FullyQualifiedErrorId : DriveNotFound,Microsoft.PowerShell.Commands.GetChildItemCommand

```

#### Try/Catch/Finally Blocks:
The behavior of try/catch is to catch terminating errors (exceptions). This means Non-terminating (operational) errors inside a try block will not trigger a Catch*. If you would like to catch all possible errors (terminating and non-terminating) – then simply set the error action preference to Stop. Remember that Stop error action forces a non-terminating error to behave like a terminating error, which means it can then be trapped in a catch block. 
```bash
PS C:\> try
{
    <#
        Add dangerous code here that might produce exceptions.
        Place as many code statements as needed here.
        Non-terminating errors must have error action preference set to Stop to be caught.
    #>
 
    write-host “Attempting dangerous operation”
    $content = get-content -Path “C:\SomeFolder\This_File_Might_Not_Exist.txt” -ErrorAction Stop
}
catch
{
    <#
        You can have multiple catch blocks (for different exceptions), or one single catch.
        The last error record is available inside the catch block under the $_ variable.
        Code inside this block is used for error handling. Examples include logging an error,
        sending an email, writing to the event log, performing a recovery action, etc.
        In this example I’m just printing the exception type and message to the screen.
    #>
 
    write-host “Caught an exception:” -ForegroundColor Red
    write-host “Exception Type: $($_.Exception.GetType().FullName)” -ForegroundColor Red
    write-host “Exception Message: $($_.Exception.Message)” -ForegroundColor Red
}
finally
{
    <#
        Any statements in this block will always run even if errors are caught.
        This statement block is optional. Normally used for cleanup and
        releasing resources that must happen even under error situations.
    #>
 
    write-host “Finally block reached”
}
Attempting dangerous operation
Caught an exception:
Exception Type: System.Management.Automation.ItemNotFoundException
Exception Message: Cannot find path 'C:\SomeFolder\This_File_Might_Not_Exist.txt
' because it does not exist.
Finally block reached
```
`Finally` block is option; but `try` and `catch` blocks are essential for handling exceptions.

```bash
PS C:\> write-Host $(1/0)
Attempted to divide by zero.
At line:1 char:14
+ write-Host $(1/0)
+              ~~~
    + CategoryInfo          : NotSpecified: (:) [], RuntimeException
    + FullyQualifiedErrorId : RuntimeException
 
```
Catching this exception
```bash
PS C:\> try
{
    write-Host $(1/0)
}
catch
{
    write-Host "This is an Exception"
}

This is an Exception
```
Displaying the actual exception
```bash
PS C:\> try
{
    write-Host $(1/0)
}
catch
{
    write-Host $_.Exception
}

System.Management.Automation.RuntimeException: Attempted to divide by zero. --->
 System.DivideByZeroException: Attempted to divide by zero.
   --- End of inner exception stack trace ---
   at System.Management.Automation.ExceptionHandlingOps.CheckActionPreference(Fu
nctionContext funcContext, Exception exception)
   at System.Management.Automation.Interpreter.ActionCallInstruction`2.Run(Inter
pretedFrame frame)
   at System.Management.Automation.Interpreter.EnterTryCatchFinallyInstruction.R
un(InterpretedFrame frame)
   at System.Management.Automation.Interpreter.EnterTryCatchFinallyInstruction.R
un(InterpretedFrame frame)
```
Handling the exception with the appropriate exception type:
```bash
PS C:\> try
{
    write-Host $(1/0)
}
catch [System.Management.Automation.RuntimeException]
{
    write-Host "This is Run-time Exception"
}
catch
{
    write-Host "Other Exception"
}
This is Run-time Exception

```
To get all the exceptions
```bash
PS C:\> [appdomain]::CurrentDomain.GetAssemblies() | ForEach {
    Try {
        $_.GetExportedTypes() | Where {
            $_.Fullname -match 'Exception'
        }
    } Catch {}
} | Select FullName

FullName                                                                       
--------                                                                       
System.AggregateException                                                      
System.Exception                                                               
System.SystemException                                                         
System.OutOfMemoryException                                                    
System.StackOverflowException                                                  
System.DataMisalignedException                                                 
System.ExecutionEngineException                                                
System.MemberAccessException                                                   
System.AccessViolationException                                                
System.ApplicationException                                                    
System.AppDomainUnloadedException                                              
System.ArgumentException                                                       
System.ArgumentNullException                                                   
System.ArgumentOutOfRangeException                                             
System.ArithmeticException                                                     
System.ArrayTypeMismatchException                                              
System.BadImageFormatException                                                 
System.CannotUnloadAppDomainException                                          
System.TypeUnloadedException                                                   
System.ContextMarshalException                                                 
System.DivideByZeroException                                                   
System.DuplicateWaitObjectException                                            
System.EntryPointNotFoundException                                             
System.DllNotFoundException                                                    
System.FieldAccessException                                                    
System.FormatException                                                         
System.IndexOutOfRangeException                                                
System.InsufficientMemoryException                                             
System.InsufficientExecutionStackException                                     
System.InvalidCastException                                                    
System.InvalidOperationException                                               
System.InvalidProgramException                                                 
System.InvalidTimeZoneException                                                
System.MethodAccessException                                                   
System.MissingFieldException                                                   
System.MissingMemberException                                                  
System.MissingMethodException                                                  
System.MulticastNotSupportedException                                          
System.NotFiniteNumberException                                                
System.NotImplementedException                                                 
System.NotSupportedException                                                   
System.NullReferenceException                                                  
System.ObjectDisposedException                                                 
System.OperationCanceledException                                              
System.OverflowException                                                       
System.PlatformNotSupportedException                                           
System.RankException                                                           
System.TimeoutException                                                        
System.TimeZoneNotFoundException                                               
System.TypeAccessException                                                     
System.TypeInitializationException                                             
System.TypeLoadException                                                       
System.UnauthorizedAccessException                                             
System.UnhandledExceptionEventArgs                                             
System.UnhandledExceptionEventHandler                                          
System.IO.DirectoryNotFoundException                                           
System.IO.DriveNotFoundException                                               
System.IO.EndOfStreamException                                                 
System.IO.FileLoadException                                                    
System.IO.FileNotFoundException                                                
System.IO.IOException                                                          
System.IO.PathTooLongException                                                 
System.IO.IsolatedStorage.IsolatedStorageException                             
System.Security.XmlSyntaxException                                             
System.Security.SecurityException                                              
System.Security.HostProtectionException                                        
System.Security.VerificationException                                          
System.Security.AccessControl.PrivilegeNotHeldException                        
System.Security.Cryptography.CryptographicException                            
System.Security.Cryptography.CryptographicUnexpectedOperationException         
System.Security.Principal.IdentityNotMappedException                           
System.Security.Policy.PolicyException                                         
System.Resources.MissingManifestResourceException                              
System.Resources.MissingSatelliteAssemblyException                             
System.Globalization.CultureNotFoundException                                  
System.Diagnostics.Tracing.EventSourceException                                
System.Collections.Generic.KeyNotFoundException                                
System.Threading.AbandonedMutexException                                       
System.Threading.LockRecursionException                                        
System.Threading.SemaphoreFullException                                        
System.Threading.SynchronizationLockException                                  
System.Threading.ThreadAbortException                                          
System.Threading.ThreadInterruptedException                                    
System.Threading.ThreadStateException                                          
System.Threading.ThreadStartException                                          
System.Threading.WaitHandleCannotBeOpenedException                             
System.Threading.Tasks.TaskCanceledException                                   
System.Threading.Tasks.TaskSchedulerException                                  
System.Threading.Tasks.UnobservedTaskExceptionEventArgs                        
System.Reflection.AmbiguousMatchException                                      
System.Reflection.CustomAttributeFormatException                               
System.Reflection.InvalidFilterCriteriaException                               
System.Reflection.ExceptionHandlingClauseOptions                               
System.Reflection.ExceptionHandlingClause                                      
System.Reflection.ReflectionTypeLoadException                                  
System.Reflection.TargetException                                              
System.Reflection.TargetInvocationException                                    
System.Reflection.TargetParameterCountException                                
System.Reflection.Emit.ExceptionHandler                                        
System.Runtime.Serialization.SerializationException                            
System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute
System.Runtime.ExceptionServices.FirstChanceExceptionEventArgs                 
System.Runtime.ExceptionServices.ExceptionDispatchInfo                         
System.Runtime.Remoting.RemotingException                                      
System.Runtime.Remoting.ServerException                                        
System.Runtime.Remoting.RemotingTimeoutException                               
System.Runtime.CompilerServices.RuntimeWrappedException                        
System.Runtime.InteropServices.COMException                                    
System.Runtime.InteropServices.ExternalException                               
System.Runtime.InteropServices._Exception                                      
System.Runtime.InteropServices.InvalidOleVariantTypeException                  
System.Runtime.InteropServices.MarshalDirectiveException                       
System.Runtime.InteropServices.SEHException                                    
System.Runtime.InteropServices.InvalidComObjectException                       
System.Runtime.InteropServices.SafeArrayRankMismatchException                  
System.Runtime.InteropServices.SafeArrayTypeMismatchException                  
System.Text.DecoderExceptionFallback                                           
System.Text.DecoderExceptionFallbackBuffer                                     
System.Text.DecoderFallbackException                                           
System.Text.EncoderExceptionFallback                                           
System.Text.EncoderExceptionFallbackBuffer                                     
System.Text.EncoderFallbackException                                           
System.Windows.Forms.UnhandledExceptionMode                                    
System.Windows.Forms.ThreadExceptionDialog                                     
System.Windows.Forms.AxHost+InvalidActiveXStateException                       
System.UriFormatException                                                      
System.Configuration.ConfigurationException                                    
System.Configuration.SettingsPropertyIsReadOnlyException                       
System.Configuration.SettingsPropertyNotFoundException                         
System.Configuration.SettingsPropertyWrongTypeException                        
System.Net.CookieException                                                     
System.Net.HttpListenerException                                               
System.Net.ProtocolViolationException                                          
System.Net.WebException                                                        
System.Net.WebExceptionStatus                                                  
System.Net.WebSockets.WebSocketException                                       
System.Net.Mail.SmtpException                                                  
System.Net.Mail.SmtpFailedRecipientException                                   
System.Net.Mail.SmtpFailedRecipientsException                                  
System.Net.NetworkInformation.NetworkInformationException                      
System.Net.NetworkInformation.PingException                                    
System.Net.Sockets.SocketException                                             
System.Security.Authentication.AuthenticationException                         
System.Security.Authentication.InvalidCredentialException                      
System.Threading.BarrierPostPhaseException                                     
System.Threading.ThreadExceptionEventArgs                                      
System.Threading.ThreadExceptionEventHandler                                   
System.IO.InvalidDataException                                                 
System.IO.InternalBufferOverflowException                                      
System.ComponentModel.InvalidAsynchronousStateException                        
System.ComponentModel.InvalidEnumArgumentException                             
System.ComponentModel.LicenseException                                         
System.ComponentModel.WarningException                                         
System.ComponentModel.Win32Exception                                           
System.ComponentModel.Design.CheckoutException                                 
System.CodeDom.CodeThrowExceptionStatement                                     
System.Text.RegularExpressions.RegexMatchTimeoutException                      
System.Drawing.Printing.InvalidPrinterException                                
System.Management.Automation.RuntimeException                                  
System.Management.Automation.ScriptRequiresException                           
System.Management.Automation.RemoteException                                   
System.Management.Automation.Runspaces.TypeTableLoadException                  
System.Management.Automation.ExtendedTypeSystemException                       
System.Management.Automation.MethodException                                   
System.Management.Automation.MethodInvocationException                         
System.Management.Automation.GetValueException                                 
System.Management.Automation.PropertyNotFoundException                         
System.Management.Automation.GetValueInvocationException                       
System.Management.Automation.SetValueException                                 
System.Management.Automation.SetValueInvocationException                       
System.Management.Automation.PSInvalidCastException                            
System.Management.Automation.SettingValueExceptionEventArgs                    
System.Management.Automation.GettingValueExceptionEventArgs                    
Microsoft.PowerShell.Commands.HelpCategoryInvalidException                     
Microsoft.PowerShell.Commands.HelpNotFoundException                            
System.Management.Automation.Runspaces.InvalidRunspaceStateException           
System.Management.Automation.Runspaces.RunspaceOpenModuleLoadException         
System.Management.Automation.Runspaces.InvalidPipelineStateException           
System.Management.Automation.InvalidPowerShellStateException                   
System.Management.Automation.Runspaces.InvalidRunspacePoolStateException       
System.Management.Automation.InvalidJobStateException                          
System.Management.Automation.JobFailedException                                
System.Management.Automation.Remoting.PSRemotingDataStructureException         
System.Management.Automation.Remoting.PSRemotingTransportException             
System.Management.Automation.Remoting.PSRemotingTransportRedirectException     
System.Management.Automation.Runspaces.RunspaceConfigurationAttributeException 
System.Management.Automation.Runspaces.RunspaceConfigurationTypeException      
System.Management.Automation.WildcardPatternException                          
System.Management.Automation.FlowControlException                              
System.Management.Automation.LoopFlowException                                 
System.Management.Automation.BreakException                                    
System.Management.Automation.ContinueException                                 
System.Management.Automation.ExitException                                     
System.Management.Automation.ScriptBlockToPowerShellNotSupportedException      
System.Management.Automation.PSSecurityException                               
System.Management.Automation.Runspaces.PSConsoleLoadException                  
System.Management.Automation.Runspaces.PSSnapInException                       
System.Management.Automation.CommandNotFoundException                          
System.Management.Automation.ApplicationFailedException                        
System.Management.Automation.CmdletInvocationException                         
System.Management.Automation.CmdletProviderInvocationException                 
System.Management.Automation.PipelineStoppedException                          
System.Management.Automation.PipelineClosedException                           
System.Management.Automation.ActionPreferenceStopException                     
System.Management.Automation.ParentContainsErrorRecordException                
System.Management.Automation.RedirectedException                               
System.Management.Automation.ScriptCallDepthException                          
System.Management.Automation.PipelineDepthException                            
System.Management.Automation.HaltCommandException                              
System.Management.Automation.Host.HostException                                
System.Management.Automation.Host.PromptingException                           
System.Management.Automation.MetadataException                                 
System.Management.Automation.ValidationMetadataException                       
System.Management.Automation.ArgumentTransformationMetadataException           
System.Management.Automation.ParsingMetadataException                          
System.Management.Automation.PSArgumentException                               
System.Management.Automation.PSArgumentNullException                           
System.Management.Automation.PSArgumentOutOfRangeException                     
System.Management.Automation.PSInvalidOperationException                       
System.Management.Automation.PSNotImplementedException                         
System.Management.Automation.PSNotSupportedException                           
System.Management.Automation.PSObjectDisposedException                         
System.Management.Automation.ParameterBindingException                         
System.Management.Automation.ParseException                                    
System.Management.Automation.IncompleteParseException                          
System.Management.Automation.ProviderInvocationException                       
System.Management.Automation.SessionStateException                             
System.Management.Automation.SessionStateOverflowException                     
System.Management.Automation.SessionStateUnauthorizedAccessException           
System.Management.Automation.ProviderNotFoundException                         
System.Management.Automation.ProviderNameAmbiguousException                    
System.Management.Automation.DriveNotFoundException                            
System.Management.Automation.ItemNotFoundException                             
System.Management.Automation.Runspaces.FormatTableLoadException                
System.Management.Instrumentation.InstrumentationBaseException                 
System.Management.Instrumentation.InstrumentationException                     
System.Management.Instrumentation.InstanceNotFoundException                    
System.Diagnostics.Eventing.Reader.EventLogException                           
System.Diagnostics.Eventing.Reader.EventLogNotFoundException                   
System.Diagnostics.Eventing.Reader.EventLogReadingException                    
System.Diagnostics.Eventing.Reader.EventLogProviderDisabledException           
System.Diagnostics.Eventing.Reader.EventLogInvalidDataException                
System.ComponentModel.Composition.CompositionContractMismatchException         
System.ComponentModel.Composition.ImportCardinalityMismatchException           
System.ComponentModel.Composition.ChangeRejectedException                      
System.ComponentModel.Composition.CompositionException                         
System.ComponentModel.Composition.Primitives.ComposablePartException           
System.Windows.ExceptionRoutedEventArgs                                        
System.Windows.ResourceReferenceKeyNotFoundException                           
System.Windows.Data.UpdateSourceExceptionFilterCallback                        
System.Windows.Data.ValueUnavailableException                                  
System.Windows.Markup.XamlParseException                                       
System.Windows.Controls.ExceptionValidationRule                                
System.Windows.Controls.PrintDialogException                                   
System.Security.RightsManagement.RightsManagementException                     
System.Windows.Threading.DispatcherUnhandledExceptionEventArgs                 
System.Windows.Threading.DispatcherUnhandledExceptionEventHandler              
System.Windows.Threading.DispatcherUnhandledExceptionFilterEventArgs           
System.Windows.Threading.DispatcherUnhandledExceptionFilterEventHandler        
System.IO.FileFormatException                                                  
System.Windows.Media.InvalidWmpVersionException                                
System.Windows.Media.ExceptionEventArgs                                        
System.Windows.Media.Animation.AnimationException                              
System.Xaml.XamlException                                                      
System.Xaml.XamlParseException                                                 
System.Xaml.XamlObjectWriterException                                          
System.Xaml.XamlDuplicateMemberException                                       
System.Xaml.XamlInternalException                                              
System.Xaml.XamlSchemaException                                                
System.Xaml.XamlObjectReaderException                                          
System.Xaml.XamlXmlWriterException                                             
System.Configuration.ConfigurationErrorsException                              
System.Configuration.Provider.ProviderException                                
System.Xml.XmlException                                                        
System.Xml.Schema.XmlSchemaException                                           
System.Xml.Schema.XmlSchemaValidationException                                 
System.Xml.Schema.XmlSchemaInferenceException                                  
System.Xml.Xsl.XsltException                                                   
System.Xml.Xsl.XsltCompileException                                            
System.Xml.XPath.XPathException                                                
System.Runtime.Serialization.InvalidDataContractException                      
System.DirectoryServices.DirectoryServicesCOMException                         
System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectNotFoundException
System.DirectoryServices.ActiveDirectory.ActiveDirectoryOperationException     
System.DirectoryServices.ActiveDirectory.ActiveDirectoryServerDownException    
System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectExistsException  
System.DirectoryServices.ActiveDirectory.SyncFromAllServersOperationException  
System.DirectoryServices.ActiveDirectory.ForestTrustCollisionException         
System.Management.ManagementException                                          
Microsoft.Management.Infrastructure.CimException                               
System.Configuration.Install.InstallException                                  
System.Transactions.TransactionException                                       
System.Transactions.TransactionAbortedException                                
System.Transactions.TransactionInDoubtException                                
System.Transactions.TransactionManagerCommunicationException                   
System.Transactions.TransactionPromotionException                              
Microsoft.PowerShell.Commands.CertificateProviderItemNotFoundException         
Microsoft.PowerShell.Commands.CertificateNotFoundException                     
Microsoft.PowerShell.Commands.CertificateStoreNotFoundException                
Microsoft.PowerShell.Commands.CertificateStoreLocationNotFoundException        
Microsoft.Management.UI.Internal.FilterExceptionEventArgs                      
System.Windows.Automation.ProxyAssemblyNotLoadedException                      
System.Windows.Automation.NoClickablePointException                            
System.Windows.Automation.ElementNotEnabledException                           
System.Windows.Automation.ElementNotAvailableException                         
Microsoft.SqlServer.Server.InvalidUdtException                                 
System.Data.StrongTypingException                                              
System.Data.TypedDataSetGeneratorException                                     
System.Data.DataException                                                      
System.Data.ConstraintException                                                
System.Data.DeletedRowInaccessibleException                                    
System.Data.DuplicateNameException                                             
System.Data.InRowChangingEventException                                        
System.Data.InvalidConstraintException                                         
System.Data.MissingPrimaryKeyException                                         
System.Data.NoNullAllowedException                                             
System.Data.ReadOnlyException                                                  
System.Data.RowNotInTableException                                             
System.Data.VersionNotFoundException                                           
System.Data.DBConcurrencyException                                             
System.Data.InvalidExpressionException                                         
System.Data.EvaluateException                                                  
System.Data.SyntaxErrorException                                               
System.Data.OperationAbortedException                                          
System.Data.SqlTypes.SqlTypeException                                          
System.Data.SqlTypes.SqlNullValueException                                     
System.Data.SqlTypes.SqlTruncateException                                      
System.Data.SqlTypes.SqlNotFilledException                                     
System.Data.SqlTypes.SqlAlreadyFilledException                                 
System.Data.SqlClient.SqlException                                             
System.Data.OleDb.OleDbException                                               
System.Data.Odbc.OdbcException                                                 
System.Data.Common.DbException                                                 
Microsoft.PowerShell.Commands.WriteErrorException                              
Microsoft.PowerShell.Commands.StringManipulation.FlashExtractWrapper.FlashEx...
Microsoft.PowerShell.Commands.StringManipulation.FlashExtractWrapper.FlashEx...
Microsoft.PowerShell.Commands.StringManipulation.FlashExtractWrapper.Templat...
Microsoft.PowerShell.Commands.ProcessCommandException                          
Microsoft.PowerShell.Commands.ServiceCommandException                          
Microsoft.PowerShell.Commands.RestartComputerTimeoutException                  
Microsoft.PowerShell.Cmdletization.Cim.CimJobException                         
Microsoft.CSharp.RuntimeBinder.RuntimeBinderException                          
Microsoft.CSharp.RuntimeBinder.RuntimeBinderInternalCompilerException          
System.ServiceProcess.TimeoutException
```

#### Handling Errors from non-PowerShell processes
when exception occurs while executing external processes like .exe execution, ..., they can be handled using **$LastExitCode** powerShell variable.

when the launched process exits, powerShell will write the exit code directly to `$LastExitCode`
In most cases, exit code `0` means `Success`, and `1` means `failure`.


## 10. Working with cmdlets
####	10.1 Finding and Learning Commands
####	10.2 Working with the Pipeline
####		10.2.1 Passing Data in the Pipeline By Value
####	10.3 Selecting, Sorting, and Measuring Objects
####	10.4 Converting, Exporting, and Importing Objects
####	10.5 Filtering and Validating Objects Out of the Pipeline
TODO Filter-Object

Where-Object
```
PS C:\> (1..15) |  Where-Object { $_ -gt 10 }
11
12
13
14  
15
PS C:\> (1..15).Where{ $_ -gt 10 }    # Possible from version 4.0
11
12
13
14
15
```
####	10.6 Enumerating Objects in the Pipeline
####	10.7 Formatting Output
####		10.7.1 Using Basic Formatting
####		10.7.2 Using Advanced Formatting
####		10.7.3 Redirecting Formatted Output
####	10.8 Working with date and time
####    10.9 File Handling 

####	10.10 Aliases in PowerShell	
TODO creating , reading and writing to files


To get all the profiles in the machine
```
PS C:\> Resolve-Path -Path C:\users\*\Desktop -ErrorAction SilentlyContinue

Path
----
C:\users\Administrator.JAINABHISHEK\Desktop
C:\users\JAINABHISHEK\Desktop
C:\users\Public\Desktop

```
To get only the names, and not the paths, 
```
PS C:\> Resolve-Path -Path C:\users\*\Desktop -ErrorAction SilentlyContinue |
>>     ForEach-Object {
>>         $_.Path.Split('\')[-2]
>>     }
>>
Administrator.JAINABHISHEK
JAINABHISHEK
Public

```

## 11. Working with Windows Interfaces
####	11.1 Managing services and Processes
####	11.2 working with WMI and Other windows APIs
####	11.3 Working with MS Word, MS Excel and Speach products
## 12. Windows Remoting
####	12.1 Working with winrm service
####	12.2 Connecting to the remote windows server and managing the services
####	12.3 Connecting to the remote Linux server and managing the services
## 13. Advanced PowerShell Techniques
####	13.1 Using Background Jobs and Scheduled Jobs
####	13.2 Using PSProviders and PSDrives
	
## 14. Other Modules
#### 14.1 ShowUI
```
PS C:\> $User = [ordered]@{
   FirstName = "jain"
   LastName = "abhishek"
   BirthDate = [DateTime]
   UserName = "jainabhishek"
}

$data = Get-Input $User -Show
Write-Host $data
#System.Collections.Hashtable

PS C:\> $data

Name                           Value                                                                                      
----                           -----                                                                                      
UserName                       jainabhishek                                                                                
FirstName                      jain                                                                                       
LastName                       abhishek                                                                                    
BirthDate                      6/16/2017 2:52:11 PM                                                                       
```
