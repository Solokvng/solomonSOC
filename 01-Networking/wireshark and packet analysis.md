# Wireshark & Packet Analysis

## 🎯 Objective
Capture and analyze normal network traffic to establish a baseline for DNS, HTTP, and TCP connections, and practice isolating conversations using Display Filters.

## 🛠️ Filters & Techniques Practiced
* **DNS Resolution (`dns`):** Verified how hostnames map to IPv4/IPv6 addresses over UDP port 53.
* **TCP 3-Way Handshake (`tcp.flags.syn == 1`):** Observed the `SYN` -> `SYN-ACK` -> `ACK` sequence establishing a reliable connection.
* **HTTP Traffic (`http.request`):** Inspected `GET` requests, User-Agent strings, and server response codes (`200 OK`).

## 📝 Lab Notes & Screenshots
### 1. Capturing a DNS Packet:
DNS(Domain Name System) helps in resolving domain names (google.com, cisco.com) to IP addresses in this packet capture, I captured packet from google using the command on a Command Line Interface(CLI) such as command prompt or the linux Terminal. to generate this traffic i ran 'ping www.google.com' from command prompt. I observed that the DNS server was queried over **UDP port 53** to resolve 'www.google.com. to its IP address with **0% packet loss**
<img width="1366" height="715" alt="_Wi-Fi 11_20_2026 1_36_09 PM" src="https://github.com/user-attachments/assets/14408bf1-6bb7-488e-8a47-091598f23641" />

### 2. Capturing a TCP Packet
TCP(Transmission Control Protocol) is a reliable protocol that ensures data packets arrive in the exact order in which they are sent and this is usually done using the three way handshake (SYN, SYN-ACK, ACK).To capture this I connected to the web and ran a webpage and filtered the capture on wireshark using 'tcp.flags.syn ==1', where I observed the client sending the initial 'SYN' packet, the server responding with the 'SYN-ACK' and then the client completing the session with the 'ACK' before data transfer began. from the capture observed i noticed that a there was a connection on port '443' which indicates that the connection was with a secure web sever.
<img width="1366" height="715" alt="_Wi-Fi 11_20_2026 2_37_26 PM" src="https://github.com/user-attachments/assets/bbdb56de-1c33-4bbd-bce2-0032590970c8" />


