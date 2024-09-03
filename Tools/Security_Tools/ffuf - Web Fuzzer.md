
> [!NOTE] FFUF vs GoBuster
> Appears to be more granular to finding directories. Insertable fuzzing space vs for '/'
> 
> 

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt -u http://10.10.99.113:1337/hmr_FUZZ -s
```

