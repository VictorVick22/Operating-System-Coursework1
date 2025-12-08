Phase 2: Security Planning and Testing Methodology (Week 2)

**1. Performance Testing Plan (Remote Monitoring)**
All monitoring and testing will be performed remotely from the workstation (192.168.56.10) over SSH.  
Tools used: htop, vmstat, iostat, nethogs, sar (sysstat), and dstat.  
Baseline measurements will be taken on an idle system, unhardened server.  
Each hardening step will be applied one-by-one, and the same tests repeated to measure performance impact.  
Load will be generated with stress-ng (CPU, memory, I/O) and iperf3 (network).  
Minecraft PaperMC server will be used as real-world mixed workload.  
All output will be timestamped and saved using script + tee for reproducible graphs.

**2. Security Configuration Checklist**
- SSH: Port 2222, key-only authentication, disable root login, disable password auth, Fail2Ban installed
- Firewall (UFW): Default deny, allow only port 2222 from 192.168.56.10
- Automatic security updates: unattended-upgrades configured for security only
- User management: Only user “vick” with sudo rights, no other accounts
- Mandatory Access Control: AppArmor in enforce mode for all profiles (sshd, java, etc.)
- Disable IPv6 in sysctl
- Regular apt autoremove & log monitoring with logwatch

**3. Threat Model (Top 3)**
1. Remote brute-force → mitigated by key-only + non-standard port + Fail2Ban  
2. Zero-day vulnerabilities → mitigated by automatic security updates  
3. Local privilege escalation → mitigated by minimal users + AppArmor confinement

All changes will be tested with nmap, ssh-audit, and lynis before/after.

References  
[1] Ubuntu Security Team, “SSH Hardening,” 2024. [Online].  
[2] Canonical, “Unattended Upgrades,” Ubuntu Server Guide, 2024. [Online].  
[3] AppArmor Documentation, 2024. [Online].
