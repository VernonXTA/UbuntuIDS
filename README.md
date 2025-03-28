# XMAS Scan Intrusion Detection System (IDS)

## Overview
This project is an Intrusion Detection System (IDS) designed to detect and respond to XMAS scans targeting a system and its running services. The IDS leverages **Snort**, a powerful open-source network intrusion detection and prevention system, to identify and log malicious scan activity.

## Features
- **XMAS Scan Detection**: Identifies stealthy XMAS scans commonly used for reconnaissance.
- **Real-time Logging**: Captures and logs suspicious activity for further analysis.
- **Automated Response**: Optionally blocks malicious IP addresses upon detection.
- **Snort Integration**: Utilizes Snort rules for high-accuracy intrusion detection.
- **Customizable Rules**: Users can modify detection rules based on security needs.

## How It Works
XMAS scans are a type of stealth scan where the FIN, PSH, and URG flags are set in TCP packets. These scans are used to probe open ports on a target system. The IDS:
1. Monitors network traffic using **Snort**.
2. Detects packets with FIN, PSH, and URG flags set.
3. Logs the detected scans for analysis.
4. (Optional) Blocks the attacker's IP address using firewall rules.

## Installation
1. Install Snort:
   ```bash
   sudo apt update && sudo apt install snort -y
   ```
2. Configure Snort rules:
   ```bash
   sudo nano /etc/snort/rules/local.rules
   ```
   Add the following rule:
   ```
   alert tcp any any -> any any (flags: FPU; msg:"XMAS Scan detected"; sid:1000001;)
   ```
3. Update Snort configuration:
   ```bash
   sudo nano /etc/snort/snort.conf
   ```
   Ensure the local rule path is included:
   ```
   include /etc/snort/rules/local.rules
   ```
4. Start Snort:
   ```bash
   sudo snort -A console -q -c /etc/snort/snort.conf -i eth0
   ```

## Usage
- Monitor logs:
  ```bash
  sudo tail -f /var/log/snort/alert
  ```
- Block an attacker manually:
  ```bash
  sudo iptables -A INPUT -s <attacker_ip> -j DROP
  ```

## Future Enhancements
- Automated blocking using fail2ban.
- Integration with SIEM solutions for centralized monitoring.
- Advanced anomaly detection with machine learning.

## License
This project is open-source under the MIT License.

## Author
**Dante Worthington** - Cybersecurity Researcher & Blue Teaming Enthusiast