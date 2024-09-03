```bash
ip r
ip a

route

sudo -l

netstat -tulnp                              


touch - create file
echo "Thing" > file.txt - Add
echo "Thing2" >> file.txt - Append

sudo service {servicename} start/stop/restart

sudo systemctl start/stop/restart {servicename}

sudo systemctl --daemon reload

python -m http.server [port] - defaults 8000


```


```bash
cat file.txt | grep "Item" | cut -d " " -f {item} | tr -d ":"
```

#### Finding things

```bash
find . -name "*string*" -print

find . -maxdepth 1 -name "*string*" -print`find . -maxdepth 1 -name "*string*" -print
```

#### Count results

Pipe to `wc -l`

Example:
```bash
tshark -r directory-curiosity.pcap -Y 'http.host == "bad_domain" && http.request' | wc -l
```

#### Hashing Checks
```bash
sha256sum extracted_file.raw
sha1sum extracted.raw
md5sum extracted.raw
```


### Upgrade Rev Shell
#stable_shell
```bash
script /dev/null -c bash - can be used inplace of python

# In reverse shell
$ python -c 'import pty; pty.spawn("/bin/bash")'
Ctrl-Z

# In Kali
$ stty raw -echo
$ fg

# In reverse shell
$ reset
$ export SHELL=bash
$ export TERM=xterm-256color
$ stty rows <num> columns <cols>

```