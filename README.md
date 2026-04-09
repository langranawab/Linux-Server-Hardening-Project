Linux Server Hardening & Brute Force Protection (SSH + UFW + Fail2Ban)

 Project Overview
This project demonstrates practical Linux defensive security by hardening SSH access, configuring firewall rules, monitoring authentication logs, and implementing automated brute-force protection using Fail2Ban.
The goal was to simulate a real-world server environment where SSH is commonly targeted by attackers and apply security best practices to protect the system.

 Objectives
•	Secure SSH remote access 
•	Reduce attack surface by changing default SSH port 
•	Restrict SSH login to specific users 
•	Disable root SSH login 
•	Configure firewall rules using UFW 
•	Monitor SSH login attempts via logs 
•	Implement brute-force protection using Fail2Ban 
•	Test security using real remote access (Termux) 
________________________________________
 Tools & Technologies Used
•	Kali Linux (Rolling) 
•	OpenSSH Server 
•	UFW Firewall 
•	Fail2Ban 
•	systemctl (Systemd) 
•	journalctl (log monitoring) 
•	auth.log analysis 
•	Termux (Android) for remote SSH testing
 Security Implementation Steps
 Install and Enable SSH
sudo apt update
sudo apt install openssh-server -y
sudo systemctl start ssh
sudo systemctl enable ssh
sudo systemctl status ssh
________________________________________
 SSH Hardening (sshd_config)
Edit SSH config:
sudo nano /etc/ssh/sshd_config
Applied security settings:
Port 2222
PermitRootLogin no
AllowUsers selenophile test
Validate and restart:
sudo sshd -t
sudo systemctl restart ssh
Check SSH port:
sudo ss -tulnp | grep 2222
________________________________________
 Configure Firewall (UFW)
Allow only SSH port 2222:
sudo ufw allow 2222/tcp
sudo ufw deny 22/tcp
sudo ufw enable
sudo ufw status verbose
________________________________________
 Log Monitoring (Authentication Logs)
Check SSH logs:
sudo tail -n 20 /var/log/auth.log
sudo journalctl -u ssh --since today | tail -n 20
Failed attempts:
sudo grep "Failed password" /var/log/auth.log
Successful attempts:
sudo grep "Accepted password" /var/log/auth.log
________________________________________



Install and Configure Fail2Ban
Install Fail2Ban:
sudo apt install fail2ban -y
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
Create jail.local:
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo nano /etc/fail2ban/jail.local
Configure SSH jail:
[sshd]
enabled = true
port = 2222
logpath = /var/log/auth.log
maxretry = 3
findtime = 600
bantime = 600
Restart Fail2Ban:
sudo systemctl restart fail2ban
Check status:
sudo fail2ban-client status
sudo fail2ban-client status sshd
________________________________________
Testing & Validation
SSH login test from another device (Termux)
ssh -p 2222 username@<server-ip>
After entering wrong password 3 times, Fail2Ban banned the IP.
Check banned IP:
sudo fail2ban-client status sshd
Unban IP:
sudo fail2ban-client set sshd unbanip <IP_ADDRESS>
________________________________________
Results Achieved
SSH port changed from 22 to 2222
Root login disabled
SSH access restricted to allowed users
 Firewall configured to allow only required ports
Logs monitored for failed and successful login attempts
Fail2Ban successfully banned attacker IP after brute-force attempts
Real testing completed using Termux (Android)
________________________________________
 Skills Demonstrated
•	Linux Administration 
•	SSH Hardening & Security 
•	Firewall Configuration (UFW) 
•	Log Monitoring & Filtering 
•	Brute Force Prevention (Fail2Ban) 
•	Real-world troubleshooting and validation
 Security Implementation Steps
Install and Enable SSH
sudo apt update
sudo apt install openssh-server -y
sudo systemctl start ssh
sudo systemctl enable ssh
sudo systemctl status ssh
________________________________________
SSH Hardening (sshd_config)
Edit SSH config:
sudo nano /etc/ssh/sshd_config
Applied security settings:
Port 2222
PermitRootLogin no
AllowUsers selenophile test
Validate and restart:
sudo sshd -t
sudo systemctl restart ssh
Check SSH port:
sudo ss -tulnp | grep 2222
________________________________________
 Configure Firewall (UFW)
Allow only SSH port 2222:
sudo ufw allow 2222/tcp
sudo ufw deny 22/tcp
sudo ufw enable
sudo ufw status verbose
________________________________________
 Log Monitoring (Authentication Logs)
Check SSH logs:
sudo tail -n 20 /var/log/auth.log
sudo journalctl -u ssh --since today | tail -n 20
Failed attempts:
sudo grep "Failed password" /var/log/auth.log
Successful attempts:
sudo grep "Accepted password" /var/log/auth.log
________________________________________
 Install and Configure Fail2Ban
Install Fail2Ban:
sudo apt install fail2ban -y
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
Create jail.local:
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo nano /etc/fail2ban/jail.local
Configure SSH jail:
[sshd]
enabled = true
port = 2222
logpath = /var/log/auth.log
maxretry = 3
findtime = 600
bantime = 600



Restart Fail2Ban:
sudo systemctl restart fail2ban
Check status:
sudo fail2ban-client status
sudo fail2ban-client status sshd
________________________________________
Testing & Validation
SSH login test from another device (Termux)
ssh -p 2222 username@<server-ip>
After entering wrong password 3 times, Fail2Ban banned the IP.
Check banned IP:
sudo fail2ban-client status sshd
Unban IP:
sudo fail2ban-client set sshd unbanip <IP_ADDRESS>
________________________________________
 Results Achieved
SSH port changed from 22 to 2222
Root login disabled
SSH access restricted to allowed users
Firewall configured to allow only required ports
Logs monitored for failed and successful login attempts
Fail2Ban successfully banned attacker IP after brute-force attempts
Real testing completed using Termux (Android)
________________________________________


 

 
 Skills Demonstrated
•	Linux Administration 
•	SSH Hardening & Security 
•	Firewall Configuration (UFW) 
•	Log Monitoring & Filtering 
•	Brute Force Prevention (Fail2Ban) 
•	Real-world troubleshooting and validation

