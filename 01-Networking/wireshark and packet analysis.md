# Wireshark & Packet Analysis

## 🎯 Objective
Capture and analyze normal network traffic to establish a baseline for DNS, HTTP, and TCP connections, and practice isolating conversations using Display Filters.

## 🛠️ Filters & Techniques Practiced
* **DNS Resolution (`dns`):** Verified how hostnames map to IPv4/IPv6 addresses over UDP port 53.
* **TCP 3-Way Handshake (`tcp.flags.syn == 1`):** Observed the `SYN` -> `SYN-ACK` -> `ACK` sequence establishing a reliable connection.
* **HTTP Traffic (`http.request`):** Inspected `GET` requests, User-Agent strings, and server response codes (`200 OK`).

## 📝 Lab Notes & Screenshots
### 1. capturing a DNS packet:
DNS(Domain Name System) helps in resolving domain names (google.com, cisco.com) to IP addresses in this packet capture, I captured packet from google using the command on a Command Line Interface(CLI) such as command prompt or the linux Terminal. to generate this traffic i ran 'ping www.google.com' from command prompt. I observed that the DNS server was queried over **UDP port 53** to resolve 'www.google.com. to its IP address with **0% packet loss**
<img width="1366" height="715" alt="_Wi-Fi 11_20_2026 1_36_09 PM" src="https://github.com/user-attachments/assets/14408bf1-6bb7-488e-8a47-091598f23641" />
