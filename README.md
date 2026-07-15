# Linux-Administration

Deployment documentation and standard operating procedures (SOPs) for the enterprise Linux infrastructure, featuring LAMP stack deployments, bash automation, and open-source security configurations for Everett Technologies.

## 🛠️ Infrastructure Topology & Deployment Roadmap

## ✅ Phase 1: Enterprise Web Server (LAMP Stack) Provisioning
- **Status:** ✅ Completed
- **Documentation:** View Phase 1 SOP
- **Description:** Provisioning a Debian-based Linux server, configuring an Apache web server, and securing the perimeter with UFW (Uncomplicated Firewall) to host Everett Technologies' external assets.

### 📸 Phase 1 Quality Assurance (QA) Validation

*1. Apache Service Verification*
![Apache Status](Screenshots/1.%20Apache%20Service%20Verifivation.png)

*2. UFW Active Ruleset*
![UFW Status](Screenshots/2.%20UFW%20Active%20Ruleset.png)

*3. Everett Technologies Landing Page*
![Web Page Verification](Screenshots/3.%20Everett%20Technologies%20Landing%20Page.png)

## ✅ Phase 2: Database Integration (MariaDB/MySQL)
- **Status:** ✅ Completed
- **Documentation:** View Phase 2 SOP
- **Description:** Securing and configuring a backend MariaDB database for Everett Technologies' web applications, including service account creation and PHP connectivity testing to complete the LAMP stack.

### 📸 Phase 2 Quality Assurance (QA) Validation

*1. MariaDB Service Status*
![MariaDB Service Status](Screenshots/1-mariaDB-Service-Status.png)

*2. PHP Database Connectivity Test*
![PHP Database Connectivity Test](Screenshots/2-PHP-Database-Connectivity.png)

## ✅ Phase 3: Automated Server Backups (Bash & Cron)
- **Status:** ✅ Completed
- **Documentation:** View Phase 3 SOP
- **Description:** Developing custom Bash scripts to archive /var/www/html and Apache configurations, scheduled via cron jobs for automated nightly disaster recovery.

### 📸 Phase 3 Quality Assurance (QA) Validation

*1. Successful Archive Creation*
![Successful Archive Creation](Screenshots/1-Successful-Archive-Creation.png)

*2. Active Cron Job Schedule*
![Active Cron Job Schedule](Screenshots/2-Active-Cron-Job-Schedule.png)

## ✅ Phase 4: SSH Hardening & Intrusion Prevention
- **Status:** ✅ Completed
- **Documentation:** View Phase 4 SOP
- **Description:** Hardening remote access by enforcing SSH key-pair authentication and deploying Fail2ban to actively mitigate automated brute-force attacks against the server.

### 📸 Phase 4 Quality Assurance (QA) Validation

*1. SSH Key Authentication Requirement*
![SSH Key Authentication Requirement](Screenshots/1-SSH-Key-Auth-Requirement.png)

*2. Fail2ban Active Jails*
![Fail2ban Active Jails](Screenshots/2-Fail2ban-Active-Jails.png)

## 📁 Repository Directory Structure
- **/SOPs** — Step-by-step deployment documentation, bash scripts, and configuration guides.
- **/Screenshots** — Visual QA validation of successful command outputs, active cron schedules, and system configurations.
