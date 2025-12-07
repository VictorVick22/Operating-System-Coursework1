Phase 2: Security Planning and Testing Methodology (Week 2)

1. Performance Testing Plan
I will monitor the server remotely from the workstation (192.168.56.10) using SSH. Tools used: htop, iotop, nload, vmstat, and sar (from sysstat). Baseline will be recorded with an idle system, then repeated under load using stress-ng --cpu 4 --io 2 --vm 2 --timeout 300s. All results will be saved with timestamps and screenshots for comparison before/after hardening.
2. Security Configuration Checklist

SSH Hardening: Disable root login (PermitRootLogin no), password authentication (PasswordAuthentication no), use key-only, change port to 2222, limit to user vick.
Firewall (UFW): Enable UFW, allow only SSH (port 2222) from 192.168.56.10, deny everything else.
Automatic Updates: Install unattended-upgrades, configure auto security updates.
User Privileges: Only one admin user (vick) in sudo group, no unnecessary users.
Mandatory Access Control: Install and enable AppArmor (aa-enforce /etc/apparmor.d/*).
Network Security: Disable IPv6, ensure no open ports except 2222.

3. Threat Model (Top 3 Threats)

Brute-force SSH attack → Mitigated by key-only auth + Fail2Ban + non-standard port.
Unpatched vulnerabilities → Mitigated by unattended-upgrades and weekly manual checks.
Local privilege escalation → Mitigated by minimal users, AppArmor profiles, and regular apt update && apt upgrade.


[1] Ubuntu Security Team, “SSH/OpenSSH/Configuring,” Ubuntu Documentation, 2024. [Online]. Available: https://help.ubuntu.com/community/SSH/OpenSSH/Configuring

[2] Canonical Ltd., “Automatic Updates,” Ubuntu Server Guide, 2024. [Online]. Available: https://ubuntu.com/server/docs/automatic-updates

[3] AppArmor Documentation Team, “AppArmor Administration,” Ubuntu, 2024. [Online]. Available: https://wiki.ubuntu.com/AppArmor
