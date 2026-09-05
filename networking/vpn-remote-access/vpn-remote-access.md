# VPNs & Remote Access

This lab documents my study of Virtual Private Networks (VPNs), tunneling, remote connectivity, authentication, and secure remote access from CompTIA Network+ coursework and practice.

The goal is to demonstrate my understanding of how VPNs securely connect users and networks across untrusted networks such as the internet, how different VPN designs work, and how to troubleshoot common remote-access problems.

## Concepts Practiced

- Virtual Private Networks (VPNs)
- Remote-access VPNs
- Site-to-site VPNs
- VPN tunnels
- Full tunneling
- Split tunneling
- IPsec
- IKE
- ESP
- NAT Traversal
- SSL/TLS VPNs
- L2TP/IPsec
- PPTP concepts and limitations
- Remote authentication
- RADIUS
- Multi-Factor Authentication (MFA)
- SSH
- RDP
- Secure remote administration
- VPN troubleshooting
- DNS and routing over VPNs

## What Is a VPN?

A Virtual Private Network creates a logical connection across another network, commonly the internet.

A VPN can provide a secure path between:

- A remote user and an organization
- Two office locations
- Two networks
- A device and a cloud environment

Conceptually:

```text
Remote User
    |
    v
 Internet
    |
    v
Encrypted VPN Tunnel
    |
    v
Corporate Network
```

The VPN tunnel allows traffic to travel across an untrusted network while protecting the communication.

## VPN Benefits

VPNs can provide:

- Encryption
- Confidentiality
- Integrity
- Secure remote access
- Site-to-site connectivity
- Protection when using untrusted networks
- Access to internal resources
- Centralized remote connectivity

A VPN does not automatically make every system secure, but it protects network communication when properly configured.

## Remote-Access VPN

A remote-access VPN connects an individual user or device to another network.

This is commonly used by employees working from:

- Home
- Hotels
- Airports
- Remote offices
- Other external locations

Example:

```text
Employee Laptop
      |
      v
   Internet
      |
      v
VPN Gateway
      |
      v
Internal Network
```

The user's device runs VPN software or uses an operating-system VPN client to establish the secure connection.

## Site-to-Site VPN

A site-to-site VPN connects entire networks.

Example:

```text
Office A
192.168.10.0/24
      |
VPN Gateway
      |
====== Internet ======
      |
VPN Gateway
      |
Office B
192.168.20.0/24
```

Devices at each location can communicate across the encrypted tunnel without each user creating an individual VPN connection.

Site-to-site VPNs are commonly used to connect:

- Branch offices
- Data centers
- Corporate locations
- Cloud networks

## VPN Tunnel

A VPN tunnel encapsulates network traffic so it can travel across another network.

Depending on the VPN technology, the traffic may also be:

- Encrypted
- Authenticated
- Integrity protected

The original traffic is carried inside another protocol as it crosses the external network.

## Encapsulation

Encapsulation places one set of network data inside another protocol.

Conceptually:

```text
Original Packet
      |
      v
VPN Encapsulation
      |
      v
Transport Across Internet
      |
      v
VPN Decapsulation
      |
      v
Original Packet Delivered
```

The receiving VPN endpoint removes the VPN encapsulation and forwards the original traffic.

## IPsec

IPsec, or Internet Protocol Security, is a group of protocols used to secure IP communication.

IPsec can provide:

- Encryption
- Authentication
- Integrity
- Anti-replay protection

IPsec is commonly used for:

- Site-to-site VPNs
- Remote-access VPNs
- Secure network-to-network communication

## IPsec Modes

IPsec can operate in two general modes.

### Transport Mode

Transport mode protects the payload of the original IP packet.

The original IP header remains available for routing.

### Tunnel Mode

Tunnel mode protects the entire original IP packet by encapsulating it inside a new packet.

Tunnel mode is commonly associated with VPN connections between network gateways.

## ESP

Encapsulating Security Payload, or ESP, is an IPsec protocol used to protect network traffic.

ESP can provide:

- Encryption
- Integrity
- Authentication
- Anti-replay protection

ESP is widely used with modern IPsec VPNs.

## IKE

Internet Key Exchange, or IKE, helps VPN peers establish secure IPsec communication.

IKE is responsible for tasks such as:

- Authenticating VPN peers
- Negotiating security parameters
- Establishing encryption keys
- Creating security associations

IKE commonly uses UDP port:

`500`

When NAT Traversal is required, IPsec commonly uses UDP port:

