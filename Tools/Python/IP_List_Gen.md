```python
import random

def generate_random_ip():
    return f"{random.randint(1, 255)}.{random.randint(0, 255)}.{random.randint(0, 255)}.{random.randint(1, 255)}"

def generate_ip_list(count=25000):
    ip_list = []
    for _ in range(count):
        ip_list.append(generate_random_ip())
    return ip_list

def write_ips_to_file(ip_list, filename="ips.txt"):
    with open(filename, "w") as file:
        for ip in ip_list:
            file.write(ip + "\n")

if __name__ == "__main__":
    ip_list = generate_ip_list(25000)
    write_ips_to_file(ip_list)
    print(f"Successfully wrote {len(ip_list)} IPs to 'ips.txt'.")
```


This script is a quick dirty ip list generator when brute forcing timeout/rate-limits for pin cracking
EX: Tryhackme Hammer room