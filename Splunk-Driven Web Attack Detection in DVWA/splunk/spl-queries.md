SPL Queries for DVWA Attacks

### 1. Cross-Site Scripting (XSS)

```spl
index=main sourcetype="apache:access"
("alert" OR "<script>" OR "%3Cscript%3E" OR "%3E")
| table _time, client_ip, uri_path, status
```
![image](https://github.com/user-attachments/assets/0cc06781-b28e-47ec-8522-37356f73b19d)


### 2. SQL Injection

```spl
index=main sourcetype="apache:access"
(id="*1%3D1*" OR id="*OR*" OR id="*%27*")
| table _time, client_ip, uri_path, status
```
![image](https://github.com/user-attachments/assets/3e39d7e8-00ca-4518-b4a6-72dd648d2fb5)



### 3. Command Injection

```spl
index=main sourcetype="apache:access"
("ls" OR "whoami" OR "uname" OR ";ls" OR "|uname" OR "&&")
| table _time, client_ip, uri_path, status
```
![image](https://github.com/user-attachments/assets/f8dd160c-8caa-475c-bd2d-6e919eae6316)


### 4. Brute Force (Hydra)

```spl
index=main sourcetype=apache:access uri_path="/dvwa/login.php"
| stats count by client_ip
| sort -count
| where count > 10
```
![image](https://github.com/user-attachments/assets/0548cb3f-47db-4fe5-91ee-4b8fae6fd9c5)


### 5. File Inclusion

```spl
index=main sourcetype=apache:access
| search "/dvwa/vulnerabilities/fi/" "php://filter"
| table _time, client_ip, uri_path, status
```
![image](https://github.com/user-attachments/assets/4750bd04-5209-4d7f-b3eb-98f673a36f0a)


### 6. Nmap Scan Detection

```spl
index=main sourcetype=apache:access
user_agent="*Nmap Script Engine*"
| stats count by client_ip, user_agent, uri_path, status
```
![image](https://github.com/user-attachments/assets/8832b14f-4d32-4a27-a4cb-c29da24e2a69)



📌 Note: You will need to manually extract fields (like id, uri_path,client_ip etc.) in Splunk's field extractor to ensure accurate detection and table generation.
