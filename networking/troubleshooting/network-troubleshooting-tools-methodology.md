# Network Troubleshooting Tools & Methodology

This lab documents my study of network troubleshooting methodology, diagnostic tools, command-line utilities, physical testing tools, and structured problem-solving from CompTIA Network+ coursework and practice.

The goal is to demonstrate my understanding of how network problems can be identified, isolated, tested, resolved, and documented using a consistent troubleshooting process.

## Concepts Practiced

- Structured troubleshooting methodology
- Identifying symptoms
- Establishing a theory of probable cause
- Testing theories
- Developing an action plan
- Implementing solutions
- Verifying functionality
- Documentation
- Escalation
- `ping`
- `tracert` / `traceroute`
- `ipconfig`
- `ifconfig`
- `ip`
- `nslookup`
- `dig`
- `arp`
- `netstat`
- `route`
- `pathping`
- `Test-NetConnection`
- `tcpdump`
- Wireshark
- Nmap
- Cable testers
- Tone generators and probes
- Loopback plugs
- Optical power meters
- Wi-Fi analyzers
- Protocol analyzers
- Network baselines
- Logs and monitoring

# Troubleshooting Methodology

A structured troubleshooting process helps reduce guesswork and prevents unnecessary changes.

A common troubleshooting methodology includes:

1. Identify the problem.
2. Establish a theory of probable cause.
3. Test the theory.
4. Establish a plan of action.
5. Implement the solution.
6. Verify full system functionality.
7. Document findings, actions, and outcomes.

Following a consistent process makes troubleshooting more efficient and easier to repeat.

# Step 1 — Identify the Problem

The first step is gathering information.

Questions may include:

- What is the user experiencing?
- When did the problem start?
- Is the problem constant or intermittent?
- Is one user affected or many?
- What changed recently?
- Which devices or applications are involved?
- What error messages are visible?
- Can the issue be reproduced?

Open-ended questions are often useful.

Example:

```text
User:
"I cannot access the internet."

Possible follow-up questions:

- Can you access internal resources?
- Are other users affected?
- Are you connected through Ethernet or Wi-Fi?
- Did this work earlier?
- Have any settings recently changed?
```

Good information gathering helps narrow the scope of the problem.

# Identify the Scope

The scope helps determine whether the issue is:

- One user
- One device
- One switch port
- One VLAN
- One subnet
- One building
- One application
- One network service
- The entire organization

Example:

```text
One workstation affected
        |
        v
Likely local device, port, or configuration issue

Entire office affected
        |
        v
Likely shared network or infrastructure issue
```

Scope can dramatically change the troubleshooting direction.

# Identify Recent Changes

Recent changes are an important troubleshooting clue.

Examples include:

- New firewall rules
- Switch configuration changes
- Software updates
- New VLANs
- DHCP changes
- DNS changes
- Cable replacement
- Hardware upgrades
- Routing changes

A problem beginning immediately after a change may be related to that change.

# Step 2 — Establish a Theory of Probable Cause

After gathering information, I develop possible explanations for the problem.

For example:

**Problem:** A workstation cannot reach the network.

Possible causes:

- Disconnected cable
- Disabled network adapter
- Incorrect IP address
- DHCP failure
- Incorrect VLAN
- Bad switch port
- DNS issue
- Default gateway problem

I start with the simplest or most likely cause before moving into more complex possibilities.

# Top-Down vs Bottom-Up Troubleshooting

Troubleshooting can sometimes be approached using the OSI model.

## Bottom-Up

Start with the physical layer and move upward.

Example:

```text
Layer 1 — Cable and signal
Layer 2 — Switching and VLAN
Layer 3 — IP addressing and routing
Layer 4 — TCP/UDP
Layer 7 — Application
```

This approach is useful when physical connectivity may be involved.

## Top-Down

Start with the application layer and move downward.

Example:

```text
Application
DNS
TCP/UDP
IP
Ethernet
Physical connection
```

This can be useful when the user reports a specific application problem.

## Divide and Conquer

Start somewhere in the middle.

For example:

```text
Can the user ping the default gateway?
```

If yes, Layer 1 through Layer 3 may be functioning locally.

If no, troubleshooting can focus lower in the stack.

This method can quickly narrow the problem.

# Step 3 — Test the Theory

The theory should be tested before making unnecessary changes.

Example:

**Theory:** DHCP is failing.

