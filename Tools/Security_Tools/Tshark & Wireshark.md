
### Filter http requests
```bash
tshark -r yourfile.pcap -Y "http.request" 
```

```bash
tshark -r yourfile.pcap -Y "http.request" | wc -l
```

```bash
tshark -r yourfile.pcap -Y "http.request.method == POST"

```
##### Find by domain

```bash
tshark -r yourfile.pcap -Y 'http.host == "example.com" && http.response' -T fields -e http.host -e http.server
```

```bash
tshark -r yourfile.pcap -Y 'http.host == "example.com" && http.request'
```

#### Find IP/Domain by DNS

```bash
tshark -r yourfile.pcap -Y "dns.flags.response == 1 && dns.qry.type == 1 && dns.qry.name == 'example.com'" -T fields -e dns.qry.name -e dns.a

tshark -r yourfile.pcap -Y "dns.flags.response == 1 && dns.qry.type == 1" -T fields -e dns.qry.name -e dns.a

```
##### Find server header
```bash
tshark -r yourfile.pcap -Y 'http.host == "example.com" && http.response' -T fields -e http.host -e http.server

```
#### Follow Streams
```bash
tshark -r yourfile.pcap -q -z follow,tcp,ascii,0
```
#### Exporting Objects
> [!NOTE] Export HTTP Objects
>Do this in a Sandbox Only! 
>This will recreate the file that was downloaded... Could be bad news.

```bash
tshark -r traffic.pcap --export-objects "http,./extracted_files"

```



FIND EMAI
```bash
tshark -r teamwork.pcap -Y "http.request.method == POST" -T fields -e http.file.data | grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b"
```