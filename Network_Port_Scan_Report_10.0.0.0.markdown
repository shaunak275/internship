# Network Port Scan Report (IP Range: 10.0.0.0/24)

## Objective
The objective of this lab was to learn how to discover open ports on devices within a local network to understand network exposure, using Nmap as the primary tool and Wireshark for optional packet analysis.

## Tools Used
- **Nmap**: Free, open-source network scanning tool (Version 7.94, downloaded from https://nmap.org).
- **Wireshark** (Optional): Network protocol analyzer (Version 4.2.0).
- **Operating System**: Kali Linux (for Nmap) and Windows 11 (for Wireshark).

## Methodology

### Step 1: Install Nmap
- Installed Nmap on Kali Linux using:
  ```bash
  sudo apt-get install nmap
  ```
- Verified with `nmap --version`, confirming Nmap version 7.94.

### Step 2: Find Local IP Range
- Ran `ip addr` to identify the network interface (e.g., eth0) with IP `10.0.0.100` and subnet mask `/24`, indicating the IP range `10.0.0.0/24`.

### Step 3: Perform TCP SYN Scan
- Executed a TCP SYN scan with:
  ```bash
  nmap -sS 10.0.0.0/24
  ```
- The `-sS` flag performs a stealth SYN scan, minimizing detection.
- Scan duration: ~2 minutes.

### Step 4: Note IP Addresses and Open Ports
- Nmap detected 4 active hosts. Findings:
  - **10.0.0.1 (Router)**:
    - Open ports: 80 (HTTP), 443 (HTTPS), 23 (Telnet).
  - **10.0.0.100 (Local Machine)**:
    - Open ports: 22 (SSH), 5900 (VNC).
  - **10.0.0.101 (NAS Workstation)**:
    - Open ports: 80 (FTP), 443 (HTTPS), 445 (SMB).
  - **10.0.0.102 (IP Camera)**:
    - Open ports: 554 (RTSP), 8080 (HTTP-Alt).

### Step 5: Analyze Packet Capture with Wireshark)
- Used Wireshark on Windows 11 to capture packets during a targeted scan (`nmap -sS 10.168.0.101`).
- Observed SYN packets from Nmap and SYN-ACK responses for ports 80 and 445.
- Filtered traffic with `ip.addr == 10.0.0.101 && tcp.port == 445` to analyze SMB traffic.
- No anomalies detected.

### Step 6: Research Common Services
- Researched services on open ports:
  - **80/443 (HTTP/HTTPS)**: Router web interface or NAS web server.
  - **23 (Telnet)**: Remote admin access, insecure.
  - **22 (FTP)**: Secure file transfer.
  - **5900 (VNC SSH)**: Remote desktop access.
  - **445 (HTTPS)**: File sharing.
  - **554 (SMB)**: File sharing on NAS.
  - **8080 (RTSP)**: Alternate HTTP port, likely camera web interface.
  - **554 (RTSP)**:
Streaming media, common for IP cameras.

### Step 7: Identify Potential Security Risks
- **Router (10.0.0.1)**:
  - Telnet (port 23): is highly vulnerable due to unencrypted traffic and weak authentication.
  - HTTP/HTTPS: (80/443): Admin interface may be at risk if default credentials are unchanged.
  - **Recommendation**: **Disable Telnet**, secure HTTP/HTTPS with strong passwords, disable remote access.
- **Local Machine (10.0.0.100)**:
  - SSH (22): Secure if properly configured; VNC (5900): may expose weak passwords.
  - **Recommendation**: Use SSH keys, enforce strong VNC authentication.
- **NAS Workstation (10.0.0.101)**:
  - SMB (445): Risks file exposure if permissions are lax; FTP/HTTPS (80/443): may host sensitive data.
  - **Recommendation**: Restrict SMB/FTP access, update NAS firmware.
- **IP Camera (10.0.0.102)**:
  - RTSP/HTTP-Alt (554/8080): Unpatched firmware could allow unauthorized access.
  - **Recommendation**: Update firmware, isolate on VLAN.

### Step 8: Save Scan Results
- Saved results using:
  ```bash
  nmap -sS 10.0.0.0/24 -oN scan_results.txt -oX scan_results.xml
  ```
- Generated HTML report:
  ```bash
  xsltproc scan_results.xml -o scan_results.html
  ```
- Stored in `/home/user/nmap_scans/`.

## Results Summary
- **Hosts Discovered**: 4
- **Total Open Ports**: 10
- **Key Findings**:
  - Router’s Telnet port poses a significant risk.
  - NAS and IP camera services may be vulnerable if unpatched.
  - Local machine’s VNC needs secure configuration.
- **Wireshark Analysis**: Validated Nmap’s scan, no disruptions noted.

## Recommendations
1. **Disable Telnet**: Replace with SSH on router.
2. **Secure NAS**: Limit SMB/FTP access, apply updates.
3. **Harden Camera**: Update firmware, use VLAN isolation.
4. **Strengthen VNC**: Enforce strong passwords or disable.
5. **Firewall Rules**: Allow only necessary ports.
6. **Regular Scans**: Monitor network with Nmap periodically.

## Conclusion
Using the `10.0.0.0/24` range, this lab demonstrated Nmap’s ability to identify open ports and exposed services. The discovery of Telnet and unsecured IoT services underscores the need for robust security practices. Wireshark provided packet-level insights, confirming scan behavior. Ongoing network monitoring and service hardening are critical for security.

## Attachments
- `scan_results.txt`: Nmap raw output.
- `scan_results.html`: HTML report.
- Wireshark capture (available on request).