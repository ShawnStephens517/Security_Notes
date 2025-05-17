#Essentials #Web  #DNS 
```bash
gobuster vhost -u http://inlanefreight.htb:30946 -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain

gobuster -u http://{ipadress} -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-2.3-big.txt

```