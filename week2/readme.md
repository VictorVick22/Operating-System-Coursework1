Phase 2: Security Planning and Testing Methodology (Week 2)



During Week 2, a comprehensive security baseline and performance testing methodology were designed for the isolated VirtualBox lab consisting of two Ubuntu 24.04.3 LTS virtual machines connected through a host-only network (192.168.56.0/24). The performance testing plan relies exclusively on remote, agentless monitoring from the workstation VM (op – 192.168.56.20) by executing standard Linux utilities (vmstat, iostat, mpstat, sar, iftop, and optionally Glances) over SSH against the server VM (192.168.56.10). This approach enables repeatable baseline measurements, stress testing with stress-ng and iperf3, and multi-session load simulation while keeping the server footprint minimal.
A detailed security configuration checklist was established covering SSH hardening (root login disabled, password authentication disabled in favour of ed25519 key-only access, AllowUsers restriction), strict UFW firewall rules limited to the 192.168.56.0/24 subnet, AppArmor enforcement verification, automatic security updates via unattended-upgrades, single non-root user principle, removal of unnecessary packages, IPv6 disablement, and persistent journal configuration. Finally, a STRIDE-based threat model identified the three most relevant risks in the current lab environment: (1) unauthorized SSH access via credential compromise, mitigated by key-only authentication and network isolation; (2) brute-force attacks on the SSH service, rendered impossible by the host-only network topology; and (3) privilege escalation through unpatched vulnerabilities, countered by enabled unattended-upgrades and future live patching considerations.
All planned configurations are documented and ready for incremental implementation in subsequent phases, ensuring the lab remains both functional for testing and aligned with current Ubuntu 24.04 server hardening best practices [1]–[4].





References
[1] Ubuntu Server Team, “Ubuntu Server Guide 24.04 LTS,” Canonical Ltd., 2024. [Online]. Available: https://ubuntu.com/server/docs
[2] OpenSSH Project, “OpenSSH Security Best Practices,” 2024. [Online]. Available: https://www.openssh.com/security.html
[3] National Institute of Standards and Technology (NIST), “Guide to General Server Security,” NIST Special Publication 800-123, Jul. 2008. [Online]. Available: https://doi.org/10.6028/NIST.SP.800-123
[4] M. Abbott and M. Howard, “The STRIDE Threat Model,” Microsoft Corporation, 2006. [Online]. Available: https://learn.microsoft.com/en-us/previous-versions/commerce-server/ee823878(v=cs.20)
