# masscan 2 nmap oneliner


```shell
nmap -sV -sC -p`masscan -i tun0 -p0-65535 10.10.10.184 --rate=5000 |grep open |cut -d ' ' -f 4 |cut -d '/' -f 1 |xargs |tr ' ' ','` 10.10.10.184


# Run it as root
TG="10.10.10.185";nmap -sV -sC -p`masscan -i tun0 -p0-65535 $TG --rate=1500 |grep open |cut -d ' ' -f 4 |cut -d '/' -f 1 |xargs |tr ' ' ','` $TG -oA quick-scan


# Or
TG="10.10.10.185";nmap -sV -sC -p`sudo masscan -i tun0 -p0-65535 $TG --rate=1500 |grep open |cut -d ' ' -f 4 |cut -d '/' -f 1 |xargs |tr ' ' ','` $TG -oA quick-scan
```

## massmap

sudo vim /bin/massmap

```shell
#!/bin/bash
TG=$1       # target
INT=$2      # interface

if [[ $# -ne 2 ]];then
    echo "massmap <target> <interface>"
    exit
fi
grc nmap -Pn -sV -sC -p`sudo masscan -i $INT -p0-65535 $TG --rate=1500 --interactive |grep open |cut -d ' ' -f 4 |cut -d '/' -f 1 |xargs |tr ' ' ','` $TG -oA quick-scan
```

sudo chmod +x /bin/massmap
