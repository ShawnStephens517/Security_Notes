```embed
title: "anthem-walkthrough-tryhackme.html?m=1"
image: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6QU_Vc17R8wHLsK4zsB3WhTl3NpptNxiwr3jO8KfVN6-3Ig0vfGGmNZx_09gpTFTV22VfaTdWKFDRc7G6LWlTMfujcTYqvB2-GFOC22KAtsU2WcEbYl06C5dnKlC2hQ7d4hO-XPBqLQ/w1200-h630-p-k-no-nu/Screenshot_20200601-003434%7E2.png"
description: "Anthem Exploit a Windows machine in this beginner-level challenge. We first did a Nmap scan to check information about services and open por…"
url: "https://securityhackerctf.blogspot.com/2020/05/anthem-walkthrough-tryhackme.html?m=1"
```
```bash
┌──(sstephens㉿kali-ppt)-[~]
└─$ rustscan -a 10.10.155.201
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Nmap? More like slowmap.🐢

[~] The config file is expected to be at "/home/sstephens/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.155.201:80
Open 10.10.155.201:3389

[~] Starting Script(s)
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-14 03:51 EDT
Initiating Ping Scan at 03:51
Scanning 10.10.155.201 [2 ports]
Stats: 0:00:00 elapsed; 0 hosts completed (0 up), 1 undergoing Ping Scan
Ping Scan Timing: About 100.00% done; ETC: 03:51 (0:00:00 remaining)
Completed Ping Scan at 03:51, 0.03s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 03:51
Completed Parallel DNS resolution of 1 host. at 03:51, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 03:51
Scanning 10.10.155.201 [2 ports]
Discovered open port 80/tcp on 10.10.155.201
Discovered open port 3389/tcp on 10.10.155.201
Completed Connect Scan at 03:51, 0.03s elapsed (2 total ports)
Nmap scan report for 10.10.155.201
Host is up, received syn-ack (0.028s latency).
Scanned at 2024-08-14 03:51:18 EDT for 1s

PORT     STATE SERVICE       REASON
80/tcp   open  http          syn-ack
3389/tcp open  ms-wbt-server syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds

```