# 📁 File Exploration & Data Extraction Cheatsheet
*"The treasure is in the files you don't check" - Anonymous Pentester*

## 🔍 Basic File Inspection

### File Type Identification
```bash
file suspicious.bin          # Determine file type
stat secret.txt             # Show file metadata/timestamps
```
### Text File Examination
```bash
cat file.txt                # View entire file
head -n 20 file.txt         # First 20 lines
tail -n 20 file.txt         # Last 20 lines
grep -i "flag{" file.txt    # Search for flags
strings file.bin | less     # Extract printable strings
```
### Binary Analysis
```bash
xxd file.bin | less         # Hex dump
xxd -r hexdump.txt > out.bin # Reverse hex to binary
hexedit file.bin            # Interactive hex editor
```

## 🗜️ Archive Operations

### ZIP Files
```bash
unzip archive.zip           # Basic extract
unzip -l archive.zip        # List contents without extracting
unzip -P "password" secure.zip  # Password-protected zip
zip -r backup.zip directory/ # Create zip archive
```
### GZ/TAR Files
```bash
tar xvf archive.tar         # Extract tar
tar tvf archive.tar         # List contents
gzip -d file.gz             # Decompress gzip
gunzip file.gz              # Alternative decompression
```
### RAR Files
```bash
unrar x archive.rar         # Extract with full paths
rar a backup.rar directory/ # Create RAR archive
```

## 🔐 Embedded Data Extraction

### Binwalk Analysis
```bash
binwalk suspicious.jpg      # Scan for embedded files
binwalk -e suspicious.jpg   # Auto-extract files
binwalk -Me malware.bin     # Recursive extraction
```
### Steganography Tools
```bash
steghide extract -sf image.jpg  # Extract hidden data (requires passphrase)
stegolsb steglsb -r -i image.png -o output.txt -n 2  # LSB extraction
zsteg hidden.png            # PNG/RGB analysis
```

## 🔥 Hash Cracking

### Identify Hash Types
```bash
hashid '$1$O3JMY.Tw$AdLnLjQ/5jXF9.MTp3gHv/'  # Detect hash type
```
### John The Ripper
```bash
echo "hash_value" > hash.txt
john --format=raw-md5 --wordlist=rockyou.txt hash.txt
```
### Hashcat Examples
```bash
hashcat -m 0 -a 0 hash.txt rockyou.txt        # MD5
hashcat -m 1000 -a 0 hash.txt rockyou.txt     # NTLM
hashcat -m 1800 -a 0 hash.txt rockyou.txt     # sha512crypt
```

## 🕵️‍♂️ Advanced Tricks

## Find Modified Files (Last 24h)
```bash
find / -type f -mtime -1 2>/dev/null | grep -v "proc\|sys"
```
## Search for Hidden Files
```bash
find / -name ".*" -type f ! -path "/proc/*" ! -path "/sys/*" 2>/dev/null
```
## Extract HTTP Endpoints from Files
```bash
grep -rEo '(http|https)://[^/"]+' /path/to/files 2>/dev/null
```
