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

