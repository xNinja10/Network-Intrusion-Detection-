Network Intrusion Detection System (NIDS)

A simple, lightweight, and educational Network Intrusion Detection System (NIDS) built with Python and Scapy. This project is designed to monitor network traffic in real-time and detect potential threats based on a set of predefined signatures.

Features

Real-time Packet Sniffing:
Captures live network traffic from a specified interface.

Signature-Based Detection: Analyzes packets against a ruleset of known threat signatures.

Multi-Threat Detection: Capable of detecting various activities, including:

Common web attacks (SQL Injection, XSS)

Network scanning (Nmap Null/Xmas scans)

Suspicious tool usage (Nikto scanner)

Potential exploit attempts (Shellshock)

Logging and Alerting: Logs all detected alerts to both the console and a dedicated log file (nids_alerts.log).

Command-Line Interface: Easy to run with simple command-line arguments.

How It Works

The NIDS operates in a few simple steps:

Capture: The script uses the scapy library to listen on a specified network interface (e.g., eth0 for wired, wlan0 for wireless) and capture every packet.

Analyze: Each captured packet is passed to the packet_analyzer function. This function dissects the packet's layers (IP, TCP, Raw payload).

Detect: The analyzer compares the packet's contents against the THREAT_SIGNATURES dictionary. It checks for things like specific TCP flag combinations (for scans) or suspicious strings within the raw data payload (for web attacks or exploits).

Alert: If a packet matches a known signature, the log_alert function is triggered. It formats a detailed warning message and prints it to the screen while also saving it permanently in nids_alerts.log.

RequirementsPython 3.

xscapy library

Installation

Clone the repository:git clone https://github.com/your-username/python-nids.git
cd python-nids

Install the required Python library:pip install scapy

Usage

You must run the script with root privileges (sudo) to allow it to capture network packets.

Find your network interface:

On Linux/macOS: ifconfig or ip a

On Windows: ipconfig

Run the NIDS:

Replace eth0 with your actual network interface name.sudo python nids.py -i eth0


Monitor the output:

Alerts will be printed directly to your terminal and saved in nids_alerts.log.

$ sudo python nids.py -i eth0
INFO:root:Starting Network Intrusion Detection System on interface 'eth0'...
INFO:root:Alerts will be logged to 'nids_alerts.log'.
INFO:root:Press Ctrl+C to stop.
WARNING:root:ALERT! Threat Detected: 'Potential SQL Injection Attempt' | Source: 192.168.1.50 -> Destination: 192.168.1.10 | Details: Payload snippet: 1' OR '1'='1'--
To stop the sniffer, press Ctrl+C.

