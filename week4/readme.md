***Phase 4: Initial System Configuration & Security Implementation (Week 4)**
**1. Configure SSH with key-based authentication**
<img width="635" height="800" alt="Screenshot 2025-12-11 180106" src="https://github.com/user-attachments/assets/938e7124-0ab2-44eb-ab0b-48aff7041e62" />
<img width="638" height="800" alt="Screenshot 2025-12-11 175949" src="https://github.com/user-attachments/assets/bbb24334-1e52-4949-b428-6f46bb75cf96" />
<img width="638" height="800" alt="Screenshot 2025-12-11 175812" src="https://github.com/user-attachments/assets/1fc3edb7-f8c9-401e-9f80-25b0da11ecf4" />
<img width="639" height="800" alt="Screenshot 2025-12-11 175418" src="https://github.com/user-attachments/assets/55e7c4fc-9974-4098-b84f-c3bf77247e52" />




**2. Configure a firewall permitting SSH from one specific workstation only**


<img width="1273" height="797" alt="Screenshot 2025-12-11 185926" src="https://github.com/user-attachments/assets/358b09c3-0fd1-44a5-b531-742c9223b0eb" />


**3. Manage users and implement privilege management, creating a non-root administrative 
user.**

<img width="638" height="800" alt="Screenshot 2025-12-11 175328" src="https://github.com/user-attachments/assets/b8caa08f-434d-423b-a2fe-a3c23b469c8a" />
<img width="603" height="799" alt="Screenshot 2025-12-11 175302" src="https://github.com/user-attachments/assets/5fa3ecfe-5d84-41a4-9ad7-5cd270f9b329" />
<img width="638" height="800" alt="Screenshot 2025-12-11 175229" src="https://github.com/user-attachments/assets/23b758c8-d883-4811-a978-f34cd0e284de" />


**4. SSH Access Evidence showing successful connection screenshots**

1)No password required:
<img width="632" height="800" alt="nopassword" src="https://github.com/user-attachments/assets/9522998a-c67d-40f7-9d06-10e4b6c97df2" />

Proves that i am on server:

<img width="629" height="794" alt="Screenshot 2025-12-11 192352" src="https://github.com/user-attachments/assets/08746c18-b402-40ac-9848-287cdf76cc25" />

<img width="1273" height="797" alt="Screenshot 2025-12-11 185926" src="https://github.com/user-attachments/assets/5ab858ef-deaa-4232-ad80-f2bedffb37f1" />

**5. Configuration Files with before and after comparisons**

Unfortunately, I forgot to take screenshots of the original configuration files before applying the hardening changes.
The default Ubuntu 24.04 Server configuration uses port 22, allows password authentication, permits root login with password, and ships with UFW inactive.
These are the standard settings for a fresh Ubuntu Server installation and are well-documented in the official Ubuntu Server Guide.
The ‘after’ screenshots attached clearly show the final hardened state: SSH listening exclusively on port 2222, PasswordAuthentication no, PermitRootLogin no, a systemd override forcing the custom port, and UFW configured to allow SSH only from my workstation (192.168.56.10).
The contrast between the default settings and the current secure configuration is therefore still fully evident.

 1. Current SSH config:

<img width="626" height="797" alt="Screenshot 2025-12-11 193152" src="https://github.com/user-attachments/assets/75c6baae-19a8-4639-9dd3-fb32bdbcb51b" />


2. Systemd override forcing port 2222

<img width="626" height="791" alt="2" src="https://github.com/user-attachments/assets/514d2ad5-3a7a-45e9-945c-bf00003b775c" />


 3. SSH really listening only on 2222


<img width="623" height="794" alt="3" src="https://github.com/user-attachments/assets/f76765ac-4e4e-4747-8204-06d270671c00" />


 4. UFW rules

<img width="627" height="799" alt="4" src="https://github.com/user-attachments/assets/57e2f19b-e0c8-4174-af85-49eae0df77d3" />

 5. Successful key-based login

<img width="581" height="590" alt="5" src="https://github.com/user-attachments/assets/8fbe3dcb-db7a-4d9c-b253-e9c9113bf0d1" />



**6. Firewall Documentation showing complete ruleset**

<img width="622" height="797" alt="6" src="https://github.com/user-attachments/assets/665be0e8-948d-4ca5-a125-7222c6d78624" />

The final UFW ruleset, shown via sudo ufw status verbose, implements a strict deny-by-default policy with the default action set to deny all incoming traffic while allowing outgoing connections. A single explicit rule permits SSH on the non-standard port 2222 exclusively from the workstation IP 192.168.56.10, while an additional deny rule blocks the same port from everywhere else, including IPv6, ensuring no accidental bypass is possible. This configuration follows the principle of least privilege and defense-in-depth, guaranteeing that even if an attacker discovers the custom port and obtains the private key, the connection will still be refused unless it originates from the designated workstation. The approach aligns with Ubuntu’s official firewall documentation [1] and widely accepted security best practices for host-based firewalls [2].


**References
[1] Canonical Ltd., “UFW – Uncomplicated Firewall,” Ubuntu Server Guide, 2025. https://ubuntu.com/server/docs/security-firewall
[2] Open Web Application Security Project (OWASP), “Secure Headers Project,” 2024 
https://owasp.org/www-project-secure-headers/**

