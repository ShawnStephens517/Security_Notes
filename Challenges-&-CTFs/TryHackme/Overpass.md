# Overpassed
```bash
root@ip-10-10-44-36:~# rustscan -a 10.10.255.116
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
ðµ https://admin.tryhackme.com

[~] The config file is expected to be at "/home/rustscan/.rustscan.toml"
[~] File limit higher than batch size. Can increase speed by increasing batch size '-b 1048476'.
Open 10.10.255.116:22
Open 10.10.255.116:80
Open 10.10.255.116:2222
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-28 10:41 UTC
Initiating Ping Scan at 10:41
Scanning 10.10.255.116 [2 ports]
Completed Ping Scan at 10:41, 0.00s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 10:41
Completed Parallel DNS resolution of 1 host. at 10:41, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 1, NX: 0, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 10:41
Scanning ip-10-10-255-116.eu-west-1.compute.internal (10.10.255.116) [3 ports]
Discovered open port 22/tcp on 10.10.255.116
Discovered open port 80/tcp on 10.10.255.116
Discovered open port 2222/tcp on 10.10.255.116
Completed Connect Scan at 10:41, 0.00s elapsed (3 total ports)
Nmap scan report for ip-10-10-255-116.eu-west-1.compute.internal (10.10.255.116)
Host is up, received syn-ack (0.00093s latency).
Scanned at 2024-08-28 10:41:03 UTC for 0s

PORT     STATE SERVICE      REASON
22/tcp   open  ssh          syn-ack
80/tcp   open  http         syn-ack
2222/tcp open  EtherNetIP-1 syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.18 seconds

root@ip-10-10-44-36:~# nmap -A -p 22,80,2222 10.10.255.116

Starting Nmap 7.60 ( https://nmap.org ) at 2024-08-28 11:42 BST
Nmap scan report for ip-10-10-255-116.eu-west-1.compute.internal (10.10.255.116)
Host is up (0.00042s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 e4:3a:be:ed:ff:a7:02:d2:6a:d6:d0:bb:7f:38:5e:cb (RSA)
|   256 fc:6f:22:c2:13:4f:9c:62:4f:90:c9:3a:7e:77:d6:d4 (ECDSA)
|_  256 15:fd:40:0a:65:59:a9:b5:0e:57:1b:23:0a:96:63:05 (EdDSA)
80/tcp   open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: LOL Hacked
2222/tcp open  ssh     OpenSSH 8.2p1 Debian 4 (protocol 2.0)
| ssh-hostkey: 
|_  2048 a2:a6:d2:18:79:e3:b0:20:a2:4f:aa:b6:ac:2e:6b:f2 (RSA)
MAC Address: 02:86:4E:C1:5C:67 (Unknown)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.1 (94%), Linux 3.2 (94%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), Linux 3.8 (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Linux 2.6.32 (92%), Linux 2.6.39 - 3.2 (92%), Linux 3.1 - 3.2 (92%), Linux 3.2 - 4.8 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.42 ms ip-10-10-255-116.eu-west-1.compute.internal (10.10.255.116)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 43.34 seconds

```

Gobuster
```
root@ip-10-10-44-36:~# gobuster dir -u http://10.10.255.116 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-big.txt 
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.255.116
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-big.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2024/08/28 11:43:26 Starting gobuster
===============================================================
/img (Status: 301)
/downloads (Status: 301)
/aboutus (Status: 301)
/css (Status: 301)
/server-status (Status: 403)
===============================================================
2024/08/28 11:47:50 Finished
===============================================================
```