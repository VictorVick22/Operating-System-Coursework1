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

VM: <img width="637" height="462" alt="Screenshot 2025-12-01 184926" src="https://github.com/user-attachments/assets/ff125d32-96d5-4dcf-a6e5-fd5bd10e3813" />


<img width="636" height="457" alt="Screenshot 2025-12-01 185153" src="https://github.com/user-attachments/assets/9a0595d8-a939-470e-bc60-7416a16d0100" />

