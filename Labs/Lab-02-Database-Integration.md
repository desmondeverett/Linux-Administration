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
- sudo apt update
- sudo apt install mariadb-server php-mysql -y
- sudo systemctl enable mariadb
- sudo systemctl status mariadb

### Phase 2: Securing the Database
Modern Debian deployments secure MariaDB by default during installation (enforcing unix_socket authentication and removing test databases). Manual execution of the mariadb-secure-installation script was bypassed as per Debian OS documentation.

### Phase 3: Provisioning a Service Account
- CREATE DATABASE everett_db;
- CREATE USER 'everett_admin'@'localhost' IDENTIFIED BY 'StrongPassword123!';
- GRANT ALL PRIVILEGES ON everett_db.* TO 'everett_admin'@'localhost';
- FLUSH PRIVILEGES;
- exit;*(Documentation notes and commands will be logged here)*

### Phase 4: PHP Connectivity Test
- sudo nano /var/www/html/db_test.php
- <?php
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
- sudo systemctl restart apache2
- curl http://localhost/db_test.php

---

## 📸 Verification & Screenshots

**1. MariaDB Service Status**
*(Insert Active Database Service Screenshot Here)*

**2. PHP Database Connectivity Test**
*(Insert Web/DB Connection Success Screenshot Here)*
