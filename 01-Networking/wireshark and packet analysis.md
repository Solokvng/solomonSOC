# Wireshark & Packet Analysis

## 🎯 Objective
Capture and analyze normal network traffic to establish a baseline for DNS, HTTP, and TCP connections, and practice isolating conversations using Display Filters.

## 🛠️ Filters & Techniques Practiced
* **DNS Resolution (`dns`):** Verified how hostnames map to IPv4/IPv6 addresses over UDP port 53.
* **TCP 3-Way Handshake (`tcp.flags.syn == 1`):** Observed the `SYN` -> `SYN-ACK` -> `ACK` sequence establishing a reliable connection.
* **HTTP Traffic (`http.request`):** Inspected `GET` requests, User-Agent strings, and server response codes (`200 OK`).

## 📝 Lab Notes & Screenshots
