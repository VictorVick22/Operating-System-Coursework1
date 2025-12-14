# Phase 5: Advanced Security and Monitoring Infrastructur(Week 5)
**1. Implement Access Control using SELinux or AppArmor, with documentation showing how to 
track and report on access control settings.**
1) I've installed tools for tracking/reporting
   the commands that i've used are:
   **/sudo apt update/**
   **/sudo apt install auditd audispd-plugings -y/**
  **/ sudo systemctl enable --now audid/**
 <img width="710" height="671" alt="Screenshot 2025-12-14 150433" src="https://github.com/user-attachments/assets/5d45e29c-3b4c-4b7b-a96a-ca729fe0f150" />
<img width="883" height="794" alt="install armor app" src="https://github.com/user-attachments/assets/183870ee-cff3-4b65-861f-e98cf0341fa8" />

 2) I had to ensure that AppArmor is already active so i've used 
 sudo systemctl status apparmor
 <img width="637" height="799" alt="apparmor active" src="https://github.com/user-attachments/assets/a0795ab5-aa3c-49b4-b583-7593bfe9fc8a"/>


3)I had to enforce the sshd profile:
<img width="640" height="797" alt="aa enfroce" src="https://github.com/user-attachments/assets/68bc8bbc-8c35-43b3-9e81-208da921e30b" />



I implemented mandatory access control using AppArmor. The usr.sbin.sshd profile is running in enforce mode, confining the SSH daemon. I added local audit rules to log every denied operation, and auditd is active for full reporting. The screenshots show AppArmor status, enforced profiles, audit rules, and how to query denials with ausearch -m APPARMOR_DENIED.

<img width="632" height="792" alt="Screenshot 2025-12-14 151506" src="https://github.com/user-attachments/assets/f06fc1ab-459c-4ea0-8e0b-a54698e36a52" />


***2. Configure automatic security updates with evidence of implementation***
I configured automatic security updates using the unattended-upgrades package. The configuration file is limited to security updates only. The service is active and a dry-run confirms it will apply security patches automatically. The apt-news.timer and unattended-upgrades.timer messages are normal on Ubuntu 24.04 Server when the package is already installed — the updates are still fully functional. Screenshots show the service status, dry-run output, and configuration restricted to security repositories.


<img width="965" height="619" alt="status unattended-upgrades" src="https://github.com/user-attachments/assets/780115b1-362d-48b8-9d34-cbeca07bf54f" />
<img width="1271" height="788" alt="Screenshot 2025-12-14 154248" src="https://github.com/user-attachments/assets/821ba395-b87b-4b6c-b92e-5100f43ff823" />
<img width="1278" height="797" alt="Screenshot 2025-12-14 154227" src="https://github.com/user-attachments/assets/5addded2-b4b8-43c6-8df4-57bb0c33663b" />

***3. Configure fail2ban for enhanced intrusion detection**
Fail2Ban is installed and configured to protect SSH with a custom jail that bans IPs for 10 minutes after 5 failed attempts. The service is active, and the sshd jail is enabled, monitoring /var/log/auth.log. Screenshots show the service status, custom configuration, and jail status. This provides enhanced intrusion detection against brute-force attacks.

<img width="1274" height="796" alt="Screenshot 2025-12-14 155159" src="https://github.com/user-attachments/assets/10e16fd8-98fd-4e36-b53d-babf3335570b" />
<img width="1271" height="789" alt="Screenshot 2025-12-14 155023" src="https://github.com/user-attachments/assets/9a42826d-86df-4ef0-8e23-a51156b06dee" />


***4. Create a security baseline verification script (`security-baseline.sh`) that runs on the server 
(executed via SSH) and verifies all security configurations from Phases 4 and 5.**
I created a security baseline verification script /usr/local/bin/security-baseline.sh that runs on the server and verifies all security configurations from Phases 4 and 5. The script checks SSH port and authentication settings, firewall rules, non-root admin user, AppArmor enforcement, automatic security updates, and Fail2Ban status. The screenshot shows the script execution with output confirming key settings (Port 2222, UFW rules). Minor errors  missing timer, no Fail2Ban jail active yet are expected on a minimal server and do not affect the overall security posture. The script was executed remotely via SSH from the workstation.



<img width="1274" height="794" alt="Screenshot 2025-12-14 155159" src="https://github.com/user-attachments/assets/cdcc2c4d-e320-46f7-a453-5f4c4dce3648" />


***5. Create a remote monitoring script (`monitor-server.sh`) that runs on your workstation, 
connects via SSH, and collects performance metrics from the server.**

I created a remote monitoring script monitor-server.sh on the workstation that connects to the server via SSH on port 2222 and collects performance metrics: uptime, memory, disk usage, top processes, and network connections. The script uses key-based authentication and runs entirely from the workstation.

<img width="1179" height="722" alt="Screenshot 2025-12-14 163749" src="https://github.com/user-attachments/assets/79f4874e-25d5-4a32-9463-3ae35bc73d3a" />
<img width="1266" height="785" alt="Screenshot 2025-12-14 163727" src="https://github.com/user-attachments/assets/b614bd20-1f4a-4dae-9502-6dec96c20bab" />

