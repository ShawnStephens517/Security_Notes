![[Usage.pdf]]

```bash
┌──(sstephens㉿kali-ppt)-[~]
└─$ rustscan -a 10.10.11.18  
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Scanning ports: The virtual equivalent of knocking on doors.

[~] The config file is expected to be at "/home/sstephens/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.11.18:22
Open 10.10.11.18:80
[~] Starting Script(s)
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-20 08:52 EDT
Initiating Ping Scan at 08:52
Scanning 10.10.11.18 [2 ports]
Completed Ping Scan at 08:52, 0.02s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 08:52
Completed Parallel DNS resolution of 1 host. at 08:52, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 4, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 08:52
Scanning 10.10.11.18 [2 ports]
Discovered open port 80/tcp on 10.10.11.18
Discovered open port 22/tcp on 10.10.11.18
Completed Connect Scan at 08:52, 0.04s elapsed (2 total ports)
Nmap scan report for 10.10.11.18
Host is up, received syn-ack (0.024s latency).
Scanned at 2024-08-20 08:52:05 EDT for 0s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.15 seconds
```

#### Web Enum
```bash
┌──(sstephens㉿kali-ppt)-[~]
└─$ ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://usage.htb -H "Host: FUZZ.usage.htb"
```
```html
<nav class="navbar navbar-expand-lg navbar-light navbar-laravel">

    <div class="container">

        <a class="navbar-brand" href="[#](view-source:http://usage.htb/#)">Usage</a>

        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">

            <ul class="navbar-nav ml-auto">

                
                    <li class="nav-item">

                        <a class="nav-link" href="[http://usage.htb/login](view-source:http://usage.htb/login)">Login</a>

                    </li>

                    <li class="nav-item">

                        <a class="nav-link" href="[http://usage.htb/registration](view-source:http://usage.htb/registration)">Register</a>

		    </li>
		    <li class="nav-item">

                        <a class="nav-link" href="[http://admin.usage.htb/](view-source:http://admin.usage.htb/)">Admin</a>

                    </li>
            </ul>
        </div>
    </div>
</nav>
```

### Burp Request for [[SQLMap]]
![[email_sql.xml]]