Tests:

```text
ipconfig /all
```

Look for:

- APIPA address
- Missing default gateway
- Missing DHCP server
- Incorrect subnet

Then test:

```text
ipconfig /release
ipconfig /renew
```

If a valid DHCP address is received, the theory may be supported.

# Step 4 — Establish a Plan of Action

Once the likely cause is identified, a solution should be planned.

The plan should consider:

- Potential impact
- Change approval
- Downtime
- Backup configuration
- Rollback plan
- Security implications
- User communication

For larger changes, implementation should follow organizational change-management procedures.

# Step 5 — Implement the Solution

The corrective action should address the verified cause.

Examples:

- Replace damaged cable
- Correct IP configuration
- Restore switch port
- Fix VLAN assignment
- Correct DNS settings
- Update firewall rule
- Renew DHCP lease
- Restart failed service
- Replace hardware

Only changes necessary to resolve the issue should be made.

# Step 6 — Verify Full Functionality

After applying a fix, verify that the original issue is actually resolved.

Verification may include:

- Reproduce the original task
- Test connectivity
- Test name resolution
- Test application access
- Verify multiple users if applicable
- Monitor for recurrence
- Confirm no new problems were introduced

A successful ping alone may not prove the entire issue is resolved.

# Step 7 — Document Findings

Documentation should include:

- Original problem
- Symptoms
- Scope
- Tests performed
- Root cause
- Changes made
- Final result
- Escalation details if applicable

Good documentation helps future troubleshooting and supports team knowledge.

---

# `ping`

`ping` tests basic IP connectivity using ICMP.

Example:

```text
ping 192.168.1.1
```

Possible uses:

- Test local TCP/IP stack
- Test default gateway
- Test remote host
- Test DNS by hostname
- Measure approximate response time

Example troubleshooting sequence:

```text
ping 127.0.0.1
ping local-IP
ping default-gateway
ping remote-IP
ping hostname
```

Each test provides information about where connectivity may be failing.

# Loopback Address

IPv4 loopback:

`127.0.0.1`

IPv6 loopback:

`::1`

Testing the loopback address verifies the local TCP/IP stack.

# `tracert` / `traceroute`

`tracert` on Windows and `traceroute` on many Linux systems show the path traffic takes toward a destination.

Example:

```text
tracert 8.8.8.8
```

This can help identify:

- Where routing stops
- Which routers are involved
- Possible WAN problems
- High-latency hops

A failed hop does not always mean the router itself is broken because some devices do not respond to traceroute traffic.

# `pathping`

`pathping` combines features of `ping` and `tracert`.

It can provide information about:

- Route path
- Latency
- Packet loss across hops

Example:

```text
pathping 8.8.8.8
```

This can be useful when investigating intermittent connectivity or packet loss.

# `ipconfig`

Windows `ipconfig` displays IP configuration.

Example:

```text
ipconfig
```

More detailed information:

```text
ipconfig /all
```

Useful information includes:

- IPv4 address
- IPv6 address
- Subnet mask
- Default gateway
- DNS servers
- DHCP status
- MAC address
- DHCP server

# Common `ipconfig` Commands

Release DHCP lease:

```text
ipconfig /release
```

Renew DHCP lease:

```text
ipconfig /renew
```

Clear DNS cache:

```text
ipconfig /flushdns
```

Display DNS cache:

```text
ipconfig /displaydns
```

# `ifconfig`

`ifconfig` is an older Linux and Unix network configuration tool.

It can display interface information such as:

- IP address
- Interface status
- MAC address

Modern Linux systems commonly prefer the `ip` command.

# `ip`

The Linux `ip` command can display and manage network information.

Examples:

```text
ip addr
ip link
ip route
```

These commands can show:

- Interface addresses
- Interface state
- Routing information

# `nslookup`

`nslookup` tests DNS resolution.

Example:

```text
nslookup example.com
```

It can help determine:

- Whether DNS responds
- Which server answered
- Which IP address was returned

If a user can reach an IP address but not a hostname, DNS should be investigated.

# `dig`

`dig` is another DNS query tool commonly available on Linux and Unix-like systems.

Example:

```text
dig example.com
```

It can provide detailed information about:

- DNS answers
- Record types
- Name servers
- Query timing

# `arp`

ARP associates IPv4 addresses with MAC addresses on a local network.

Windows example:

```text
arp -a
```

