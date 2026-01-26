# Detection Engineering & Network Analysis Lab

## Objective
The objective of this project was to engineer an integrated Threat Detection and Network Analysis pipeline using a Wazuh and Suricata stack within a virtualized sandbox. By deploying a Suricata sensor on Ubuntu, I established real-time signature-based inspection to monitor traffic from a Kali Linux attack node. I performed deep-dive analysis with Wireshark to resolve packet-level anomalies, such as checksum offloading, and authored custom Wazuh XML rules to decode and prioritize critical security events like TCP port scanning. This project demonstrates a full-lifecycle approach to detection engineering, from raw packet capture to centralized SIEM dashboarding.

### Skills Learned
- Wazuh Rule Development: Authored custom XML rules to promote alert levels and create human-readable event descriptions.
- Log Decoding: Utilized Wazuh decoders to map Suricata EVE JSON fields into structured SIEM data.
- Threat Tuning: Configured alerting thresholds and rate-limiting to minimize false positives and manage alert volume.
- Suricata Signature Writing: Created custom IDS rules using specific protocol flags (TCP SYN) and content matching.
- IDS Deployment: Configured Suricata in a Linux environment, including interface binding and rule-path management.
- Traffic Mirroring: Configured virtualized network interfaces in Promiscuous Mode to enable full-stack packet inspection.
- Protocol Analysis: Used Wireshark to inspect packet headers and troubleshoot handshake anomalies.
- Vulnerability Scanning: Conducted reconnaissance using Nmap (SYN scans) to validate detection logic and sensor responsiveness.
- Traffic Generation: Simulated attack traffic from a Kali Linux node to test the resilience of the security pipeline.
- Linux Hardening & Admin: Managed security services via systemd and performed real-time log analysis using CLI tools like tail, grep, and jq.
- Virtual Infrastructure: Orchestrated a multi-node lab environment using Oracle VM
- VirtualBox with isolated bridged networking.


### Tools Used
- Wazuh (SIEM/XDR): Centralized log management, correlation, and intrusion detection.
- Suricata (IDS/IPS): Served as the network sensor, performing deep packet inspection and signature-based threat detection.
- Wazuh Agent: Installed on the Ubuntu endpoint to securely ship Suricata's eve.json logs to the Wazuh Manager.
- Ubuntu Desktop: The primary "Victim/Sensor" node where the defense stack was deployed.
- Kali Linux: The "Attacker" node used to generate malicious traffic and reconnaissance scans.
- Oracle VM VirtualBox: The Type-2 hypervisor used to host the virtual network and manage promiscuous mode traffic.
- Wireshark: Utilized for packet-level troubleshooting, verifying TCP handshakes, and analyzing checksum errors.
- Nmap: The primary tool used to simulate network reconnaissance and trigger SYN-scan alerts.
- Ethtool: A critical Linux utility used to disable hardware checksum offloading on the virtual network interface.
- Systemd (systemctl): Used to manage the background lifecycle of the Suricata and Wazuh services.
- Nano: The text editor used for modifying Suricata signatures and Wazuh XML rules.
- jq: Used to parse and prettify the complex JSON output within the eve.json file.
- Tail/Grep: Essential CLI tools used for real-time log monitoring and troubleshooting.
  


## Steps


Reference: SIEM 1




<img width="600" height="222" alt="Edit_nmap" src="https://github.com/user-attachments/assets/9dfc95cb-2947-4294-8305-142fedbccada" />

This project validated a complete detection pipeline by simulating a stealth TCP SYN scan from Kali Linux against an Ubuntu target. The attack was intercepted by Suricata, which generated a JSON alert that was then ingested and decoded by Wazuh. By authoring custom XML rules to match specific signatures and promote alert levels, I successfully transformed raw network traffic into high-priority security events on the Wazuh Dashboard.

Reference: SIEM 2


<img width="747" height="589" alt="Edit_wireshark" src="https://github.com/user-attachments/assets/06dbe53b-7932-40fc-bb5b-e637d88d90c4" />


I utilized Wireshark to conduct deep-packet analysis, validating the "ground truth" of Nmap stealth scans by capturing raw TCP SYN frames in real-time. By inspecting packet headers and handshake flags, I confirmed that the virtual network was correctly delivering traffic to the Suricata sensor. This allowed me to correlate raw wire-level data with the final Wazuh alerts, ensuring the entire detection lifecycle was accurate and functional from the initial packet to the SIEM dashboard.

Reference: SIEM 3


<img width="657" height="483" alt="Screenshot 2026-01-25 233546" src="https://github.com/user-attachments/assets/13847c47-9f6b-4524-b870-de04474c94c1" />

In this project, I deployed Suricata as a signature-based Network Intrusion Detection System (NIDS) on an Ubuntu "Victim" machine to monitor for adversarial reconnaissance. By configuring Suricata to inspect traffic in real-time, I successfully captured stealth TCP SYN scans initiated from a Kali Linux attack node. As shown in the tail -f log output, Suricata generates detailed telemetry and performance metrics, which it then exports into a structured EVE JSON format. This JSON data, specifically the NMAP TCP SCAN DETECTED signature, serves as the critical bridge between raw network packets and the Wazuh alerting engine, providing high-fidelity detection of "on-the-wire" threats before they can escalate.

Reference: SIEM 4

<img width="1556" height="597" alt="Screenshot 2026-01-25 233236" src="https://github.com/user-attachments/assets/6f272742-719e-40f7-bd2a-3668fc15f1ac" />

I utilized Wazuh as the primary SIEM and XDR platform to orchestrate log collection, decoding, and alert visualization for the entire security stack. By deploying the Wazuh Agent on the Ubuntu target, I established a secure pipeline to ingest Suricata’s EVE JSON logs into the Wazuh Manager for real-time analysis. I leveraged the Wazuh Ruleset Test tool to validate that incoming JSON fields—specifically the alert.signature—were correctly decoded and matched against my custom-authored XML rules. This implementation allowed me to elevate critical reconnaissance events, such as Nmap stealth scans, to high-priority alert levels (Level 12), ensuring immediate visibility on the centralized security dashboard.


Reference: SIEM 5
<img width="1108" height="691" alt="Screenshot 2026-01-25 233324" src="https://github.com/user-attachments/assets/a3ca3fcb-e384-424b-b4e1-4378502c4f4f" />

This image showcases the final stage of the detection pipeline, where Wazuh successfully ingests and categorizes security telemetry from the environment. The interface displays a centralized event log where network-based alerts from Suricata (Rule ID 86601) are correlated alongside host-based activity, such as successful sudo executions and PAM login sessions. By mapping the alert.signature field within the Wazuh manager, I was able to transform raw JSON logs into a structured timeline, providing a unified view of the system’s security posture. This integration confirms the project's ability to aggregate disparate data sources—from wire-level IDS alerts to system-level administrative actions—into a single, actionable dashboard for security monitoring.


