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

### 5. Traceroute(Linux: traceroute, windows: tracert)
This diagnostic command is used to track the exact data path and measure the transit, delays of data packets travelling from a device to a destination(server). When the Time To Live(TTL=1) sends an ICMP echo request packet to the destination with a TTL of 1, the router receives it, and the TTL decreases by 1 to 0, the router drops the packet and sends back an ICMP 'Time Exceeded" message. If TTL=2 then the router sends it to the ISP before it decreases to zero so the TTL increments occur by 1 until it gets to the final destination.
<img width="1366" height="738" alt="Command Prompt 11_20_2026 8_11_29 PM" src="https://github.com/user-attachments/assets/e8ba6de8-5d3a-49db-812c-af9005a62df9" />
I ran the tracert command in Command Prompt to a destination of 8.8.8.8, and I got the result above whilst also capturing packets in Wireshark. From the result, column 1 stands for hop number, columns 2- 4 stand for round-trip times in milliseconds for each attempt (3), and column 5 is the Router Hostname and IP.
<img width="1366" height="715" alt="Capturing from Wi-Fi 11_20_2026 8_20_46 PM" src="https://github.com/user-attachments/assets/9247a7c2-a305-4852-8959-2a320b9e6fae" />
I captured traffic using the tracert command and got a request timed out on one of the results but that doesnt necessarily mean that packets are being dropped just happens that some ISP configures their routers to silently drop ICMP packets to prevent DOS attacks while forwarding your data. the only problem is when a timeout starts at a specific hop and never recover.

### 5. DHCP(Dynamic Host Configuration Protocol)
DHCP automatically assigns IP addresses to devices when they connect to a network. i ran the command 'ipconfig /renew' in Command Prompt and captured traffic on Wireshark. I noticed the messages sent from the client to the DHCP server to get the IP address start with a 'DHCP Discover' sent by the client, the DHCP server responds with a 'DHCP Offer' message which contains the IP address, subnet mask, DNS server, default gateway and lease time. After this, the client responds with a 'DHCP Request' to accept the IP address offered by the DHCP server, the DHCP server responds with the final message 'DHCP Ack' to acknowledge the confirmation of assigning the IP address.
<img width="1366" height="715" alt="Capturing from Wi-Fi 11_21_2026 9_56_05 AM" src="https://github.com/user-attachments/assets/db52ea72-fd74-4455-9dc4-94c29035e5f3" />
<img width="1366" height="715" alt="Capturing from Wi-Fi 11_21_2026 10_15_21 AM" src="https://github.com/user-attachments/assets/c2c58133-3c1f-467d-8dd6-7a7899798284" /> 
as seen in this picture above the messages shown are the process i got an IP address on my device

### 6. HTTP(HyperText Transfer Protocol)
used in communication between client and server the common method for a request is 'GET' which is used to request a resource while the server responds with a status code and the resources being requested.
status codes include: 200: Ok, 201: Moved Permanently, 404: Not Found, 500: Internal Server Error
<img width="1366" height="715" alt="_Adapter for loopback traffic capture 11_23_2026 6_20_12 PM" src="https://github.com/user-attachments/assets/2ce68657-ba53-4d2a-91a1-647affb6cadf" />
i captured packets from a local server on wireshark from the packet capture we can see the GET request from the client and the response from the server with a status code. 
HTTPS(HyperText Transfer Protocol Secure): uses SSL or TSL(Transport Layer Security) to secure communication by encryption. a server sends it's digital certificate and public key to the client to verify the server identity,The client validates the certificate. It then generates a unique Session Key and encrypts it using the server's Public Key.The server uses its Private Key to decrypt the Session Key. A secure, authenticated connection is now established. in HTTPS All subsequent data (request and response) is sent through an "ENCRYPTED TUNNEL (SSL/TLS)".Even if intercepted, the data is scrambled (e.g., "SESSION KEY ENCRYPTION") and unreadable without the Session Key.
HTTP traffic is sent using TCP port 80 whilst HTTPS uses TCP port 443