This displays the local ARP cache.

It can help identify:

- Known local devices
- IP-to-MAC mappings
- Unexpected ARP entries

# `netstat`

`netstat` displays network connections and listening ports.

Example:

```text
netstat -an
```

Possible uses:

- Identify active TCP connections
- Identify listening ports
- Review local network sessions
- Troubleshoot unexpected connections

# `route`

Routing commands show the local routing table.

Windows:

```text
route print
```

Linux:

```text
ip route
```

Routing tables help determine:

- Default route
- Local networks
- VPN routes
- Next hops
- Interface paths

# `Test-NetConnection`

PowerShell's `Test-NetConnection` can test connectivity and specific ports.

Example:

```powershell
Test-NetConnection server.example.com -Port 443
```

Useful results may include:

- DNS resolution
- Remote IP
- TCP connectivity
- Interface used

This is especially useful when testing whether a service port is reachable.

# `tcpdump`

`tcpdump` captures and displays network packets from the command line.

Example:

```text
tcpdump -i eth0
```

It can be used to inspect:

- TCP traffic
- UDP traffic
- ICMP
- DNS
- Network conversations

`tcpdump` is especially useful on Linux servers where a graphical packet analyzer may not be available.

# Wireshark

Wireshark provides graphical packet capture and analysis.

It can help troubleshoot:

- TCP handshakes
- DNS
- DHCP
- ICMP
- Retransmissions
- Port usage
- Application traffic

Wireshark provides deeper visibility when normal connectivity tools do not reveal the cause.

# Nmap

Nmap is a network discovery and scanning tool.

Authorized uses may include:

- Discovering hosts
- Identifying open ports
- Identifying network services
- Troubleshooting service availability

Example:

```text
nmap 192.168.1.10
```

Nmap should only be used on networks where scanning is authorized.

# Network Discovery Tools

Discovery tools help identify devices connected to a network.

Possible methods include:

- Ping sweep
- ARP table review
- Nmap
- SNMP
- LLDP
- CDP

These tools can help identify:

- Unauthorized devices
- Missing devices
- Network topology
- Device addresses

# LLDP

LLDP stands for **Link Layer Discovery Protocol**.

LLDP is a vendor-neutral Layer 2 discovery protocol.

It can provide information such as:

- Neighbor device
- Port
- Device identity
- Capabilities

# CDP

Cisco Discovery Protocol, or CDP, provides similar neighbor-discovery information on Cisco devices.

LLDP is standards-based, while CDP is Cisco-specific.

# Cable Tester

A cable tester can verify copper cabling.

It may detect:

- Opens
- Shorts
- Miswires
- Split pairs
- Incorrect pinouts

Cable testing is useful when physical connectivity is unreliable.

# Tone Generator and Probe

A tone generator and probe can help locate and identify cables.

The tone generator sends a signal through a cable.

The probe detects the signal.

This can be useful in environments with many unlabeled cables.

# Loopback Plug

A loopback plug sends transmitted signals back to the receiving pins of an interface.

It can help test whether a network interface is functioning properly.

# Optical Power Meter

An optical power meter measures the signal strength of fiber-optic links.

It can help identify:

- Excessive signal loss
- Weak optical power
- Fiber problems

# OTDR

An Optical Time Domain Reflectometer, or OTDR, is used to test fiber-optic cabling.

It can help identify:

- Fiber breaks
- Distance to a fault
- Signal loss
- Splice problems

# TDR

A Time Domain Reflectometer, or TDR, can help identify faults in copper cabling.

It can estimate the distance to problems such as:

- Cable breaks
- Shorts

# Wi-Fi Analyzer

A Wi-Fi analyzer provides information about wireless networks.

It may show:

- SSIDs
- Channels
- Signal strength
- Interference
- Nearby access points
- Channel utilization

This is useful when troubleshooting slow or unstable wireless connections.

# Spectrum Analyzer

A spectrum analyzer measures radio-frequency activity.

Unlike a basic Wi-Fi analyzer, it can identify interference from devices that are not Wi-Fi.

Examples may include:

- Microwave ovens
- Bluetooth devices
- Other radio sources

# Protocol Analyzer

A protocol analyzer examines network communication.

Wireshark is a common example.

Protocol analyzers can help identify:

- Packet structure
- Protocol behavior
- Errors
- Retransmissions
- Unexpected traffic

