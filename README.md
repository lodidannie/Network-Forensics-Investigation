# 🕵️‍♂️ Network Forensics Investigation — ANZ Cybersecurity Management Simulation (Forage)

![Status](https://img.shields.io/badge/status-completed-success)
![Tool](https://img.shields.io/badge/tool-Wireshark-blue)
![Tool](https://img.shields.io/badge/tool-NetworkMiner-green)
![Skill](https://img.shields.io/badge/skill-Network_Forensics-orange)
![Skill](https://img.shields.io/badge/skill-Incident_Response-red)



## Project Overview

This repository documents my cybersecurity investigation completed as part of the **ANZ Cyber Security Management Virtual Experience** on **[Forage](https://www.theforage.com/)**.

The task involved **analyzing a packet capture (PCAP)** file to investigate suspicious network activity from a user within the ANZ network. The objective was to identify the **websites visited**, **files accessed**, and **images viewed or downloaded** — ultimately producing a professional **forensic investigation report**.



## Objectives

- Analyze a PCAP file containing user network traffic  
- Detect suspicious connections and web activity  
- Reconstruct and extract transferred files and images  
- Document findings in a structured investigation report  
- Demonstrate use of digital forensics and network analysis tools  



## Tools & Technologies Used

| Tool | Purpose |
|------|----------|
| **Wireshark** | Packet analysis, filtering, stream reconstruction |
| **NetworkMiner** | Artifact extraction (files, images, credentials) |
| **tshark** | Command-line packet inspection |
| **File carving tools** | Recovering embedded or transferred content |
| **HxD Editor** | Reading ASCII characters and carving out document headers and footers |
| **Markdown / PDF report** | Documentation and presentation of findings |



## My Investigation Process

### 1. Load & Inspect
- Opened the provided `network_traffic.pcap` file in **Wireshark**  
- Inspected protocol hierarchy to identify HTTP, DNS, and TCP flows  

### 2. Filter Suspicious Traffic
- Applied filters such as:
  ```bash
  http || tcp.port == 80
