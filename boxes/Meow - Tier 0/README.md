# MEOW

STARTING POINT - TIER 0

## Enumeration

**Nmap scan**

```bash
nmap -sC -sV 10.129.7.236
```

![nmap](pics/nmap.png)

## Exploitation

**Connect to Telnet Server**

```bash
telnet 10.129.7.236
```

![telnet](pics/telnet.png)

**list all contents**

```bash
ls
```

![ls](pics/ls.png)

**Get flag**

```bash
cat flag.txt
```