# Network TAP

A network TAP provides a copy of network traffic for monitoring.

It can be used with:

- Packet analyzers
- Security monitoring systems
- Network troubleshooting tools

# SPAN Port

A SPAN port mirrors traffic from one or more switch interfaces to another port.

A packet analyzer can connect to the destination port.

This provides visibility without placing the analyzer directly in the traffic path.

---

# Troubleshooting with the OSI Model

The OSI model provides a useful way to organize troubleshooting.

## Layer 1 — Physical

Check:

- Power
- Cables
- Connectors
- Link lights
- Transceivers
- Signal strength

Possible tools:

- Cable tester
- TDR
- OTDR
- Optical power meter

## Layer 2 — Data Link

Check:

- MAC address
- VLAN assignment
- Switch port status
- Trunking
- STP
- LACP

Possible tools:

- Switch MAC table
- LLDP
- CDP
- Wireshark

## Layer 3 — Network

Check:

- IP address
- Subnet mask
- Default gateway
- Routing table
- VLAN routing
- ACLs

Possible tools:

- `ping`
- `tracert`
- `route print`
- `ip route`

## Layer 4 — Transport

Check:

- TCP
- UDP
- Ports
- Connection state

Possible tools:

- `netstat`
- `Test-NetConnection`
- Nmap
- Wireshark

## Layer 7 — Application

Check:

- DNS
- HTTP/HTTPS
- Email
- Application configuration
- Authentication

Possible tools:

- `nslookup`
- `dig`
- Browser tests
- Application logs

# Example Scenario — No Network Connectivity

**Problem:** One workstation cannot access any network resources.

Troubleshooting process:

1. Check physical cable or Wi-Fi connection.
2. Verify link status.
3. Run `ipconfig /all`.
4. Check for APIPA.
5. Verify subnet mask.
6. Verify default gateway.
7. Ping `127.0.0.1`.
8. Ping the local IP address.
9. Ping the default gateway.
10. Check switch port and VLAN.
11. Test another cable or switch port if needed.
12. Document the results.

# Example Scenario — Internet Works but Internal Server Does Not

Possible process:

1. Verify local connectivity.
2. Ping the internal server by IP.
3. Check routing table.
4. Run `tracert`.
5. Verify VLANs and routing.
6. Review ACLs or firewall rules.
7. Check the server is online.
8. Verify required ports.
9. Test with `Test-NetConnection`.
10. Document findings.

# Example Scenario — Website Fails by Name but Works by IP

Possible process:

1. Confirm the website works by IP.
2. Run `nslookup`.
3. Check configured DNS servers.
4. Flush the DNS cache.
5. Test another hostname.
6. Verify DNS server availability.
7. Review DNS records.
8. Document findings.

This strongly suggests a DNS issue rather than a general connectivity issue.

# Example Scenario — Slow Network

Possible process:

1. Determine whether one or many users are affected.
2. Compare current performance with baseline.
3. Check interface utilization.
4. Review latency and packet loss.
5. Check interface errors.
6. Review NetFlow/IPFIX.
7. Identify top talkers.
8. Check for duplex or physical issues.
9. Review Wi-Fi interference if wireless.
10. Review monitoring data.
11. Document results.

# Example Scenario — Intermittent Connection

Possible causes include:

- Bad cable
- Failing switch port
- Wireless interference
- DHCP issue
- Duplicate IP
- Flapping interface
- Routing instability

Useful checks:

- Syslog
- Interface counters
- SNMP
- Packet loss
- Wi-Fi signal
- Cable test
- DHCP logs

# Example Scenario — Port 443 Unreachable

**Problem:** A server responds to ping but HTTPS does not work.

Possible process:

1. Confirm ping succeeds.
2. Run:

```powershell
Test-NetConnection server.example.com -Port 443
```

3. Check whether the service is listening.
4. Review firewall rules.
5. Review ACLs.
6. Confirm routing.
7. Use Nmap if authorized.
8. Review server logs.
9. Document findings.

This demonstrates that IP connectivity can work while an application port remains unavailable.

# Example Scenario — Wrong VLAN

**Problem:** A workstation receives an IP address from the wrong subnet.

Possible process:

1. Check `ipconfig /all`.
2. Identify the assigned subnet.
3. Check switch port configuration.
4. Verify access VLAN.
5. Check trunk configuration if needed.
6. Correct VLAN assignment.
7. Renew DHCP lease.
8. Verify new IP address.
9. Test connectivity.
10. Document the change.

