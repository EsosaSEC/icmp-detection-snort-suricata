# icmp-detection-snort-suricata

# Detecting ICMP Traffic with Snort and Suricata – A Beginner's Guide

## Overview
This project demonstrates the setup, configuration, and use of Snort and Suricata, two open-source Network Intrusion Detection Systems (NIDS), to detect ICMP (ping) traffic in a lab environment. By creating custom detection rules, this project showcases real-time monitoring and alert generation, providing hands-on experience with foundational cybersecurity tools and techniques.

## Objectives
- Install and configure Snort and Suricata on an Ubuntu Linux environment.
- Write and implement custom detection rules for ICMP traffic.
- Simulate network traffic using ping to trigger alerts.
- Analyze generated alerts and logs to verify detection functionality.

## Skills Demonstrated
- Installation and configuration of Snort and Suricata.
- Writing custom NIDS rules for traffic detection.
- Real-time network traffic monitoring and alert analysis.
- Log analysis and system troubleshooting in a Linux environment.

## Tools Used
- **Snort**: Open-source NIDS for packet inspection and intrusion detection.
- **Suricata**: High-performance NIDS for real-time traffic monitoring.
- **Ubuntu Linux**: Virtual machine environment for testing.
- **ping**: Utility to generate ICMP traffic for testing detection rules.

## Project Steps

### Snort Setup
- Installed Snort using apt package manager on Ubuntu.
- Configured snort.conf to define HOME_NET for the local network.
- Created a custom rule to detect ICMP packets:
  ```plaintext
  alert icmp any any -> any any (msg:"ICMP detected"; sid:1000001; rev:1;)
  ```
- Ran Snort in NIDS mode and tested with `ping 8.8.8.8`.
- Verified alerts in real-time and analyzed logs.

### Suricata Setup
- Installed Suricata from the OISF repository.
- Configured suricata.yaml to set HOME_NET.
- Added a custom ICMP detection rule:
  ```plaintext
  alert icmp any any -> any any (msg:"ICMP Packet Detected"; sid:1000001; rev:1;)
  ```
- Enabled Suricata as a system service.
- Generated ICMP traffic with `ping 8.8.8.8` and verified alerts in `/var/log/suricata/fast.log`.

## Key Findings
- Successfully detected ICMP packets using custom rules in both Snort and Suricata.
- Real-time alerts were triggered during simulated ping traffic.
- Demonstrated foundational NIDS functionality, scalable to more complex detection scenarios like TCP port scans or malware traffic.

## Installation and Setup

To replicate this project:

### Install Ubuntu
Set up an Ubuntu VM (e.g., using VirtualBox or VMware).

### Install Snort
```bash
sudo apt update
sudo apt install snort
```

### Install Suricata
```bash
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt update
sudo apt install suricata
```

- Configure `snort.conf` or `suricata.yaml` to define HOME_NET.
- Add the custom ICMP rules provided above to the respective configuration files.
- Run Snort or Suricata in NIDS mode and generate ICMP traffic with `ping`.

## Usage

### Start Snort
```bash
sudo snort -c /etc/snort/snort.conf -i <interface> -A console
```

### Start Suricata
```bash
sudo suricata -c /etc/suricata/suricata.yaml -i <interface>
```

### Generate ICMP Traffic
```bash
ping 8.8.8.8
```

### Check Logs
- Snort: `/var/log/snort/alert`
- Suricata: `/var/log/suricata/fast.log`

## Troubleshooting
- No Alerts:
  - Verify the network interface (ifconfig or ip link).
  - Ensure the HOME_NET range matches your network.
  - Check rule syntax in local.rules.

- Configuration Errors:
   - Run test commands (snort -T or suricata -T) to identify issues.

- Permissions:
    - Use sudo for all commands, as both tools require root privileges.


## Future Enhancements
- Expand rules to detect advanced threats (e.g., TCP port scans, malware C2 traffic).
- Integrate with SIEM tools for centralized log analysis.
- Automate rule updates using community rule sets (e.g., Snort VRT or Emerging Threats).

## Conclusion
This project provides a hands-on introduction to network intrusion detection using Snort and Suricata. By detecting ICMP traffic with custom rules, it builds a foundation for more advanced NIDS scenarios, making it a valuable learning experience for aspiring SOC analysts and blue team professionals.




