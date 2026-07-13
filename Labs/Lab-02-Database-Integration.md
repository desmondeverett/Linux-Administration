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
- CREATE DATABASE everett_db;
- CREATE USER 'everett_admin'@'localhost' IDENTIFIED BY 'StrongPassword123!';
- GRANT ALL PRIVILEGES ON everett_db.* TO 'everett_admin'@'localhost';
- FLUSH PRIVILEGES;
- exit;

### Phase 3: Provisioning a Service Account
*(Documentation notes and commands will be logged here)*

### Phase 4: PHP Connectivity Test
*(Documentation notes and commands will be logged here)*

---

## 📸 Verification & Screenshots

**1. MariaDB Service Status**
*(Insert Active Database Service Screenshot Here)*

**2. PHP Database Connectivity Test**
*(Insert Web/DB Connection Success Screenshot Here)*
