# Lab 4: SSH Hardening & Intrusion Prevention

## 📖 Scenario
With the *Everett Technologies* infrastructure fully operational, securing the perimeter against automated brute-force attacks is the highest priority. This phase hardens remote administration access by enforcing cryptographic SSH key-pair authentication and deploying Fail2ban to actively monitor logs and ban malicious IP addresses.

## 🎯 Objectives
- Enforce strict directory permissions on SSH configuration files.
- Modify the `sshd_config` file to disable root login and enforce key-only access (disabling passwords).
- Install and configure Fail2ban to protect the SSH daemon.
- Verify security policies by checking active Fail2ban jails and observing authentication rejections.

## 🛠️ Execution Steps

### Phase 1: SSH Key Generation & Server Configuration
*(Note: Key generation is executed on the local client machine. The public key is then transferred to the server's `~/.ssh/authorized_keys` file. Assuming the key is in place, we proceed to harden the server's backend.)*

Ensure the SSH directory has the correct strict permissions before locking down the service:
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### Phase 2: Hardening the SSH Daemon
Edit the core SSH configuration file to disable passwords and root access.
```bash
sudo nano /etc/ssh/sshd_config
```

*Locate and update the following directives to match these exact values:*
```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

Test the configuration for syntax errors and restart the SSH service to apply the new security rules:
```bash
sudo sshd -t
sudo systemctl restart ssh
```

### Phase 3: Installing & Configuring Fail2ban
Install the intrusion prevention system to actively block brute-force attempts.
```bash
sudo apt update
sudo apt install fail2ban -y
```

Create a local configuration override file and add the SSH jail rules:
```bash
sudo nano /etc/fail2ban/jail.local
```

*Paste the following SSH jail configuration:*
```ini
[sshd]
enabled = true
port    = ssh
logpath = %(sshd_log)s
backend = %(sshd_backend)s
maxretry = 5
bantime = 3600
```

Enable and start the Fail2ban service:
```bash
sudo systemctl enable fail2ban
sudo systemctl restart fail2ban
```

### Phase 4: Service Verification
Check the status of the SSH jail to ensure Fail2ban is actively monitoring for threats.
```bash
sudo fail2ban-client status sshd
```

---

## 🧠 Lessons Learned & Troubleshooting

During the deployment of these security measures, several critical administrative challenges were encountered and resolved:

### 1. Configuration Typos & The "Always-Open" Rule
- **Challenge:** A typo was accidentally introduced when modifying the SSH configuration (`PublicAuthentication` instead of `PubkeyAuthentication`). If the service had restarted with this error, it would have crashed and permanently locked out all administrators.
- **Resolution:** By implementing the "Always-Open" rule (keeping the current authenticated terminal session open while testing in a new window) and utilizing the `sshd -t` syntax checker *before* restarting the service, the typo was identified on line 59 and safely corrected without losing server access.

### 2. Missing Privilege Separation Directories
- **Challenge:** After correcting the SSH configuration typo, the `sshd -t` check failed with a `Missing privilege separation directory: /run/sshd` error.
- **Resolution:** Secure services often require temporary runtime directories to manage permissions. This directory was manually created using `sudo mkdir -p /run/sshd`, allowing the service to validate the configuration and restart successfully.

### 3. Fail2ban Configuration Conflicts
- **Challenge:** When verifying the Fail2ban service, the client returned a socket error (`Failed to access socket path`). Log auditing via `systemctl status fail2ban` revealed that the `jail.local` file contained duplicate `[sshd]` section headers, causing the service to panic and crash.
- **Resolution:** Rather than modifying the complex default configuration, the `jail.local` file was completely wiped and replaced with *only* the specific override rules required for the SSH jail. This clean configuration allowed the service to parse the rules correctly and initialize the active monitoring jails.

---

## 📸 Verification & Screenshots

**1. SSH Key Authentication Requirement**
*(Simulating a login attempt without the proper private key)*
![SSH Key Authentication Requirement](../Screenshots/1-SSH-Key-Auth-Requirement.png)

**2. Fail2ban Active Jails**
![Fail2ban Active Jails](../Screenshots/2-Fail2ban-Active-Jails.png)
