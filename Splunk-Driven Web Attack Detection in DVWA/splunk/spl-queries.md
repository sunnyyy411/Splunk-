SPL Queries for DVWA Attacks

### 1. Cross-Site Scripting (XSS)

```spl
index=main sourcetype="apache:access"
("alert" OR "<script>" OR "%3Cscript%3E" OR "%3E")
| table _time, client_ip, uri_path, status
```

### 2. SQL Injection

```spl
index=main sourcetype="apache:access"
(id="*1%3D1*" OR id="*OR*" OR id="*%27*")
| table _time, client_ip, uri_path, status
```

### 3. Command Injection

```spl
index=main sourcetype="apache:access"
("ls" OR "whoami" OR "uname" OR ";ls" OR "|uname" OR "&&")
| table _time, client_ip, uri_path, status
```

### 4. Brute Force (Hydra)

```spl
index=main sourcetype=apache:access uri_path="/dvwa/login.php"
| stats count by client_ip
| sort -count
| where count > 10
```

### 5. File Inclusion

```spl
index=main sourcetype=apache:access
| search "/dvwa/vulnerabilities/fi/" "php://filter"
| table _time, client_ip, uri_path, status
```

### 6. Nmap Scan Detection

```spl
index=main sourcetype=apache:access
user_agent="*Nmap Script Engine*"
| stats count by client_ip, user_agent, uri_path, status
```


📌 Note: You will need to manually extract fields (like id, uri_path,client_ip etc.) in Splunk's field extractor to ensure accurate detection and table generation.
