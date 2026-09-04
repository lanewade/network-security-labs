# Wireshark Packet Analysis Practice

This lab documents my Wireshark practice from networking coursework and Network+ study.

The goal is to strengthen my understanding of how network traffic looks in real captures and how protocols can be identified, filtered, and analyzed during troubleshooting.

## Concepts Practiced

- Packet capture
- Protocol identification
- Source and destination addressing
- TCP and UDP traffic
- DNS traffic
- DHCP traffic
- ICMP traffic
- HTTP and HTTPS traffic
- Port numbers
- TCP connection states
- Display filters
- Basic packet analysis
- Network troubleshooting using captured traffic

## Wireshark Interface

Wireshark captures network packets and displays detailed information about each frame.

Important areas of the interface include:

- **Packet List Pane** — displays captured packets
- **Packet Details Pane** — shows protocol information for a selected packet
- **Packet Bytes Pane** — shows the raw packet data
- **Display Filter Bar** — filters packets already captured
- **Capture Interfaces** — selects the network interface used for packet capture

## Common Display Filters

### IP Address

Filter traffic involving a specific IP address:

`ip.addr == 192.168.1.10`

Filter by source:

`ip.src == 192.168.1.10`

Filter by destination:

`ip.dst == 192.168.1.10`

## Protocol Filters

### DNS

`dns`

Useful for identifying DNS queries and responses.

### DHCP

`dhcp`

Useful for reviewing DHCP address assignment traffic.

### ICMP

`icmp`

Useful for analyzing ping traffic and connectivity testing.

### TCP

`tcp`

Displays TCP traffic.

### UDP

`udp`

Displays UDP traffic.

### HTTP

`http`

Displays unencrypted HTTP traffic.

### TLS

`tls`

Useful for identifying encrypted web traffic and TLS sessions.

## Port Filters

Filter traffic using a specific TCP port:

`tcp.port == 443`

Filter traffic using a specific UDP port:

`udp.port == 53`

Examples:

- Port 53 — DNS
- Port 80 — HTTP
- Port 443 — HTTPS
- Port 22 — SSH
- Port 3389 — RDP

## TCP Three-Way Handshake

A normal TCP connection begins with the three-way handshake:

1. SYN
2. SYN-ACK
3. ACK

Wireshark can be used to identify each part of the handshake and verify that a TCP connection was successfully established.

A useful filter for SYN packets is:

`tcp.flags.syn == 1`

## DNS Analysis

DNS traffic can be filtered with:

`dns`

A normal DNS process includes:

1. A client sends a DNS query.
2. The DNS server receives the request.
3. The server returns a response containing the requested record.
4. The client uses the returned IP address to communicate with the destination.

Wireshark can help troubleshoot DNS issues by showing whether:

- A query was sent
- A DNS server responded
- The correct record was returned
- Errors occurred during name resolution

## DHCP Analysis

DHCP can be examined to troubleshoot IP address assignment.

The traditional DHCP process is often remembered as DORA:

1. Discover
2. Offer
3. Request
4. Acknowledge

Wireshark can help identify whether the client and DHCP server are successfully completing this exchange.

## ICMP Analysis

ICMP is commonly used for connectivity testing.

A typical ping involves:

- ICMP Echo Request
- ICMP Echo Reply

Wireshark can show whether the request leaves the source and whether a reply is received.

This can help determine where connectivity may be failing.

## HTTP vs HTTPS

HTTP traffic is generally readable because it is not encrypted.

HTTPS uses TLS encryption, so the application data is protected.

Wireshark can still show information such as:

- Source and destination IP addresses
- Port numbers
- TCP connection details
- TLS handshake information

The encrypted application data itself is not normally readable without the appropriate session keys.

## Packet Troubleshooting Process

When reviewing a capture, I use a structured process:

1. Identify the device or connection involved.
2. Filter traffic using the relevant IP address or protocol.
3. Check source and destination addresses.
4. Identify the protocol and port being used.
5. Look for request and response traffic.
6. Check for errors, resets, retransmissions, or missing responses.
7. Compare the packet behavior with what should normally occur.
8. Document the findings.

## Example Troubleshooting Scenario — DNS

**Problem:** A workstation can reach an IP address but cannot access a website by name.

Possible troubleshooting process:

1. Filter traffic using:

   `dns`

2. Look for DNS queries from the workstation.
3. Verify the destination DNS server.
4. Check whether a DNS response is returned.
5. Review the response for the requested record.
6. Check for errors such as failed or unanswered queries.

If IP connectivity works but DNS resolution fails, the issue may be related to DNS configuration or DNS server availability.

## Example Troubleshooting Scenario — TCP Connection

**Problem:** A client cannot establish a connection to a server.

Possible troubleshooting process:

1. Filter by the destination IP or TCP port.
2. Look for the initial SYN packet.
3. Check whether a SYN-ACK is returned.
4. Verify whether the final ACK occurs.

If a SYN is repeatedly sent without receiving a SYN-ACK, possible causes include:

- The destination host is unreachable
- A firewall is blocking the connection
- The service is not listening
- The destination port is closed
- A routing problem exists

## Tools Used

- Wireshark
- Windows networking commands
- Linux networking commands
- `ping`
- `nslookup`
- `tracert` / `traceroute`
- `ipconfig`
- `tcpdump`

## Key Takeaways

Wireshark helped me connect networking concepts with what actually happens on the wire.

Instead of only memorizing protocols and ports, packet analysis makes it possible to see:

- How devices communicate
- How protocols interact
- How TCP connections are established
- How DNS and DHCP exchanges work
- How connectivity failures appear in captured traffic
- How filtering can isolate relevant packets during troubleshooting

Packet analysis is useful for both network troubleshooting and cybersecurity because it provides visibility into how systems communicate across a network.

## Safety Note

Packet captures can contain sensitive information.

I only capture and analyze traffic in authorized lab environments and avoid uploading packet captures containing private credentials, personal information, internal company data, or other sensitive content.
