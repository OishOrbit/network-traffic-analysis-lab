# Network Traffic Analysis Lab

A virtual lab for capturing and analyzing network traffic, built with VMware, Kali Linux, and Metasploitable 2.

## Topology
- Kali Linux (analyst): 192.168.100.128
- Metasploitable 2 (target): 192.168.100.129
- Isolated host-only network: VMnet2 (192.168.100.0/24)

## Progress
- [x] Isolated lab network built
- [x] Baseline capture (ping, HTTP, FTP, Telnet)
- [x] Cleartext FTP credentials recovered with Follow TCP Stream
- [x] Suricata analysis (default rules + custom SYN scan rule)
- [x] Zeek analysis (conn.log comparison: scan vs baseline)
- [x] Scenario 1: nmap SYN and version scan with custom detection rule
- [ ] More scenarios (FTP login, SSH brute force, web attack)
