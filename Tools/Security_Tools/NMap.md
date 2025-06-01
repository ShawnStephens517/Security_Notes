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


## Firewall and IDS/IPS Evasions Tips
```bash
SYN
sudo nmap 10.129.2.80 -p- -sS -Pn -n --disable-arp-ping --packet-trace

SYN-Filtered
sudo nmap 10.129.2.80 -p- -sS -n -Pn --disable-arp-ping --packet-trace

Syn Custom Source Port
sudo nmap 10.129.2.80 -p- -sS -n -Pn --disable-arp-ping --packet-trace --source-port 53

ACK
sudo nmap 10.129.2.80 -p- -sA -Pn -n --disable-arp-ping --packet-trace

#DecoyScan
sudo nmap 10.129.2.80 -p- -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5

Different Source
sudo nmap 10.129.2.80 -p- -n -Pn -O -S <source-ip> -e tun0
```


### Advanced Scan Options
[[Basics]] [[Active Scanning]]

| Null Scan | No Flags Set | Expect RST if true Closed                |
| --------- | ------------ | ---------------------------------------- |
| FIN Scan  | FIN Flag     | Expect RST = closed, else Open\|Filtered |
| XMAS Scan | FIN,PUSH,URG | Expect RST = closed, else Open\|Filtered |


| Port Scan Type                 | Example Command                                       |
| ------------------------------ | ----------------------------------------------------- |
| TCP Null Scan                  | `sudo nmap -sN MACHINE_IP`                            |
| TCP FIN Scan                   | `sudo nmap -sF MACHINE_IP`                            |
| TCP Xmas Scan                  | `sudo nmap -sX MACHINE_IP`                            |
| TCP Maimon Scan                | `sudo nmap -sM MACHINE_IP`                            |
| TCP ACK Scan                   | `sudo nmap -sA MACHINE_IP`                            |
| TCP Window Scan                | `sudo nmap -sW MACHINE_IP`                            |
| Custom TCP Scan                | `sudo nmap --scanflags URGACKPSHRSTSYNFIN MACHINE_IP` |
| Spoofed Source IP              | `sudo nmap -S SPOOFED_IP MACHINE_IP`                  |
| Spoofed MAC Address            | `--spoof-mac SPOOFED_MAC`                             |
| Decoy Scan                     | `nmap -D DECOY_IP,ME MACHINE_IP`                      |
| Idle (Zombie) Scan             | `sudo nmap -sI ZOMBIE_IP MACHINE_IP`                  |
| Fragment IP data into 8 bytes  | `-f`                                                  |
| Fragment IP data into 16 bytes | `-ff`                                                 |


| Option                   | Purpose                                  |
| ------------------------ | ---------------------------------------- |
| `--source-port PORT_NUM` | specify source port number               |
| `--data-length NUM`      | append random data to reach given length |

These scan types rely on setting TCP flags in unexpected ways to prompt ports for a reply. Null, FIN, and Xmas scan provoke a response from closed ports, while Maimon, ACK, and Window scans provoke a response from open and closed ports.


| Option     | Purpose                               |
| ---------- | ------------------------------------- |
| `--reason` | explains how Nmap made its conclusion |
| `-v`       | verbose                               |
| `-vv`      | very verbose                          |
| `-d`       | debugging                             |
| `-dd`      | more details for debugging            |

| Option                  | Purpose                         |
| ----------------------- | ------------------------------- |
| `--max-rate 50`         | rate <= 50 packets/sec          |
| `--min-rate 15`         | rate >= 15 packets/sec          |
| `--min-parallelism 100` | at least 100 probes in parallel |