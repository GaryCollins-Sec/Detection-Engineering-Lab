<h1>Detection Engineering & Network Analysis Lab</h1>

<h2>Objective</h2>
<p>
Built a threat detection and network analysis pipeline using Wazuh (SIEM/XDR) and Suricata (IDS) in a virtualized lab.
</p>
<ul>
  <li>Deployed Suricata on Ubuntu to monitor traffic from a Kali attack node</li>
  <li>Conducted deep-packet analysis with Wireshark to validate alerts</li>
  <li>Authored custom Wazuh XML rules to prioritize critical security events like TCP port scans</li>
  <li>Demonstrated end-to-end detection: raw packet capture → alerting → SIEM dashboard</li>
</ul>

<hr>

<h2>Skills Developed</h2>
<ul>
  <li>Created custom Wazuh rules and decoders</li>
  <li>Parsed Suricata EVE JSON into structured SIEM data</li>
  <li>Tuned alerts to reduce false positives</li>
  <li>Deployed and configured Suricata sensors</li>
  <li>Wrote IDS signatures using TCP flags and content matching</li>
  <li>Troubleshot packets with Wireshark and tcpdump</li>
  <li>Simulated network attacks (SYN scans, reconnaissance) using Kali Linux</li>
  <li>Orchestrated multi-node virtual networks in VirtualBox</li>
  <li>Managed logs and alerts using CLI tools (grep, jq, tail)</li>
  <li>Maintained services using systemd</li>
</ul>

<hr>

<h2>Tools</h2>
<ul>
  <li>Wazuh (SIEM/XDR)</li>
  <li>Suricata (IDS/IPS)</li>
  <li>Wazuh Agent</li>
  <li>Ubuntu Desktop (Sensor)</li>
  <li>Kali Linux (Attacker)</li>
  <li>Oracle VM VirtualBox</li>
  <li>Wireshark</li>
  <li>Nmap</li>
  <li>Ettool</li>
  <li>Systemd (systemctl)</li>
  <li>Nano</li>
  <li>jq</li>
  <li>Tail/Grep</li>
</ul>

<hr>

<h2>Implementation Steps</h2>

<h3>Ref 1 – Simulated Attack Detection</h3>
<p>
Simulated a stealth TCP SYN scan from Kali against Ubuntu. Suricata captured the traffic and generated JSON alerts, which Wazuh ingested. Custom XML rules promoted critical events to high-priority alerts.
</p>
<img width="600" height="222" src="https://github.com/user-attachments/assets/9dfc95cb-2947-4294-8305-142fedbccada" />

<h3>Ref 2 – Packet Validation</h3>
<p>
Used Wireshark to confirm SYN scans reached the Suricata sensor. Validated TCP handshakes and packet headers, ensuring accurate correlation between raw traffic and Wazuh alerts.
</p>
<img width="747" height="589" src="https://github.com/user-attachments/assets/06dbe53b-7932-40fc-bb5b-e637d88d90c4" />

<h3>Ref 3 – IDS Deployment</h3>
<p>
Configured Suricata on Ubuntu to monitor adversarial reconnaissance. Captured stealth TCP SYN scans and exported alerts in EVE JSON format for SIEM ingestion.
</p>
<img width="657" height="483" src="https://github.com/user-attachments/assets/13847c47-9f6b-4524-b870-de04474c94c1" />

<h3>Ref 4 – SIEM Integration</h3>
<p>
Deployed Wazuh Agent on Ubuntu to ingest Suricata logs into Wazuh Manager. Validated JSON fields and matched them against custom XML rules. Elevated Nmap stealth scans to high-priority alerts (Level 12) on the dashboard.
</p>
<img width="1556" height="597" src="https://github.com/user-attachments/assets/6f272742-719e-40f7-bd2a-3668fc15f1ac" />

<h3>Ref 5 – Centralized Dashboard</h3>
<p>
Wazuh aggregated IDS and host telemetry into a unified event timeline. Alerts from Suricata (Rule ID 86601) and host activity (sudo, PAM logins) were correlated, providing a complete view of network and system security.
</p>
<img width="1108" height="691" src="https://github.com/user-attachments/assets/a3ca3fcb-e384-424b-b4e1-4378502c4f4f" />
