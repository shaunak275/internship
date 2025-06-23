# internship
Project Description: Network Port Scanning Lab
Overview
This project involves a hands-on lab to discover open ports on devices within a local network (192.168.0.0/24) using Nmap, with optional packet analysis using Wireshark. The goal is to understand network exposure by identifying active hosts, their open ports, and associated services, while assessing potential security risks. The lab simulates a real-world network scanning scenario, providing insights into network security and best practices for securing exposed services.
Objectives

Learn to use Nmap for network discovery and port scanning.
Identify open ports and services on local network devices.
Analyze potential security risks associated with exposed services.
Optionally use Wireshark to capture and analyze network packets.
Document findings in a comprehensive report and share via GitHub.

Tools Used

Nmap: A free, open-source tool for network exploration and security auditing, used to perform a TCP SYN scan.
Wireshark: An optional packet analyzer for inspecting network traffic (simulated in this lab).
GitHub: Used to store and share the lab report and related files.

Methodology

Installed Nmap from the official website and verified its version.
Determined the local IP range (192.168.0.0/24) using ipconfig or equivalent.
Conducted a TCP SYN scan with the command nmap -sS 192.168.0.0/24 to identify active hosts and open ports.
Recorded IPs and ports (e.g., 192.168.0.1: 80, 443, 631; 192.168.0.101: 22, 445).
(Simulated) Captured packets with Wireshark to confirm open ports via TCP SYN/ACK exchanges.
Researched services (e.g., HTTP, SSH, SMB) and their common uses.
Identified security risks, such as exposed router admin interfaces or vulnerable SMB services.
Saved scan results as text and HTML files for documentation.

Key Findings

Discovered two active hosts: a router (192.168.0.1) with ports 80 (HTTP), 443 (HTTPS), and 631 (IPP), and a computer (192.168.0.101) with ports 22 (SSH) and 445 (SMB).
Identified risks: Exposed router services could allow unauthorized access; SSH and SMB are vulnerable to brute-force or malware attacks if not secured.
Recommended mitigations: Strong passwords, disabling unnecessary services (e.g., IPP, SMB), and restricting access via firewalls or VPNs.

Deliverables

A detailed Markdown report (Network_Scan_Report.md) documenting the methodology, results, and recommendations.
Placeholder images for terminal outputs, Wireshark captures, and network diagrams (to be replaced with actual images if needed).
A GitHub repository (e.g., Network-Scanning-Lab) hosting the report and related files.

Skills Demonstrated

Network scanning and enumeration using Nmap.
Basic packet analysis with Wireshark.
Security risk assessment and mitigation strategies.
Technical documentation and version control with GitHub.

Repository Contents

Network_Scan_Report.md: The main lab report with methodology, results, and analysis.
Placeholder image references for visual documentation (e.g., Nmap output, network diagram).
(Optional) Future additions: Actual images, Nmap scan output files, or automation scripts.

Conclusion
This project provides a practical introduction to network security auditing, demonstrating how to use Nmap and Wireshark to assess network exposure. By identifying and analyzing open ports and services, it underscores the importance of securing network devices to prevent unauthorized access and potential attacks. The GitHub repository serves as a centralized platform to share findings and facilitate collaboration or further development.
