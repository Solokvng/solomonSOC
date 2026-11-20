# Wireshark & Packet Analysis

## 🎯 Objective
Capture and analyze normal network traffic to establish a baseline for DNS, HTTP, and TCP connections, and practice isolating conversations using Display Filters.

## 🛠️ Filters & Techniques Practiced
* **DNS Resolution (`dns`):** Verified how hostnames map to IPv4/IPv6 addresses over UDP port 53.
* **TCP 3-Way Handshake (`tcp.flags.syn == 1`):** Observed the `SYN` -> `SYN-ACK` -> `ACK` sequence establishing a reliable connection.
* **HTTP Traffic (`http.request`):** Inspected `GET` requests, User-Agent strings, and server response codes (`200 OK`).

## 📝 Lab Notes & Screenshots
### 1. Capturing a DNS Packet:
DNS(Domain Name System) helps in resolving domain names (google.com, cisco.com) to IP addresses in this packet capture, I captured packet from google using the command-line interface (CLI) such as Command Prompt or the Linux Terminal. to generate this traffic i ran 'ping www.google.com' from Command Prompt. I observed that the DNS server was queried over **UDP port 53** to resolve 'www.google.com. to its IP address with **0% packet loss**
<img width="1366" height="715" alt="_Wi-Fi 11_20_2026 1_36_09 PM" src="https://github.com/user-attachments/assets/14408bf1-6bb7-488e-8a47-091598f23641" />

### 2. Capturing a TCP Packet
TCP(Transmission Control Protocol) is a reliable protocol that ensures data packets arrive in the exact order in which they are sent and this is usually done using the three way handshake (SYN, SYN-ACK, ACK).To capture this I connected to the web and ran a webpage and filtered the capture on wireshark using 'tcp.flags.syn ==1', where I observed the client sending the initial 'SYN' packet, the server responding with the 'SYN-ACK' and then the client completing the session with the 'ACK' before data transfer began. from the capture observed i noticed that a there was a connection on port '443' which indicates that the connection was with a secure web sever.
<img width="1366" height="715" alt="_Wi-Fi 11_20_2026 2_37_26 PM" src="https://github.com/user-attachments/assets/bbdb56de-1c33-4bbd-bce2-0032590970c8" />

### 3. Analysing a TCP Packet Capture
in this packet capture, it was observed that some packets were out of order, previous segments were not captured, there were duplicated acknowledgements, and there were retransmissions
For packets were previous segment not captured, this happens when a received packet with a higher sequence number than expected is received. it occurs because either a packet was dropped before getting to the machine, Network interface card or wireshark dropped the packet due to spikes. i found a packet capture flagged as out of order

Another flag encountered was 'TCP out-of-order'; packets arrive at their destination in a different order than they were sent. This occurs when a router is balancing traffic across different paths and then a packet takes a slightly faster route than another packet its supposed to come after, but it arrives first.
<img width="1046" height="638" alt="_Ethernet 11_20_2026 5_49_30 PM" src="https://github.com/user-attachments/assets/17b85455-7e75-4941-906b-7978350dc3cd" />


There is another flag I encountered called Retransmission when the server resends a packet that has already been transmitted caused by either the original packet being lost or the device confirming receipt of the packet being lost.
<img width="1366" height="715" alt="_Wi-Fi 11_20_2026 3_10_15 PM" src="https://github.com/user-attachments/assets/a18973f6-1cc3-4fe8-9820-24b3f09b9163" />

### 4. Capturing ICMP Packets
ICMP(Internet Control Message Protocol) is a protocol used by networking devices to send error messages and operational diagnostics back to the source IP address (it reports on the health and delivery of the IP packets). it is connectionless, no handshake. if an ICMP packet gets dropped, another ICMP error is not generated 
I captured an ICMP packet by pinging '8.8.8.8'
<img width="1366" height="715" alt="Capturing from Wi-Fi 11_20_2026 6_52_13 PM" src="https://github.com/user-attachments/assets/01097f78-573a-44c3-8974-78b510d6eb25" />



