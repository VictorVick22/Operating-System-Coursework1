**Phase 3: Application Selection for Performance Testing (Week 3) 
Select applications representing different workload types for performance evaluation.**

**1. Select applications representing different workload types (e.g. CPU-intensive, RAM
intensive, I/O-intensive, Network-intensive, and Server applications such as game servers) 
for performance evaluation and create an Application Selection Matrix listing applications 
with justifications for choosing them.**

1) **Type**:  CPU - intensive
2) **Aplication/Tool**: stress-ng
3) **Command(via SSH)**:stress-ng --cpu 8 --  timeout 300s --metrics-brief  |
4) **Justification**:Pure CPU load, fully configurable, no disk/network interference, repetable results.
**Screenshots:**
<img width="638" height="800" alt="Screenshot 2025-12-08 160848" src="https://github.com/user-attachments/assets/7e3ec7c5-cd72-4ebb-a816-9f0c6b3485a9" />
<img width="637" height="800" alt="Screenshot 2025-12-08 160617" src="https://github.com/user-attachments/assets/fa13ce34-65e2-4e84-8708-66a689284fcd" />
<img width="637" height="800" alt="Screenshot 2025-12-08 160001" src="https://github.com/user-attachments/assets/1789b41e-a428-4fda-a9aa-b83746f1308a" />



2)**Type**: Memory-intensive
**Aplication/Tool**: stress-ng
**Command(via SSH)**: stress-ng --vm 4 --vm-bytes 85% --timeout 300s --metrics-brief
**Justification**: Allocates huge amounts of RAM and forces swapping – perfect to measure memory pressure

**Screenshots**:
<img width="636" height="800" alt="Screenshot 2025-12-08 163317" src="https://github.com/user-attachments/assets/13f375f0-eb87-4120-8386-40972ef3ebea" />
<img width="646" height="800" alt="Screenshot 2025-12-08 162812" src="https://github.com/user-attachments/assets/2c758e9b-f4a8-4936-8ed8-2f138dfff054" />



3)**Type**:Disk I/O-intensive
**Aplication/Tool**: fio
**Command(via SSH)**: fio --name=randrw --rw=randrw --bs=4k --size=2G --numjobs=8 --runtime=120 --time_based
**Justification**: Industry-standard flexible I/O benchmark, can saturate disk with random reads/writes

 <img width="710" height="800" alt="Screenshot 2025-12-08 163625" src="https://github.com/user-attachments/assets/f397866c-a92b-4a48-bcb5-81b9251b28a9" />
<img width="667" height="800" alt="Screenshot 2025-12-04 161927" src="https://github.com/user-attachments/assets/86790066-c8cd-44be-819d-c548aad5a33f" />
<img width="958" height="800" alt="Screenshot 2025-12-08 163823" src="https://github.com/user-attachments/assets/b6109851-5e2a-44c7-8056-a468f82af06e" />




 4)**Type**:Network-intensive
**Aplication/Tool**:iperf3 (server on 192.168.56.101)
**Command(via SSH)**:Server: iperf3 -s  →  Workstation: iperf3 -c 192.168.56.101 -t 60 -P 10
 **Justification**: Generates gigabits of traffic inside the VMs, perfect to measure network stack overhead
 <img width="1280" height="800" alt="Screenshot 2025-12-08 165032" src="https://github.com/user-attachments/assets/63b43e25-c858-4f0c-8faa-dbc54aa55326" />
<img width="1280" height="800" alt="Screenshot 2025-12-08 164717" src="https://github.com/user-attachments/assets/9d42cea5-17ae-4f50-a01a-65be698d4b08" />


 5)**Type**:Real-world server app
**Aplication/Tool**:PaperMC 1.21.4 (Minecraft)
**Command(via SSH)**:java -Xms2G -Xmx4G -jar paper.jar nogui
 **Justification**: Popular game server with mixed CPU + RAM + disk + network load – mimics production traffic

<img width="647" height="800" alt="Screenshot 2025-12-08 170735" src="https://github.com/user-attachments/assets/dac0f754-ed24-4820-9619-2682191f0401" />
<img width="718" height="800" alt="Screenshot 2025-12-08 170653" src="https://github.com/user-attachments/assets/d9844f34-37c3-43a3-8845-5bf7b5ad55f4" />
<img width="710" height="800" alt="Screenshot 2025-12-08 170552" src="https://github.com/user-attachments/assets/d3d578fd-0cf4-4971-a3c9-f7c9edad88c6" />
<img width="641" height="800" alt="Screenshot 2025-12-08 165517" src="https://github.com/user-attachments/assets/4cafc878-1e10-4891-be1e-05dac16ee467" />

 



 2)**Installation Documentation with exact commands for SSH-based installation**:
 
ssh vick@192.168.56.101
sudo apt update && sudo apt upgrade -y
sudo apt install stress-ng fio iperf3 openjdk-21-jre-headless wget screen -y

# Minecraft server
mkdir ~/minecraft && cd ~/minecraft
wget https://api.papermc.io/v2/projects/paper/versions/1.21.4/builds/160/downloads/paper-1.21.4-160.jar -O paper.jar
echo "eula=true" > eula.txt
screen -dmS mc java -Xms2G -Xmx4G -jar paper.jar nogui   # start in background

**3)Expected Resource Profiles (before hardening)**:

Test: Stress-ng cpu | CPU: 100% | RAM <5%  | Disk i/o: negligible | Network: none
Test: stress-ng VM  | CPU: 30-70% | RAM: 85-95% | Disk I/O: low | Network: none
Test: fio random I/O | CPU: 20-50% | RAM: <10% | Disk I/O: 100% | Network: none
Test: iperf3 | CPU: 50-90%| RAM: <5% | Disk I/O: none | Network: 5-9gibt/s
Test: PaperMC | CPU: 70-150% | RAM: 2.5-3.5GB | Disk I/O: Moderate | Network: 50-300mbit/s


**4. Monitoring Strategy**

**Live view:** htop <img width="640" height="800" alt="htop" src="https://github.com/user-attachments/assets/5e3d023d-173e-491f-9f6d-de7c022f657f" />


**Periodic stats**
*vmstat 1*, *iostat -xz 1*, *sar -u -r -d -n DEV 1*


<img width="638" height="800" alt="iostat xz" src="https://github.com/user-attachments/assets/413a5074-dcdb-45bd-93da-5cab0c4779af" />
<img width="638" height="800" alt="sar" src="https://github.com/user-attachments/assets/ab2a9d10-84f5-4a43-944f-3d03ebc17bc3" />
<img width="635" height="800" alt="iostat xz1" src="https://github.com/user-attachments/assets/93cded56-8597-4a57-bc89-a708d0339ce5" />
<img width="638" height="800" alt="vmstat1" src="https://github.com/user-attachments/assets/51659d0f-7e58-4670-b671-9a200980bd13" />

**Minecraft**:

screen -r mc 


<img width="638" height="800" alt="Screenshot 2025-12-08 173336" src="https://github.com/user-attachments/assets/3358f6e2-5ba1-42fb-b977-d9ec3010d552" />



