# DVWA Installation on Ubuntu (Step-by-Step Guide)

This guide walks through installing Damn Vulnerable Web Application (DVWA) on Ubuntu with step-by-step explanations.

---

## 📦 Step 1: Install Dependencies

```bash
sudo apt update
```

> Updates the package lists to ensure you're installing the latest versions.

```bash
sudo apt install apache2 mysql-server php php-mysqli php-gd libapache2-mod-php git -y
```

> Installs Apache (web server), MySQL (database), PHP (scripting language), required PHP extensions, and Git.

---

## 📁 Step 2: Clone DVWA Repository

```bash
cd /var/www/html
```

> Navigates to the web server root directory.

```bash
sudo git clone https://github.com/digininja/DVWA.git
```

> Clones the DVWA source code from GitHub.

```bash
cd DVWA
```

> Enters the DVWA directory.

```bash
sudo cp config/config.inc.php.dist config/config.inc.php
```

> Copies the default configuration file for editing.

---

## 🛠️ Step 3: Configure MySQL Database

```bash
sudo mysql
```

> Opens the MySQL shell.

Inside the MySQL shell:

```sql
CREATE DATABASE dvwa;
```

> Creates a new database named `dvwa`.

```sql
CREATE USER 'dvwa'@'localhost' IDENTIFIED BY 'dvwa';
```

> Creates a MySQL user `dvwa` with password `dvwa`.

```sql
GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa'@'localhost';
```

> Grants the user full access to the `dvwa` database.

```sql
FLUSH PRIVILEGES;
```

> Applies the changes.

```sql
EXIT;
```

> Exits the MySQL shell.

---

## ✏️ Step 4: Configure DVWA Settings

```bash
sudo nano config/config.inc.php
```

> Opens the configuration file in nano editor.

**Edit the following lines:**

```php
$_DVWA[ 'db_user' ] = 'dvwa';
$_DVWA[ 'db_password' ] = 'dvwa';
```

> Sets the database credentials for DVWA.

---

## 🔐 Step 5: Set File Permissions

```bash
sudo chown -R www-data:www-data /var/www/html/DVWA
```

> Changes file ownership to Apache’s user and group.

```bash
sudo chmod -R 755 /var/www/html/DVWA
```

> Sets directory permissions for proper access.

---

## 🔁 Step 6: Enable Apache Rewrite Module

```bash
sudo a2enmod rewrite
```

> Enables URL rewriting, which is required for DVWA.

```bash
sudo systemctl restart apache2
```

> Restarts Apache to apply changes.

---

## 🌐 Step 7: Launch DVWA in Browser

Open your browser and navigate to:

```
http://localhost/DVWA
```

Or on another machine:

```
http://<Ubuntu-IP>/DVWA
```

> Then click on "Create Database" in the DVWA UI.

---

## 🔄 Reopen DVWA After Reboot

1. Start services:

```bash
sudo systemctl start apache2
sudo systemctl start mysql
```

> These services may not auto-start on reboot.

2. Access DVWA in browser:

```
http://localhost/DVWA
```

> Or from another device on the same network:

```
http://<Ubuntu-IP>/DVWA
```
