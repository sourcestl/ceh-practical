# CEH Practical Cheat Sheet

## 1. Enumeration & Reconnaissance

### Identify Live Hosts on a Subnet
```bash
nmap -sn 192.168.0.0/24
```

### Detect Open Ports
```bash
nmap -p- 192.168.0.X
```

### Find a Domain Controller
```bash
nmap -p 389,636,88,3268 192.168.0.0/24
```

### Get NetBIOS Name and FQDN
```bash
nmap -sC 192.168.0.X --top-ports=20
```

### Find OpenSSH Version
```bash
nmap -p 22 192.168.0.0/24 --open -T5 -sV
```

### Detect Operating System

**Step 1: Find an Open Port**
```bash
nmap -p 3306 192.168.0.X --open
```

**Step 2: OS Detection**
```bash
nmap -O 192.168.0.X -sV -T5
```

### LDAP Enumeration (User Count)
```bash
nmap 192.168.0.X --script=*user*
```

### Get LDAP Version
```bash
ldapsearch -x -H ldap://192.168.0.X
```

---

## 2. Service Discovery

### Check Whether NFS is Enabled
```bash
nmap -p 111 192.168.0.0/24 --open
```

### DNS Enumeration
```bash
nslookup -type=ns www.certifiedhacker.com
```

### Find SMTP Servers
```bash
nmap -p 25 192.168.0.0/24 --open -T5
```

### SMB Enumeration (Message Signing)
```bash
nmap -p 445 192.168.0.X -sC -T5
```

---

## 3. Password Attacks

### Crack NTLM Hashes
```bash
john hashes.txt --format=NT --wordlist=password.txt
```

### FTP Brute Force
```bash
hydra -L Username.txt -P Passwords.txt 172.16.0.12 ftp
```

### Download Files from FTP
```bash
ftp 172.16.0.12
ftp> ls
ftp> mget *
cat flag.txt
```
