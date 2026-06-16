# Network Forensics and Snort Detection Engineering

## Objective
Investigated keylogger exfiltration in packet traffic and created Snort rules for ICMP and Nmap SYN-scan detection.

### Skills Learned
- Filtered traffic by protocol, host, port, flags, and credential-related strings.
- Traced keylogger exfiltration from the victim to attacker infrastructure.
- Recovered the username, password, URL, and two transferred HTML files.
- Created Snort rules for ICMP echo behavior and Nmap-style SYN packets with no payload.

### Tools Used
- Wireshark
- Snort
- PCAP analysis
- FTP/HTTP analysis
- Nmap traffic patterns

## Steps

*Ref 1: Wireshark Follow TCP Stream exposes the FTP password `Nipun@123` and confirms upload of the keylogger HTML artifact.*

<img src="assets/step-01.png" width="624" height="391" alt="Wireshark TCP stream showing FTP login success and upload of Keys_2018-11-28_16-04-42.html">

*Ref 2: Wireshark FTP-DATA object export identifies the two transferred HTML files and their source host.*

<img src="assets/step-02.png" width="624" height="391" alt="Wireshark FTP-DATA object list showing Keys and Web HTML files from 192.168.76.131">

*Ref 3: Recovered keylogger artifact shows the captured Windows Explorer activity for the Pictures directory.*

<img src="assets/step-03.png" width="624" height="391" alt="Recovered Keys HTML file showing explorer.exe activity in the Pictures directory">

*Ref 4: Recovered browser artifact records the user `nipun` opening `http://gmail.com/` in Microsoft Edge.*

<img src="assets/step-04.png" width="624" height="391" alt="Recovered Web HTML file showing Microsoft Edge activity for http://gmail.com/">

*Ref 5: Custom Snort local rules define ICMP echo request, ICMP echo reply, and TCP SYN stealth scan detections.*

<img src="assets/step-05.png" width="624" height="317" alt="Snort local.rules file containing ICMP echo and TCP SYN stealth scan alert signatures">

*Ref 6: Snort alert output confirms the TCP SYN stealth scan rule triggers on Nmap `-sS` traffic.*

<img src="assets/step-06.png" width="624" height="317" alt="Snort terminal output showing repeated TCP SYN stealth scan alerts">

*Ref 7: Snort alert output verifies the ICMP request and reply rules during ping traffic between the monitored hosts.*

<img src="assets/step-07.png" width="624" height="317" alt="Snort terminal output showing ICMP echo request and reply alerts">

*Ref 8: Nmap SYN scan against `192.168.1.11` discovers open FTP, SSH, and HTTP services used to validate the Snort scan rule.*

<img src="assets/step-08.png" width="624" height="391" alt="Nmap SYN scan results for 192.168.1.11 showing open ports 21, 22, and 80">

*Ref 9: Ping test against `192.168.1.11` generates ICMP traffic used to validate echo request and echo reply alerts.*

<img src="assets/step-09.png" width="624" height="391" alt="Ping results for 192.168.1.11 showing successful ICMP replies with no packet loss">
