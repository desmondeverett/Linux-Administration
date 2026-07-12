## Installation Steps

### Phase 1: Core System & Apache Installation
1. Update system repositories and install Apache2 using `sudo apt update && sudo apt install apache2 -y`.
2. Verify the Apache service is active and enabled on boot.

### Phase 2: Uncomplicated Firewall (UFW) Configuration
1. Allow OpenSSH, HTTP (Port 80), and HTTPS (Port 443).
2. Enable the firewall and verify the active ruleset using `sudo ufw enable` and `sudo ufw status verbose`.

### Phase 3: Enterprise Landing Page Deployment
1. Navigate to the default web directory (`/var/www/html/`).
2. Replace the default Debian Apache page with a custom HTML file confirming the server's identity and operational status.

> ## Outcome
> 
> The provisioning of the Debian-based Linux server (ET-WEB01) was completed successfully. The Apache web service was installed, the local perimeter was secured with UFW, and a custom organizational landing page was deployed to host Everett Technologies' external web assets.

## Lessons Learned

- **Service Management:** Demonstrated the ability to deploy and verify daemon states using `systemctl`, ensuring critical infrastructure remains highly available.
- **Perimeter Security:** Applied the Principle of Least Privilege to the server's network interfaces, tightly controlling inbound traffic using UFW.
- **Open-Source Hosting:** Successfully bridged command-line configuration with a live, accessible web asset for the organization.

### 🔧 Troubleshooting & Resolutions
- **Dormant Services on Install:** Encountered an issue where the Apache web server did not automatically start after installation. *Resolution:* Identified that security-focused distributions (like Kali Linux) restrict network daemons from auto-starting to prevent accidental exposure. Manually forced the daemon to start and enable on boot using `sudo systemctl enable --now apache2`.
- **Missing Core Utilities:** Received a `command not found` error when attempting to configure the UFW firewall. *Resolution:* Recognized that Kali Linux utilizes raw `iptables` by default and lacks the UFW package out-of-the-box. Rectified this by manually pulling the package from the repositories via `sudo apt install ufw -y`.
- **Markdown Rendering Issues:** Screenshots initially failed to render in the GitHub repository due to broken pathing. *Resolution:* Corrected the relative file paths by utilizing `../` to traverse up a directory level and applied `%20` URL encoding to handle spaces in the image filenames, successfully restoring the documentation visuals.

## Screenshots

## 1. Apache Service Verification
![Apache Status](../Screenshots/1.%20Apache%20Service%20Verifivation.png)

## 2. UFW Active Ruleset
![UFW Status](../Screenshots/2.%20UFW%20Active%20Ruleset.png)

## 3. Everett Technologies Landing Page
![Web Page Verification](../Screenshots/3.%20Everett%20Technologies%20Landing%20Page.png)
