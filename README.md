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
- [ ] Suricata and Zeek analysis
- [ ] Attack scenarios and custom detection rules
