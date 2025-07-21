## Enumeration
`rustscan -a 10.129.146.215 -- -A`
```bash
Open 10.129.146.215:53
Open 10.129.146.215:88
Open 10.129.146.215:111
Open 10.129.146.215:135
Open 10.129.146.215:139
Open 10.129.146.215:389
Open 10.129.146.215:445
Open 10.129.146.215:464
Open 10.129.146.215:593
Open 10.129.146.215:636
Open 10.129.146.215:2049
Open 10.129.146.215:3269
Open 10.129.146.215:3268
Open 10.129.146.215:4222
Open 10.129.146.215:5985
Open 10.129.146.215:9389
Open 10.129.146.215:47001
Open 10.129.146.215:49664
Open 10.129.146.215:49666
Open 10.129.146.215:49667
Open 10.129.146.215:49665
Open 10.129.146.215:49668
Open 10.129.146.215:57393
Open 10.129.146.215:60326
Open 10.129.146.215:60343
Open 10.129.146.215:63293
Open 10.129.146.215:63301
Open 10.129.146.215:63304
Open 10.129.146.215:63319


53/udp    open          domain       udp-response ttl 127
88/udp    open          kerberos-sec udp-response ttl 127
111/udp   open          rpcbind      udp-response ttl 127
123/udp   open          ntp          udp-response ttl 127
137/udp   open|filtered netbios-ns   no-response
138/udp   open|filtered netbios-dgm  no-response
500/udp   open|filtered isakmp       no-response
515/udp   open|filtered printer      no-response
1030/udp  open|filtered iad1         no-response
1645/udp  open|filtered radius       no-response
1646/udp  open|filtered radacct      no-response
2049/udp  open          nfs          udp-response ttl 127
3283/udp  open|filtered netassistant no-response
4444/udp  open|filtered krb524       no-response
4500/udp  open|filtered nat-t-ike    no-response
5353/udp  open|filtered zeroconf     no-response
17185/udp open|filtered wdbrpc       no-response
49181/udp open|filtered unknown      no-response
49188/udp open|filtered unknown      no-response

```
DNS:dc01.mirage.htb, DNS:mirage.htb, DNS:MIRAGE

NFS Share? #MirageReports
```bash
┌──(sstephens㉿kali-arm)-[~/…/Security_Notes/Challenges-&-CTFs/HackTheBox/Starting_Point]
└─$ netexec nfs 10.129.146.215 --port 2049 --enum-shares
NFS         10.129.146.215  2049   10.129.146.215   [*] Supported NFS versions: (2, 3, 4) (root escape:False)
NFS         10.129.146.215  2049   10.129.146.215   [*] Enumerating NFS Shares Directories
NFS         10.129.146.215  2049   10.129.146.215   [+] /MirageReports
NFS         10.129.146.215  2049   10.129.146.215   UID        Perms    File Size      File Path                                     Access List    
NFS         10.129.146.215  2049   10.129.146.215   ---        -----    ---------      ---------                                     -----------    
NFS         10.129.146.215  2049   10.129.146.215   4294967294 r-x      8.1MB          /MirageReports/Incident_Report_Missing_DNS_Record_nats-svc.pdf No network     
NFS         10.129.146.215  2049   10.129.146.215   4294967294 r-x      8.9MB          /MirageReports/Mirage_Authentication_Hardening_Report.pdf No network    
```

10.129.176.32