`4500`

## NAT Traversal

NAT can interfere with some IPsec traffic because addresses are modified as packets pass through a NAT device.

NAT Traversal, commonly called NAT-T, allows IPsec traffic to work through NAT environments.

NAT-T commonly encapsulates IPsec traffic using UDP port:

`4500`

## SSL/TLS VPN

Some remote-access VPN solutions use TLS to secure connections.

TLS-based VPNs are convenient because they can operate through networks that already allow HTTPS-style traffic.

Some implementations use:

`TCP 443`

TLS VPN designs may use:

- Dedicated VPN clients
- Browser-based access
- Application portals

The exact implementation depends on the VPN platform.

## Client-Based VPN

A client-based VPN requires software on the user's device.

The client handles tasks such as:

- Authentication
- Tunnel creation
- Encryption
- Routing
- Connection management

Client software may be provided by:

- The operating system
- A VPN vendor
- An organization

## Clientless VPN

A clientless VPN may allow access through a web browser without requiring a traditional full VPN client.

This may provide access to selected internal applications instead of providing complete network access.

Example:

```text
Remote User
    |
Web Browser
    |
HTTPS / TLS
    |
VPN Portal
    |
Internal Application
```

## Full Tunnel

With full tunneling, the user's network traffic is routed through the VPN.

Conceptually:

```text
Remote Laptop
     |
     v
VPN Tunnel
     |
     v
Corporate Network
     |
     v
Internet / Internal Resources
```

Advantages may include:

- Centralized security inspection
- Consistent organizational policies
- Improved visibility

Potential disadvantages include:

- Increased VPN bandwidth usage
- Additional load on VPN infrastructure
- Increased latency for general internet traffic

## Split Tunnel

With split tunneling, only selected traffic uses the VPN.

Example:

```text
Internal Traffic ---> VPN Tunnel ---> Corporate Network

Internet Traffic -------------------> Local Internet Connection
```

Advantages may include:

- Reduced VPN bandwidth usage
- Lower load on corporate VPN infrastructure
- More direct internet access

Security considerations include:

- Some traffic bypasses organizational security controls
- The endpoint may communicate with both internal and external networks simultaneously

Organizations must decide whether split tunneling is appropriate for their security requirements.

## VPN Authentication

Before establishing remote access, a VPN typically verifies the user's identity.

Authentication methods may include:

- Username and password
- Certificates
- Smart cards
- MFA
- Security tokens
- RADIUS

Strong authentication reduces the risk of unauthorized VPN access.

## Multi-Factor Authentication

MFA requires more than one category of authentication factor.

Example:

```text
Password
   +
Authenticator App
```

Because VPN access may provide entry into internal resources, MFA is commonly used for remote-access VPNs.

## RADIUS

RADIUS can provide centralized authentication, authorization, and accounting for remote network access.

A simplified VPN process might be:

```text
Remote User
     |
     v
VPN Gateway
     |
     v
RADIUS Server
     |
     v
Authentication Decision
```

The VPN gateway sends the authentication request to the RADIUS server.

If authentication and policy requirements are satisfied, the VPN connection may be allowed.

## Remote Desktop Protocol

Remote Desktop Protocol, or RDP, allows remote graphical access to Windows systems.

RDP commonly uses:

`TCP/UDP 3389`

RDP is not itself a VPN.

A secure design may require users to establish a VPN before connecting to an internal system with RDP.

Example:

```text
Remote User
    |
    v
VPN
    |
    v
Internal Network
    |
    v
RDP to Workstation
```

RDP should not normally be exposed directly to the public internet without appropriate security controls.

## SSH

Secure Shell, or SSH, provides secure command-line remote administration.

SSH commonly uses:

`TCP 22`

SSH can provide:

- Encrypted remote terminal sessions
- Remote system administration
- Secure file transfer
- Tunneling capabilities

SSH is commonly used with:

- Linux systems
- Routers
- Switches
- Servers
- Network appliances

## Telnet vs SSH

Telnet is an older remote-access protocol that does not provide the same encryption protection as SSH.

Common ports:

```text
Telnet: TCP 23
SSH:    TCP 22
```

SSH should generally be preferred for secure remote administration.

## RDP vs VPN

RDP and VPN serve different purposes.

A VPN creates secure network connectivity.

RDP provides remote graphical access to another computer.

They can be used together:

```text
User
 |
VPN
 |
Corporate Network
 |
RDP
 |
Workstation
```

The VPN protects network access while RDP provides the remote desktop session.

