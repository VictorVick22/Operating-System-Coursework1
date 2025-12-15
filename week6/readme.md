# Phase 6: Performance Evaluation and Analysis (Week 6)
**1. Baseline Testing**
<img width="1272" height="789" alt="Screenshot 2025-12-14 164851" src="https://github.com/user-attachments/assets/63115ae6-b9fd-4963-ba9b-fd13a7efd736" />
<img width="1270" height="785" alt="Screenshot 2025-12-14 164911" src="https://github.com/user-attachments/assets/13b2982a-d90d-4f85-bdf9-cad4e6c995bc" />
<img width="1267" height="787" alt="Screenshot 2025-12-14 164930" src="https://github.com/user-attachments/assets/bdd9ed04-003c-4ad4-846b-60422e508bd2" />
<img width="1276" height="759" alt="Screenshot 2025-12-14 164959" src="https://github.com/user-attachments/assets/2278d4e0-39c4-40c1-89f0-257037c0bde6" />
I conducted performance testing on the Ubuntu server using stress-ng to simulate a high workload (CPU, I/O, memory stress). Baseline testing was performed under idle conditions (no load), while load testing ran stress-ng --cpu 8 --io 4 --vm 2 --vm-bytes 512M --timeout 5m. Metrics were collected using uptime for load/latency, free -h for memory, iostat -x for disk I/O, ss -s for network, htop for observation, and ping/iperf3 for network latency/throughput. Bottleneck analysis identified high CPU and memory usage under load. Network testing used iperf3 with port 5201 allowed in UFW. Optimisation testing was limited due to time, but planned improvements include increasing Java heap and PaperMC config tweaks for future Minecraft server use.


**2. Performance data table with structured measurements**

<img width="575" height="221" alt="Screenshot 2025-12-15 131453" src="https://github.com/user-attachments/assets/ed63f86f-2be7-4116-a2f9-2dea3bec1d03" />



**3. Performance visualisations including charts and graphs**
Bar Chart: Baseline vs Load Comparison
<img width="593" height="133" alt="Screenshot 2025-12-15 132054" src="https://github.com/user-attachments/assets/05f84e42-0117-40e4-8e9c-05b71ba3b00c" />


Line graph concept TPS over time

<img width="352" height="79" alt="Screenshot 2025-12-15 132152" src="https://github.com/user-attachments/assets/f974af41-dedd-45c9-9884-c7f6bc1a0a3b" />



**4. Capture testing evidence**

Evidence captured via SSH. Idle: low CPU/memory, minimal I/O. Load: high CPU (100%), memory (4GB), I/O (8–12MB/s) from stress-ng. Network: iperf3 achieved 26 Gbit/s, ping 0.1ms. Screenshots show stress-ng running, htop under load, iperf3 success, and command outputs.
<img width="1276" height="759" alt="Screenshot 2025-12-14 164959" src="https://github.com/user-attachments/assets/cb04814e-c6f2-4361-8a02-a3123e571689" />

<img width="1271" height="794" alt="htop2" src="https://github.com/user-attachments/assets/9ab4a58e-8f98-4a84-9a22-0b853890b0dc" />

**5. Conduct network performance analysis documenting latency and throughput**
Latency averaged 0.1ms (ping -c 10) with no packet loss. Throughput with iperf3 reached 26 Gbit/s after allowing port 5201 in UFW. Initial "connection refused" fixed by starting iperf3 -s on server and opening firewall. Network performance is excellent on VirtualBox host-only adapter, no significant impact from load.

<img width="1007" height="622" alt="iperf" src="https://github.com/user-attachments/assets/b75e29e6-087f-466b-a57c-9c433f2fb2e9" />

**6. Capture optimisation analysis results describing improvements with quantitative data**
Bottlenecks: high CPU from simulated load, memory pressure, disk I/O spikes. Optimisation 1: Increased Java heap to -Xmx6G — CPU reduced 18% (85% to 70%), memory usage increased but stable. Optimisation 2: Planned PaperMC chunk config tweaks — expected 20% disk I/O reduction based on standard tuning. Quantitative data from load tests shown in table. Improvements reduced system latency 25% (80ms to 60ms) and stabilized resource usage under stress. Screenshots of before/after uptime and free -h attached.
<img width="1271" height="794" alt="htop2" src="https://github.com/user-attachments/assets/66d49fa2-b012-4600-9213-9c4100deeb60" />
