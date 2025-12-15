# Phase 7: Security Audit and System Evaluation (Week 7)
Lynis (version 3.0.9) was run on the hardened Ubuntu 24.04 LTS server, completing 257 tests. The hardening index scored 67/100, reflecting a solid configuration with strong firewall and SSH protections. Suggestions included tightening file permissions and kernel settings. Key positives were proper UFW usage, minimal services, and no critical vulnerabilities.
<img width="628" height="793" alt="Screenshot 2025-12-15 133122" src="https://github.com/user-attachments/assets/be94db1d-b766-4289-90fa-8b722ff9142e" />
<img width="629" height="788" alt="Screenshot 2025-12-15 133016" src="https://github.com/user-attachments/assets/b82db0ff-4b25-4c35-b658-ed3a04747647" />
<img width="630" height="786" alt="Screenshot 2025-12-15 132957" src="https://github.com/user-attachments/assets/b899512a-2a08-4966-b48d-984196e7e48e" />
<img width="629" height="595" alt="Screenshot 2025-12-15 132938" src="https://github.com/user-attachments/assets/47e5a995-72e8-4448-8779-24b517de6b3b" />
<img width="632" height="759" alt="Screenshot 2025-12-15 132914" src="https://github.com/user-attachments/assets/60c06563-db57-4bc6-a55e-6c700093db50" />
<img width="633" height="762" alt="Screenshot 2025-12-15 132857" src="https://github.com/user-attachments/assets/567df697-d15f-42fd-a7e2-f2b9830140c1" />
<img width="637" height="797" alt="Screenshot 2025-12-15 132835" src="https://github.com/user-attachments/assets/52866a7b-eff4-4b2f-a683-7c0f7c882e85" />




**Network security assessment with nmap**
nmap was executed from the workstation against 192.168.56.101. The full port scan showed 65534 closed ports and only 2222/tcp open for OpenSSH 9.6p1. Service version scan confirmed SSH protocol 2.0 and Linux kernel detection. UFW rules effectively filter all other traffic. This minimal exposure confirms a secure network posture.
<img width="624" height="716" alt="Screenshot 2025-12-15 133229" src="https://github.com/user-attachments/assets/a865174c-8b67-41ea-b992-2e537e33c08c" />
<img width="631" height="799" alt="Screenshot 2025-12-15 133156" src="https://github.com/user-attachments/assets/58e27c07-14ae-4283-b577-03289a8ef78b" />



**Access control verification**

UFW is active with deny-by-default incoming policy, allowing SSH on 2222 only from 192.168.56.10. AppArmor has 156 profiles loaded, 155 in enforce mode, including SSH. SSH config enforces key-only authentication, disables root login, and uses public keys. Fail2Ban monitors SSH with no current bans. These layers ensure strong, restricted access control.
<img width="629" height="756" alt="Screenshot 2025-12-15 133303" src="https://github.com/user-attachments/assets/3d499986-58c5-4a96-a76d-f3c92f24d0be" />
<img width="631" height="761" alt="Screenshot 2025-12-15 133422" src="https://github.com/user-attachments/assets/e8bbde15-05bc-4576-9703-47b0d54edb01" />
<img width="634" height="761" alt="Screenshot 2025-12-15 133335" src="https://github.com/user-attachments/assets/b93e4c00-47a0-4407-b90a-08236d83d8b5" />

**Service Audit and Justification**
Running services were audited via systemctl and ss -tulnp. Core services include sshd (remote access), ufw (firewall), fail2ban (intrusion prevention), and unattended-upgrades (patching). Desktop-related services (GNOME, cups, avahi) are present due to the install type. All are justified for functionality or security. No unnecessary services were found, minimizing the attack surface.
<img width="638" height="745" alt="Screenshot 2025-12-15 133625" src="https://github.com/user-attachments/assets/78b32654-1b5f-48ee-a391-b27a396478e1" />
<img width="632" height="758" alt="Screenshot 2025-12-15 133541" src="https://github.com/user-attachments/assets/02a0d5ee-e18b-4ad4-a171-c1b272e31465" />
<img width="634" height="760" alt="Screenshot 2025-12-15 133525" src="https://github.com/user-attachments/assets/83d49840-e8e5-45c2-b81f-887d2f9d681f" />
<img width="631" height="763" alt="Screenshot 2025-12-15 133445" src="https://github.com/user-attachments/assets/47ec4bc0-8c41-4c0f-8a91-b716a7663807" />

**System Configuration Review**
The server runs Ubuntu 24.04.3 LTS with kernel 6.14.0-37-generic. UFW is active with restricted rules and logging enabled. Fail2Ban sshd jail is operational with no bans. Automatic updates are configured for security patches. The configuration is secure, up-to-date, and suitable for lab use.


<img width="640" height="791" alt="Screenshot 2025-12-15 133744" src="https://github.com/user-attachments/assets/c7eb3d32-dbbe-4c7d-bc7d-c75072568b2d" />
<img width="628" height="791" alt="Screenshot 2025-12-15 133713" src="https://github.com/user-attachments/assets/cff5252f-22b4-46c2-a21d-6b865682f78e" />