## Common VPN Protocol Concepts

### IPsec

Commonly used for secure site-to-site and remote-access connections.

### L2TP/IPsec

Layer 2 Tunneling Protocol can be combined with IPsec for encryption and protection.

L2TP commonly uses:

`UDP 1701`

When used securely, IPsec provides the security rather than L2TP alone.

### PPTP

Point-to-Point Tunneling Protocol is an older VPN technology.

PPTP is considered insecure for modern deployments and should generally be avoided.

PPTP historically used:

`TCP 1723`

and GRE for tunneled traffic.

Studying PPTP is still useful for recognizing legacy network technologies.

## VPN Routing

After a VPN connection is established, the client must know which traffic should use the tunnel.

The VPN software may install routes into the client's routing table.

Example:

```text
Corporate Network:
10.20.0.0/16

Route:
10.20.0.0/16 -> VPN Interface
```

Traffic destined for the corporate network is then sent through the VPN.

Incorrect routes can cause VPN connectivity problems even when the tunnel itself is successfully connected.

## VPN and DNS

VPN clients may receive DNS settings from the organization.

For example:

```text
VPN Client
   |
   v
Internal DNS Server
   |
   v
internal.example.com
```

A VPN may appear connected while internal resources still fail because of DNS problems.

Possible issues include:

- Incorrect DNS server
- DNS traffic not routed through the tunnel
- Missing internal DNS records
- Split-DNS configuration problems
- Firewall rules blocking DNS

## VPN and DHCP

Some VPN solutions assign virtual IP addresses to remote clients.

The client may receive:

- VPN IP address
- Subnet information
- DNS server
- Routes
- Other configuration

The addressing mechanism depends on the VPN platform.

## Site-to-Site Routing

Site-to-site VPN gateways must know which remote networks are reachable through the tunnel.

Example:

```text
Office A
192.168.10.0/24
        |
        v
VPN Tunnel
        |
        v
Office B
192.168.20.0/24
```

Office A must have a route for:

`192.168.20.0/24`

Office B must have a route for:

`192.168.10.0/24`

Routing problems can make the VPN tunnel appear established while traffic still fails.

## Overlapping Subnets

VPN connectivity can become difficult when both sides use the same IP subnet.

Example:

```text
Remote Home Network:
192.168.1.0/24

Corporate Network:
192.168.1.0/24
```

The client may not know whether `192.168.1.x` traffic belongs to the local network or the remote VPN network.

Avoiding overlapping address spaces helps prevent routing conflicts.

## Firewall Considerations

Firewalls must allow required VPN traffic.

Depending on the technology, this may include:

- UDP 500 for IKE
- UDP 4500 for NAT-T
- TCP 443 for some TLS VPNs
- Other vendor-specific ports or protocols

Firewall rules should allow only required traffic.

## Example Remote-Access VPN Design

```text
Remote Employee
      |
      v
   Internet
      |
      v
Firewall / VPN Gateway
      |
      v
Authentication
      |
      v
Internal Network
      |
      +---- File Server
      |
      +---- Internal Applications
      |
      +---- RDP Workstation
```

The user authenticates to the VPN gateway before receiving access to approved internal resources.

## Example Site-to-Site VPN Design

```text
Memphis Office
10.10.0.0/16
      |
   Firewall
      |
      |<==== IPsec VPN ====>
      |
   Firewall
      |
Dallas Office
10.20.0.0/16
```

The two gateways maintain the tunnel.

Users at each location can communicate with approved systems on the other network.

## VPN Troubleshooting Process

When troubleshooting a VPN, I use a structured process:

1. Verify normal internet connectivity.
2. Confirm the VPN server or gateway address.
3. Check user credentials.
4. Verify MFA if required.
5. Confirm the VPN client configuration.
6. Check the client IP address.
7. Verify the VPN tunnel establishes successfully.
8. Check the routing table.
9. Verify internal DNS configuration.
10. Test the remote gateway.
11. Test an internal IP address.
12. Test internal name resolution.
13. Check firewall rules.
14. Verify remote network routes.
15. Check for overlapping subnets.
16. Review VPN logs when available.
17. Document the findings.

## Useful Troubleshooting Commands

### `ipconfig /all`

Displays Windows network interfaces, IP addresses, gateways, and DNS configuration.

### `route print`

Displays the Windows routing table.

This is useful for checking whether the VPN installed the expected routes.

### `ping`

Can test IP connectivity when ICMP is permitted.

### `tracert`

