1.The diagram shows a real computer (the host) running VirtualBox software to create two virtual computers inside it. One virtual computer is a workstation using Ubuntu, and the other is an SSH server also using Ubuntu. The host connects to both virtual computers through VirtualBox. The two virtual computers talk to each other over a private network with addresses like 192.168.56.101 and 192.168.56.102. The workstation can log into the server using SSH on port 22.



<img width="451" height="484" alt="Screenshot 2025-12-01 131803" src="https://github.com/user-attachments/assets/eca8992b-41bd-42b4-bacc-53f1c721dfd6" />


2)Distribution Selection Justification:

For the server distribution, I selected Ubuntu 24.04.3 LTS (Long Term Support). This choice was made after comparing it with several alternatives, focusing on factors like stability, ease of management, community support, package availability, and suitability for a server environment with SSH access.
Ubuntu 24.04.3 LTS vs. Alternatives:
Debian 12 (Bookworm): Debian is known for extreme stability, as it's the base for Ubuntu. However, its release cycle is slower, meaning packages are older (e.g., Python 3.11 in Debian vs. 3.12 in Ubuntu 24.04). Ubuntu provides a good balance with fresher software while maintaining LTS stability (5 years of support until 2029). Debian might be better for ultra-conservative environments, but Ubuntu's larger community and easier package management (via apt) make it more practical for deployment and troubleshooting.
Fedora Server 40: Fedora offers cutting-edge features and is sponsored by Red Hat, making it great for testing new technologies. However, its short support cycle (about 13 months) contrasts with Ubuntu's LTS, which is preferable for a stable server setup to avoid frequent upgrades. Fedora uses DNF for packages, which is similar to apt but less ubiquitous in tutorials/documentation compared to Ubuntu.

Justification Summary: Ubuntu 24.04.3 LTS was chosen for its optimal blend of stability, up-to-date packages, extensive documentation, and large community support. It's particularly well-suited for an SSH server due to straightforward configuration, regular security updates, and compatibility with VirtualBox. Alternatives like Debian or CentOS are more rigid for production, while Fedora is too volatile for long-term use.






3)Workstation Configuration Decision

For the workstation, I chose Ubuntu 24.04.3 LTS running in VirtualBox. This decision aligns with the server distribution for consistency, simplifying management and reducing compatibility issues (e.g., shared tooling and commands).

Justification of Workstation Option:
Options Considered:
Native Installation on Hardware: This would provide maximum performance but requires dedicated hardware, partitioning, and potential dual-boot setup. It's overkill for testing/deployment planning and risks data loss during installation.
Virtual Machine (VirtualBox with Ubuntu): Selected due to flexibility—easy to snapshot, rollback, and isolate from the host OS. VirtualBox is free, cross-platform, and supports seamless integration (e.g., shared folders, clipboard). Ubuntu as the guest OS ensures parity with the server, making it ideal for simulating real-world scenarios like SSH connections.

Ubuntu in VirtualBox provides a cost-effective, isolated environment that's easy to configure and mirrors the server setup. It supports resource allocation (e.g., 4GB RAM, 2 CPUs) tailored to needs, with LTS ensuring security patches without disruptions.





4. Network configuration documentation covering VirtualBox settings and IP addressing  

Both virtual machines are running Ubuntu 24.04 LTS and are connected to the internet through VirtualBox NAT (Adapter 1) while communicating with each other and the host via a Host-Only network (Adapter 2 – vboxnet0). The workstation (Ubuntu Desktop) uses static IP 192.168.56.10/24 and the server (Ubuntu Server CLI) uses 192.168.56.101/24 on interface enp0s8. Netplan files (/etc/netplan/01-netcfg.yaml) were configured with DHCP on enp0s3 (NAT) for internet access and static addressing on enp0s8. Permissions were secured using chmod 600 /etc/netplan/*. Both “Cable connected” checkboxes were verified as enabled. Full bidirectional connectivity and internet access confirmed with successful pings to 8.8.8.8 and between 192.168.56.10 ↔ 192.168.56.101.


<img width="647" height="650" alt="Screenshot 2025-12-04 153932" src="https://github.com/user-attachments/assets/980ad951-8f1e-4c09-ab53-27f5f07f59ec" />
<img width="642" height="464" alt="Screenshot 2025-12-04 152600" src="https://github.com/user-attachments/assets/3357a952-7c26-4b0d-934c-e02d96512ee1" />
<img width="638" height="800" alt="Screenshot 2025-12-04 151310" src="https://github.com/user-attachments/assets/1cf168e5-3902-4fe5-aed3-e26728addf27" />
<img width="637" height="800" alt="Screenshot 2025-12-04 151221" src="https://github.com/user-attachments/assets/fc6fb5a5-d887-4eeb-93ec-6f46ff126d3c" />
<img width="637" height="800" alt="Screenshot 2025-11-09 144346" src="https://github.com/user-attachments/assets/cfa44f31-de16-4ea0-b81e-c25c957fe454" />





5.


<img width="638" height="800" alt="Screenshot 2025-12-04 154722" src="https://github.com/user-attachments/assets/c0bfe3b2-ed64-49ad-9935-46be557618bc" />
<img width="642" height="800" alt="Screenshot 2025-12-04 154622" src="https://github.com/user-attachments/assets/a734081c-d499-4693-987f-e192e7a6d510" />
<img width="635" height="800" alt="Screenshot 2025-12-04 154600" src="https://github.com/user-attachments/assets/fe8d5a31-c42e-43fc-a830-64453274b4b6" />



<img width="640" height="797" alt="Screenshot 2025-12-04 154905" src="https://github.com/user-attachments/assets/c9350b05-e483-4767-9342-03b46ae49d67" />

