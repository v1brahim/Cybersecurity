# 🕵️ Forensics Cheatsheet

## Binary Extraction
```bash
binwalk -e file.bin
foremost -i image.jpg -o output/
```

## Metadata Analysis
```bash
exiftool image.jpg
```

## Steganography
```bash
steghide extract -sf image.jpg
zsteg file.png
```

## Memory Analysis (Volatility)
```bash
volatility -f mem.dmp --profile=Win10x64_18362 pslist
volatility -f mem.dmp --profile=Win10x64_18362 strings
```