Can help identify the network path being used.

### `nslookup`

Helps verify DNS resolution.

### `Test-NetConnection`

PowerShell can test network connectivity and ports.

Example:

```powershell
Test-NetConnection server.example.com -Port 443
```

## Example Troubleshooting Scenario — VPN Connects but Internal Resources Fail

**Problem:** A user successfully connects to the VPN but cannot reach an internal server.

Possible troubleshooting process:

1. Confirm the VPN shows connected.
2. Verify the client's VPN-assigned address.
3. Check the routing table.
4. Confirm a route exists for the internal subnet.
5. Ping the internal gateway if permitted.
6. Test the server by IP address.
7. Test the server by hostname.
8. Check DNS configuration.
9. Review firewall and ACL rules.
10. Verify return routing from the internal network.
11. Document the findings.

If the tunnel is connected but no route exists to the internal subnet, the problem may be routing rather than authentication.

## Example Troubleshooting Scenario — Internal IP Works but Name Does Not

**Problem:** A user can connect to:

`10.20.5.10`

but cannot reach:

`fileserver.example.local`

This suggests IP connectivity may be functioning while DNS resolution is failing.

Possible checks include:

1. Run `nslookup`.
2. Verify the VPN-provided DNS server.
3. Check whether DNS traffic uses the VPN.
4. Verify the internal DNS record.
5. Check split-DNS configuration.
6. Flush the DNS cache.
7. Retest.

## Example Troubleshooting Scenario — VPN Will Not Establish

**Problem:** The VPN client cannot establish a connection.

Possible checks include:

1. Verify internet connectivity.
2. Confirm the VPN gateway address.
3. Verify credentials.
4. Confirm MFA.
5. Check system date and time.
6. Check firewall rules.
7. Verify required VPN ports.
8. Check whether NAT-T is required.
9. Review client logs.
10. Compare with another network or device if appropriate.
11. Escalate if the VPN gateway itself appears unavailable.

## Remote Access Security Practices

Good remote-access practices include:

- Use MFA
- Use strong authentication
- Prefer modern VPN protocols
- Avoid legacy technologies such as PPTP
- Restrict remote access to authorized users
- Apply least privilege
- Keep VPN software updated
- Monitor remote connections
- Log authentication events
- Use secure remote administration protocols
- Avoid exposing RDP directly to the internet
- Disable unnecessary remote-access services
- Use certificates where appropriate

## VPN Performance Considerations

VPN performance may be affected by:

- Internet connection speed
- Latency
- Encryption overhead
- VPN gateway capacity
- Number of connected users
- Full vs split tunneling
- Packet loss
- MTU problems
- Geographic distance

A slow VPN does not necessarily mean the VPN server itself is failing.

## MTU Considerations

VPN encapsulation adds additional headers to packets.

This can increase packet size and sometimes cause fragmentation or transmission problems.

MTU-related problems may appear as:

- Certain websites not loading
- Large transfers failing
- Applications partially working
- Intermittent connectivity

MTU and fragmentation should be considered when basic VPN connectivity works but specific traffic fails.

## Remote Access and Network Security

VPNs connect directly with many other networking concepts, including:

- Routing
- DNS
- DHCP
- Firewalls
- ACLs
- Authentication
- IP addressing
- Network segmentation
- Remote administration
- Encryption

A successful VPN connection requires more than authentication.

The network must also correctly handle addressing, routing, DNS, firewall policies, and access controls.

## Key Takeaways

Some of the most important concepts I learned include:

- VPNs provide secure connectivity across untrusted networks.
- Remote-access VPNs connect individual users.
- Site-to-site VPNs connect entire networks.
- IPsec provides encryption, integrity, and authentication for IP traffic.
- IKE helps VPN peers negotiate security settings and keys.
- NAT-T helps IPsec operate through NAT.
- Full tunneling sends traffic through the VPN.
- Split tunneling sends selected traffic through the VPN.
- MFA strengthens remote-access authentication.
- RADIUS can provide centralized remote-access authentication.
- SSH provides secure command-line administration.
- RDP provides remote graphical access but is not itself a VPN.
- VPN routing and DNS configuration are common troubleshooting areas.
- A VPN tunnel can be established successfully while routing or DNS still fails.
- Secure remote access combines networking, authentication, encryption, routing, and access control.

Understanding VPNs and remote access helped me connect routing, DNS, firewalls, authentication, encryption, and troubleshooting into a complete view of how remote users and remote networks securely communicate.