# Example Scenario — Duplicate IP Address

Symptoms may include:

- Intermittent connectivity
- IP conflict warning
- Unexpected ARP entries
- One device losing connection when another appears

Possible process:

1. Identify the affected IP address.
2. Check DHCP leases.
3. Review static IP assignments.
4. Use `arp -a`.
5. Compare MAC addresses.
6. Correct duplicate configuration.
7. Test both devices.
8. Document findings.

# Example Scenario — High Packet Loss

Possible troubleshooting process:

1. Run continuous ping.
2. Use `pathping`.
3. Check interface errors.
4. Review switch port counters.
5. Test physical cabling.
6. Check wireless interference if applicable.
7. Review WAN utilization.
8. Compare against baseline.
9. Identify whether packet loss occurs locally or remotely.
10. Document results.

# Escalation

A problem should be escalated when:

- The issue exceeds my permissions
- The issue affects critical infrastructure
- Vendor support is required
- A hardware replacement requires approval
- A security incident is suspected
- A network-wide change is needed
- The root cause remains unclear after reasonable testing

Good escalation includes useful documentation rather than simply transferring the problem.

# Example Escalation Notes

```text
Issue:
Users in VLAN 20 cannot reach the application server.

Testing:
- Client IP configuration verified
- Default gateway reachable
- DNS resolution successful
- Server reachable by ping
- TCP 443 test failed
- Multiple users affected

Suspected cause:
Firewall or ACL blocking HTTPS between VLAN 20 and server network.

Escalation:
Network/security team review required.
```

This gives the next technician useful information immediately.

# Change Management

Some network fixes may require formal change control.

Examples include:

- Firewall rule changes
- Routing changes
- VLAN changes
- Firmware updates
- Switch configuration
- WAN changes

A good change process may include:

- Document planned change
- Assess risk
- Obtain approval
- Schedule maintenance
- Create rollback plan
- Implement
- Test
- Document results

# Baselines

Network baselines provide a reference for normal behavior.

Examples include:

- Normal latency
- Normal interface utilization
- Normal packet loss
- Normal CPU usage
- Normal bandwidth usage

A baseline helps determine whether current behavior is unusual.

# Logs and Monitoring

Logs and monitoring can provide important troubleshooting information.

Useful sources include:

- Syslog
- SNMP
- NetFlow/IPFIX
- Windows Event Viewer
- Linux logs
- Firewall logs
- VPN logs
- Application logs

Logs are especially useful for intermittent issues that are difficult to reproduce.

# Documentation

Good network documentation may include:

- Network diagrams
- IP address plans
- VLAN assignments
- Device names
- Port mappings
- Cable labels
- Firewall rules
- Routing information
- Change records
- Troubleshooting notes

Accurate documentation makes troubleshooting faster and safer.

# Safety and Authorization

Network troubleshooting tools should be used only in authorized environments.

Tools such as Nmap, packet capture utilities, and network scanners can reveal sensitive information or affect systems if misused.

I use these tools only for:

- Personal labs
- Coursework
- Authorized systems
- Troubleshooting environments where permission is granted

# Key Takeaways

Some of the most important concepts I learned include:

- Structured troubleshooting reduces guesswork.
- Scope helps determine whether a problem is local or widespread.
- Recent changes are often important clues.
- The OSI model can help organize troubleshooting.
- `ping` tests basic IP connectivity.
- `tracert` and `traceroute` show the network path.
- `ipconfig` and `ip` reveal local network configuration.
- `nslookup` and `dig` help troubleshoot DNS.
- `netstat` shows active connections and listening ports.
- `Test-NetConnection` can test specific TCP ports.
- Wireshark and `tcpdump` provide packet-level visibility.
- Nmap can identify hosts and services in authorized environments.
- Cable testers, TDRs, OTDRs, and optical meters help troubleshoot physical infrastructure.
- Wi-Fi and spectrum analyzers help investigate wireless problems.
- Logs and monitoring help identify intermittent and historical issues.
- Verification and documentation are part of completing the troubleshooting process.
- Good escalation provides useful evidence and testing results.

Understanding troubleshooting methodology helped me connect network tools, protocol knowledge, physical infrastructure, monitoring, and structured problem-solving into a repeatable process for diagnosing network issues.
