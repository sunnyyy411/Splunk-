# Splunk-Driven Web Attack Detection in DVWA

This project demonstrates how to detect real-world web application attacks using Splunk SIEM. It uses **Kali Linux** as the attacker machine and **Ubuntu** as the target machine running **DVWA (Damn Vulnerable Web Application)** and **Splunk**. The project simulates common web attacks and shows how they are logged and detected in Splunk.

---

## 🔧 Environment Setup

- **Attacker Machine**: Kali Linux (VirtualBox)
- **Target Machine**: Ubuntu (DVWA + Splunk installed) (VirtualBox)
- **Splunk Index Used**: `main`

---

## ⚔️ Simulated Attacks (Total: 6)

Each attack was launched from Kali Linux and detected using SPL queries in Splunk:

1. **Cross-Site Scripting (XSS)**
2. **SQL Injection**
3. **Command Injection**
4. **Brute Force**
5. **File Inclusion**
6. **Nmap Scan**

---

## 📂 Project Structure

```plaintext
Splunk-Driven Web Attack Detection in DVWA/
│
├── README.md
├── setup/
│   ├── dvwa-installation-ubuntu.md
│   ├── splunk-configuration.md 
│   └── kali-attack-scripts.md
│
├── splunk/
    └── spl-queries.md

