# Network Forensics Investigation: ANZ Cybersecurity Management Simulation (Forage)

![Status](https://img.shields.io/badge/status-completed-success)
![Tool](https://img.shields.io/badge/tool-Wireshark-blue)
![Tool](https://img.shields.io/badge/tool-NetworkMiner-green)
![Skill](https://img.shields.io/badge/skill-Network_Forensics-orange)
![Skill](https://img.shields.io/badge/skill-Incident_Response-red)



## Project Overview

This repository documents my cybersecurity investigation completed as part of the **ANZ Cyber Security Management Virtual Experience** on **[Forage](https://www.theforage.com/)**.

The task involved **analyzing a packet capture (PCAP)** file to investigate suspicious network activity from a user within the ANZ network. The objective was to identify the **websites visited**, **files accessed**, and **images viewed or downloaded** ultimately producing a professional **forensic investigation report**.



## Objectives

- Analyze a packet capture (PCAP) file containing user network traffic  
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

### 1. Load & Inspect the PCAP file
- Opened the provided `network_traffic.pcap` file in **Wireshark**  
- Inspected protocol hierarchy to identify HTTP, DNS, and TCP flows  

### 2. Filter Suspicious Traffic
- Applied filters such as:
  ```bash
  http || tcp.port == 80
  http.request.method == "GET"
  GET /images/photo1.jpg HTTP/1.1
  GET /downloads/malicious_doc.docx HTTP/1.1
  Right-click the packet → Follow → TCP Stream
  GET /images/suspicious.jpg HTTP/1.1
  Host: suspicious-domain.com
  User-Agent: Mozilla/5.0

HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 54782
<binary data...>


### 3. Reconstructed streams to identify files and images transferred

### 4. Used NetworkMiner to extract downloaded artifacts

### 5. Documented all findings, timestamps, and connections

### 6. Compiled a detailed forensic report summarizing user activity

### My Key Findings
### a) Extracted Images

To find the images the user accessed called anz-logo.jpg and bank-card.jpg I followed the following process for
both images:
   
  -First I filtered the packet capture for http traffic and looked through the remaining packets for the GET request
  that downloaded the image. I then right clicked the image and followed its TCP stream.
  -In the TCP stream I saw what looked like image data. In order to view the data in hex format, I changed the view to
  ‘raw’, and then searched the hex data for a jpeg’s file signature.
  -After finding the file signature “FFD8” the top, and the file footer “FFD9” at the bottom, I copied everything
  between those two points into the hex editor HxD and saved it as a jpg image. 


### b) Extracted Documents
-In order to view these PDF’s I viewed the TCP stream as usual, and found the file signature for a PDF, which was
the hex data “25 50 44 46”. I noticed in the ascii view that the PDF data went until the very end of the TCP stream,
so I copied all the hex date from the file signature onwards into HxD and saved it as a pdf file.

### c) Encoded Document
-After investigating the TCP stream for securepdf.pdf I discovered three things:
-The data there was not for a PDF.
-The bottom of the file contained the hidden message: Password is “secure”
-It contained the file signature for a zip file, meaning that the what the user downloaded was actually a zip file.
So I copied the hex of the zip file into HxD and saved it as a zip file. I opened this zip file, and found it contained a
pdf file called rawpdf.pdf. When opened, the pdf prompted for a password. The password ‘secure’ shown in the tcp
stream worked, and the PDF opened. It was the first two pages to a guide for internet banking.
**Downloaded File: malicious_doc.docx

### Extracted Image: contained encoded data indicating potential exfiltration

### User Behavior: visiting unsafe links and downloading unverified files

### 7. Skills Demonstrated

-Network forensics

-PCAP analysis

-Incident response documentation

-Threat detection and reporting

-Technical writing for cybersecurity

### 8. Outcome

This investigation simulated a real-world incident response task. Findings demonstrated ability to:

-Analyze and interpret complex network data

-Identify indicators of compromise

-Produce a clear, evidence-based security report
