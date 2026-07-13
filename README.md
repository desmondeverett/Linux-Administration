# Linux-Administration
Enterprise Linux administration portfolio featuring LAMP stack deployments, bash automation, and open-source security configurations for the simulated *Everett Technologies* corporate infrastructure.

## 🛠️ Linux Administration Lab Topology & Roadmap

### ✅ Lab 1: Enterprise Web Server (LAMP Stack)
- **Status:** ✅ Completed
- **Documentation:** [View Lab Documentation](./Labs/Lab-01-Enterprise-Web-Server.md)
- **Description:** Provisioning a Debian-based Linux server, configuring an Apache web server, and securing the perimeter with UFW (Uncomplicated Firewall) to host Everett Technologies' external assets.

### 📸 Lab 1 Verification

**1. Apache Service Verification**
![Apache Status](<./Screenshots/1. Apache Service Verifivation.png>)

**2. UFW Active Ruleset**
![UFW Status](<./Screenshots/2. UFW Active Ruleset.png>)

**3. Everett Technologies Landing Page**
![Web Page Verification](<./Screenshots/3. Everett Technologies Landing Page.png>)

---

---

### 🚧 Lab 2: Database Integration (MariaDB/MySQL)
- **Status:** ⏳ In Progress
- **Documentation:** *Coming Soon*
- **Description:** Securing and configuring a backend MariaDB database for Everett Technologies' web applications, including service account creation and PHP connectivity testing to complete the LAMP stack.

#### 📸 Lab 2 Verification
**1. MariaDB Service Status**
*[Screenshot: Active Database Service - Coming Soon]*

**2. PHP Database Connectivity Test**
*[Screenshot: Web/DB Connection Success - Coming Soon]*

---

### 📅 Lab 3: Automated Server Backups (Bash & Cron)
- **Status:** 🗓️ Planned
- **Documentation:** *Coming Soon*
- **Description:** Developing custom Bash scripts to archive `/var/www/html` and Apache configurations, scheduled via cron jobs for automated nightly disaster recovery.

#### 📸 Lab 3 Verification
**1. Active Cron Job Schedule**
*[Screenshot: Crontab Output - Coming Soon]*

**2. Successful Archive Creation**
*[Screenshot: .tar.gz File Verification - Coming Soon]*

---

### 📅 Lab 4: SSH Hardening & Intrusion Prevention
- **Status:** 🗓️ Planned
- **Documentation:** *Coming Soon*
- **Description:** Hardening remote access by enforcing SSH key-pair authentication and deploying Fail2ban to actively mitigate automated brute-force attacks against the server.

#### 📸 Lab 4 Verification
**1. SSH Key Authentication Requirement**
*[Screenshot: Password Authentication Denied - Coming Soon]*

**2. Fail2ban Active Jails**
*[Screenshot: Fail2ban Status Output - Coming Soon]*

---

## 📁 Repository Directory Structure
- **/Labs** — Step-by-step markdown documentation, lessons learned, and verification walkthroughs.
- **/Screenshots** — Visual proof of successful command outputs, bash scripts, and system configurations.
- **/Scripts** — Custom Bash automation and provisioning scripts.

---

## 📁 Repository Directory Structure
- **/Labs** — Step-by-step markdown documentation, lessons learned, and verification walkthroughs.
- **/Screenshots** — Visual proof of successful command outputs, bash scripts, and system configurations.
- **/Scripts** — Custom Bash automation and provisioning scripts.
