```bash:ipsweeper.sh
#!/bin/bash

if [ "$1" == ""]
then "Enter IP Address!"
echo "Syntax: ./ipsweeper.sh x.x.x"

else
for ip in `seq 1 254`; do
ping -c 1 $1.$ip | grep "64 bytes"| cut -d " " -f 200 | tr -d ":" &
done
fi
```
