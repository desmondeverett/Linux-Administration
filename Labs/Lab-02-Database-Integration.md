# Lab 2: Enterprise Database Integration (MariaDB/MySQL)

## 📖 Scenario
*Everett Technologies* requires a secure, robust backend database to support their upcoming dynamic web applications. Building upon the web server established in Lab 1, this phase completes the LAMP (Linux, Apache, MySQL/MariaDB, PHP) stack by provisioning a dedicated database service account and verifying connectivity.

## 🎯 Objectives
- Install MariaDB and PHP-MySQL extensions.
- Secure the database using enterprise best practices (`mysql_secure_installation`).
- Provision a dedicated service account and database for web applications, enforcing the Principle of Least Privilege.
- Verify backend connectivity via a custom PHP script.

## 🛠️ Execution Steps

### Phase 1: Installation & Service Verification
```bash
sudo apt update
sudo apt install mariadb-server php-mysql -y
sudo systemctl enable mariadb
sudo systemctl status mariadb
```

### Phase 2: Securing the Database
*Note: Modern Debian deployments secure MariaDB by default during installation (enforcing `unix_socket` authentication and removing test databases). Manual execution of the `mariadb-secure-installation` script was bypassed as per Debian OS documentation.*

### Phase 3: Provisioning a Service Account
```sql
CREATE DATABASE everett_db;
CREATE USER 'everett_admin'@'localhost' IDENTIFIED BY 'Password123!';
GRANT ALL PRIVILEGES ON everett_db.* TO 'everett_admin'@'localhost';
FLUSH PRIVILEGES;
exit;
```

### Phase 4: PHP Connectivity Test
```bash
sudo nano /var/www/html/db_test.php
```

```php
<?php
$servername = "localhost";
$username = "everett_admin";
$password = "Password123!";
$dbname = "everett_db";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
  die("Connection failed: " . $conn->connect_error);
}
echo "<h2>Everett Technologies Database Connection: SUCCESS!</h2>";
?>
```

```bash
sudo systemctl restart apache2
curl http://localhost/db_test.php
```

---
## 🧠 Lessons Learned & Troubleshooting

During the execution of this lab, several real-world administrative challenges were encountered and successfully resolved:

### 1. OS-Level Security vs. Manual Hardening
- **Challenge:** Attempting to run the traditional `sudo mariadb-secure-installation` hardening script resulted in an `Error 2002 (HY000): Can't connect to local server through socket` failure.
- **Resolution:** By reading the OS-level terminal warnings, it was determined that modern Debian distributions automatically secure the MariaDB installation out-of-the-box (enforcing `unix_socket` authentication and stripping test databases). Rather than forcing a redundant script, manual execution was bypassed in accordance with Debian OS documentation.

### 2. Silent PHP Crashes & Log Auditing
- **Challenge:** Executing the `curl http://localhost/db_test.php` command to verify backend connectivity returned a completely blank terminal response rather than a visible web error or success message.
- **Resolution:** To diagnose the silent crash, we audited the internal Apache error logs (`sudo tail -n 5 /var/log/apache2/error.log`). 
- **Root Cause:** The logs revealed a hidden `PHP Fatal error: Access denied for user`. This indicated a password mismatch between the newly provisioned MariaDB service account and the `$password` variable hardcoded into the PHP script. Updating the variable in the PHP file to correctly match the SQL configuration instantly resolved the authentication failure.

---
## 📸 Verification & Screenshots

**1. MariaDB Service Status**
![MariaDB Service Status](../Screenshots/1-mariaDB-Service-Status.png)

**2. PHP Database Connectivity Test**
![PHP Database Connectivity Test](../Screenshots/2-PHP-Database-Connectivity.png)
