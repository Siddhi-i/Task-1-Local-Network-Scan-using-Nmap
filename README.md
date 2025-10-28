# Local Network Scan Using Nmap

## Overview
This guide shows a basic workflow for performing a local network scan with Nmap to discover hosts and open ports on your local LAN. The purpose is to learn how network scanning works, record findings, and identify potential security issues.

Important: Only scan networks and devices you own or have explicit permission to scan. Unauthorized scanning can be illegal.

## Prerequisites
- A computer with administrative privileges.
- Nmap installed from the official site: https://nmap.org
- (Optional) Wireshark for packet capture and deeper analysis.
- Familiarity with running commands in a terminal or command prompt.

## Step-by-step Instructions

### 1. Find your local IP range
Find your machine’s local IP and subnet to determine the scan range.

Windows:
```powershell
ipconfig
```

Linux / macOS:
```bash
ip addr show
# or
ifconfig
```

Typical private ranges: 192.168.1.0/24, 10.0.0.0/24, 172.16.0.0/16.

### 2. Run a TCP SYN scan
Use a TCP SYN scan to discover hosts and open TCP ports:

```bash
nmap -sS 192.168.1.0/24
```

Replace 192.168.1.0/24 with your local subnet.

### 3. Save the scan results
Save output as text, XML, or all formats:

```bash
nmap -sS -oN scan-results.txt 192.168.1.0/24
nmap -sS -oA scan-results 192.168.1.0/24
```

The -oA option produces scan-results.nmap, scan-results.xml, and scan-results.gnmap.

### 4. Note down IP addresses and open ports
After the scan completes, review the saved file and record:
- Host IP
- Host state (up/down)
- Open ports and their services

Create a table in your notes or CSV file for clarity.

### 5. Optional: Capture and analyze packets with Wireshark
1. Start Wireshark and capture on your LAN interface.
2. Run the Nmap scan.
3. Stop capture and filter by IP or port (for example, tcp.port == 80).
4. Inspect SYN/SYN-ACK/RST patterns to confirm host responses.

### 6. Research common services on discovered ports
Common ports and services include:
- 22/tcp — SSH
- 80/tcp — HTTP
- 443/tcp — HTTPS
- 23/tcp — Telnet (insecure)
- 3389/tcp — RDP

For each open port, search for the service name and version to assess risk.

### 7. Identify potential security risks
When analyzing results, look for:
- Unnecessary or outdated services exposed on the network.
- Services with known vulnerabilities.
- Management interfaces that should be restricted.

Document the highest-risk findings and recommended actions (patching, disabling, or restricting services).

### 8. Save and document your findings
Keep your scan-results files and add a summary file listing the most important information:
- Host IP (redacted if publishing)
- Open ports and services
- Risk level and recommended fix

When publishing results publicly, redact local IPs and MAC addresses (use placeholders like 192.168.x.x or <local IP hidden>).

## Example Commands Summary
```bash
nmap -sS 192.168.1.0/24
nmap -sS -oN scan-results.txt 192.168.1.0/24
nmap -sS -oA scan-results 192.168.1.0/24
nmap -sS -sV 192.168.1.0/24
```

## Safety and Privacy
- Only scan networks you own or have permission to scan.
- Do not publish raw scan results that include real IP or MAC addresses.
- Follow laws, organizational policies, and responsible disclosure practices.

## References
- Nmap Documentation: https://nmap.org/book/
- Wireshark: https://www.wireshark.org/
- CVE Search: https://www.cvedetails.com/

