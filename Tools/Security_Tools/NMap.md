# NMAP
## Open Ports
### Top 10 Scan
```bash
sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5
```

### Nmap Packet Trace
```bash
sudo nmap 10.129.2.28 -p 21 --packet-trace -Pn -n --disable-arp-ping
```

### Connect Scan (443)
```bash
sudo nmap 10.129.2.28 -p 443 --packet-trace --disable-arp-ping -Pn -n --reason -sT
```
## Filtered
```bash
sudo nmap 10.129.2.28 -p 139 --packet-trace -n --disable-arp-ping -Pn
...
PORT    STATE    SERVICE
139/tcp filtered netbios-ssn
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
```

## Open UDP
### UDP Scan
```bash
sudo nmap 10.129.2.28 -F -sU
```

UDP can be unreliable since NMAP sends empty datagrams
