
> [!NOTE] FFUF vs GoBuster
> Appears to be more granular to finding directories. Insertable fuzzing space vs for '/'
> 
> 


```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt -u http://10.10.99.113:1337/hmr_FUZZ -s
```

**Subdomain Enum**
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -u http://creative.thm/ -H "Host:FUZZ.creative.thm" -fw 6
```
