# Report 02: Nmap SYN and Version Scan Detection

## Objective
Detect a port scan from Kali (192.168.100.128) against Metasploitable 2 (192.168.100.129), and test whether Suricata's default rules are enough.

## What I did
Captured on eth1 with tcpdump while running `sudo nmap -sS -sV 192.168.100.129`. The scan took 58.84 seconds and the capture holds 2858 packets (0 dropped). Suricata analysed the pcap offline with the `-k none` flag, because virtual NICs produce false "invalid checksum" alerts.

## Evidence
- Wireshark filter `tcp.flags.syn==1 && tcp.flags.ack==0`: many SYNs from one source to different ports
- Nmap found many open services (FTP, Samba, MySQL, VNC, IRC, Tomcat) and a root shell on port 1524

![Nmap SYN scan in Wireshark](../screenshots/nmap-syn-scan.png)

## Detection
**Default rules (Emerging Threats):** `ET SCAN Possible Nmap User-Agent Observed` (Priority 1) fired on the HTTP probes sent to ports 80 and 8180 by nmap's version detection. These alerts depend on the `-sV` option. A plain `-sS` scan would not send those probes.

![Default alerts](../screenshots/suricata-default-alerts.png)

**Custom rule (SID 1000001):**It fires when one source sends 20 or more SYN packets within 10 seconds.

| Capture | Packets | Custom rule alerts |
|---|---|---|
| nmap-scan.pcap | 2858 | 2 |
| baseline.pcap | 196 | 0 |

![Custom rule firing](../screenshots/suricata-custom-rule.png)

## Limitations
- The rule counts SYN packets, not distinct ports, so a flood of connections to a single port would also trigger it.
- A slow scan that stays below 20 SYNs per 10 seconds would evade it. I have not tested that yet.
- Tested against one scan type and one baseline capture, so the false positive rate is not measured.

## Recommendation
Alert on scanning behaviour (many SYNs, many ports) rather than relying only on tool signatures like the nmap user-agent, which are easy to change.

## MITRE ATT&CK
T1046 (Network Service Discovery)
