# Wireless Networking & Wi-Fi Security

This lab documents my wireless networking and Wi-Fi security practice from CompTIA Network+ coursework and study.

The goal is to demonstrate my understanding of wireless standards, frequency bands, channels, access points, wireless security, interference, and structured Wi-Fi troubleshooting.

## Concepts Practiced

- IEEE 802.11 wireless standards
- 2.4 GHz, 5 GHz, and 6 GHz wireless bands
- Wi-Fi channels
- Channel overlap
- Access points
- SSIDs and BSSIDs
- Infrastructure and ad hoc wireless networks
- Wireless roaming
- WPA2 and WPA3
- Wireless authentication
- Guest networks
- Wireless interference
- MIMO and MU-MIMO
- Beamforming
- OFDM and OFDMA
- Channel bonding
- DFS
- Wireless troubleshooting
- Wireless security threats

## Wireless Network Basics

Wireless LANs allow devices to communicate using radio frequency signals instead of physical Ethernet connections.

Common wireless devices include:

- Laptops
- Smartphones
- Tablets
- Wireless printers
- IoT devices
- Wireless access points
- Wireless routers

A wireless access point connects wireless devices to a wired network.

## SSID

The **SSID**, or Service Set Identifier, is the human-readable name of a wireless network.

Examples:

- Corporate-WiFi
- Guest
- HomeNetwork

Multiple access points can broadcast the same SSID to provide coverage across a larger area.

## BSSID

The **BSSID** identifies a specific wireless access point or radio interface within a wireless network.

While multiple access points may share the same SSID, each individual access point has its own BSSID.

This helps distinguish one wireless access point from another.

## Infrastructure Mode

Infrastructure mode is the most common wireless network design.

Wireless clients connect through an access point rather than communicating directly with each other.

Example:

```text
Laptop
   \
Phone ---- Wireless Access Point ---- Wired Network
   /
Tablet
```

This design allows wireless devices to access network resources and the internet through the access point.

## Ad Hoc Mode

In an ad hoc wireless network, devices communicate directly with one another without using a traditional access point.

This is different from infrastructure mode, where wireless communication is coordinated through an access point.

## 2.4 GHz Band

The 2.4 GHz band generally provides:

- Longer range
- Better penetration through walls
- Fewer non-overlapping channels
- Greater potential for interference

In North America, channels **1, 6, and 11** are commonly used because they do not overlap when using traditional 20 MHz channel widths.

Common sources of 2.4 GHz interference may include:

- Nearby Wi-Fi networks
- Bluetooth devices
- Microwave ovens
- Some cordless devices
- Other radio-frequency equipment

## 5 GHz Band

The 5 GHz band generally provides:

- More available channels
- Less congestion than 2.4 GHz
- Higher potential throughput
- Shorter range than 2.4 GHz
- Less wall penetration

5 GHz is commonly used for modern high-performance Wi-Fi networks.

## 6 GHz Band

Wi-Fi 6E and newer wireless technologies can use the 6 GHz spectrum.

The 6 GHz band provides additional wireless spectrum and can reduce congestion compared with older frequency bands.

Devices must support 6 GHz operation to use it.

## Common Wi-Fi Standards

| Standard | Common Name | Frequency Bands | Notes |
|---|---|---|---|
| 802.11a | — | 5 GHz | Up to 54 Mbps |
| 802.11b | — | 2.4 GHz | Older standard |
| 802.11g | — | 2.4 GHz | Up to 54 Mbps |
| 802.11n | Wi-Fi 4 | 2.4 / 5 GHz | Introduced MIMO |
| 802.11ac | Wi-Fi 5 | 5 GHz | Higher throughput and wider channels |
| 802.11ax | Wi-Fi 6 | 2.4 / 5 GHz | Uses OFDMA and improved efficiency |
| 802.11ax | Wi-Fi 6E | 6 GHz support | Extends Wi-Fi 6 into 6 GHz |

## OFDM

Orthogonal Frequency Division Multiplexing, or OFDM, divides wireless communication into multiple subcarriers.

OFDM is used by several modern Wi-Fi standards to improve efficient data transmission.

## OFDMA

Orthogonal Frequency Division Multiple Access, or OFDMA, improves efficiency by dividing a wireless channel into smaller resource units.

Different clients can use portions of the channel at the same time.

OFDMA is an important feature of Wi-Fi 6.

## MIMO

Multiple Input Multiple Output, or MIMO, uses multiple antennas to transmit and receive multiple data streams.

This can improve:

- Throughput
- Reliability
- Wireless performance

## MU-MIMO

Multi-User MIMO allows an access point to communicate with multiple wireless clients more efficiently.

Instead of serving only one client at a time, compatible access points can handle multiple clients simultaneously.

## Beamforming

Beamforming focuses wireless signal energy toward a client instead of transmitting equally in every direction.

This can improve:

- Signal quality
- Range
- Throughput
- Connection stability

## Channel Bonding

Channel bonding combines multiple adjacent wireless channels into a wider channel.

Examples include:

- 20 MHz
- 40 MHz
- 80 MHz
- 160 MHz

Wider channels can increase throughput but also consume more spectrum and may increase interference in crowded environments.

## DFS

Dynamic Frequency Selection, or DFS, is used on certain 5 GHz channels.

Wireless devices using DFS channels may need to detect radar systems and move to another channel when required.

DFS helps wireless networks share spectrum with systems that have priority use of those frequencies.

## Wireless Roaming

In networks with multiple access points using the same SSID, clients can move between coverage areas.

The client may transition from one access point to another as signal conditions change.

Proper access point placement and configuration help provide smooth roaming.

## Wireless Security

Wireless networks require strong security because radio signals extend beyond physical network boundaries.

Modern wireless security commonly relies on WPA2 or WPA3.

## WPA2

WPA2 improved wireless security compared with older technologies such as WEP.

WPA2 commonly uses AES-based encryption.

WPA2 can be deployed using:

- Personal / pre-shared key authentication
- Enterprise authentication

## WPA3

WPA3 provides newer wireless security improvements and stronger protections compared with WPA2.

WPA3-Personal uses SAE, or Simultaneous Authentication of Equals, instead of the traditional WPA2 pre-shared-key exchange.

WPA3 is preferred when supported by the network and client devices.

## WEP

WEP is an older wireless security technology and is considered insecure.

It should not be used for modern wireless networks.

## Personal vs Enterprise Wireless Authentication

### Personal

Personal wireless networks typically use a shared password or passphrase.

This is common in:

- Homes
- Small offices
- Simple guest environments

### Enterprise

Enterprise wireless authentication can use centralized authentication systems such as RADIUS.

This provides individual authentication rather than relying on one shared password for every user.

Enterprise authentication is more appropriate for larger organizations.

## Guest Wireless Networks

Guest wireless networks should normally be separated from internal resources.

A guest network may provide:

- Internet access
- Isolation from employee devices
- Isolation from servers
- Restricted access to internal systems

Guest wireless networks are often placed into their own VLAN or subnet.

Example:

```text
Employee Wi-Fi
VLAN 10
192.168.10.0/24

Guest Wi-Fi
VLAN 30
192.168.30.0/24
```

Security controls can allow the guest VLAN to reach the internet while blocking access to internal networks.

## Rogue Access Points

A rogue access point is an unauthorized wireless access point connected to or operating within an organization's environment.

Rogue access points can create security risks by:

- Bypassing approved security controls
- Providing unauthorized network access
- Creating unknown wireless entry points

Wireless monitoring and proper network access controls can help identify rogue access points.

## Evil Twin

An evil twin is a malicious wireless access point designed to imitate a legitimate wireless network.

An attacker may use a similar or identical SSID in an attempt to convince users to connect.

Users should verify wireless networks and avoid connecting to suspicious or unexpected access points.

## Wireless Interference

Wireless problems are not always caused by configuration errors.

Interference can reduce signal quality and performance.

Possible causes include:

- Nearby wireless networks
- Overlapping channels
- Physical obstacles
- Bluetooth devices
- Microwave ovens
- Excessive access point power
- Poor access point placement
- Too many clients on one access point

## Signal Strength

Weak signal strength may cause:

- Slow speeds
- Packet loss
- Intermittent connections
- Frequent roaming
- Connection drops

Moving closer to the access point or improving access point placement can help determine whether signal strength is contributing to the problem.

## Wireless Site Surveys

A wireless site survey helps evaluate:

- Coverage
- Signal strength
- Interference
- Channel usage
- Access point placement
- Dead zones
- Capacity requirements

Heat maps can help visualize wireless coverage and identify areas that may need additional access points or configuration changes.

## Example Wireless Design

A small organization may use:

```text
Employee SSID: Corp-WiFi
VLAN: 10
Security: WPA3-Enterprise

Guest SSID: Guest-WiFi
VLAN: 30
Security: Separate guest authentication
Access: Internet only
```

The employee network can access approved internal resources.

The guest network can be isolated from internal systems while still providing internet connectivity.

## Wi-Fi Troubleshooting Process

When troubleshooting wireless connectivity, I use a structured process:

1. Verify Wi-Fi is enabled on the client.
2. Confirm the correct SSID is selected.
3. Check signal strength.
4. Check whether the client is receiving a valid IP address.
5. Verify the subnet mask and default gateway.
6. Check DNS configuration.
7. Test connectivity to the default gateway.
8. Check for interference or channel congestion.
9. Verify wireless authentication.
10. Check the wireless adapter and driver.
11. Compare the issue with another device if possible.
12. Check access point status.
13. Verify VLAN and network configuration.
14. Document the findings.

## Example Troubleshooting Scenario — Connected but No Internet

**Problem:** A client connects to Wi-Fi but cannot access the internet.

Possible checks include:

1. Confirm the client received a valid IP address.
2. Check whether the address is APIPA.
3. Verify the default gateway.
4. Test connectivity to the gateway.
5. Test connectivity to an external IP address.
6. Test DNS resolution.
7. Verify DHCP operation.
8. Check the wireless VLAN configuration.
9. Check firewall or access-control policies.

This helps determine whether the problem is wireless, DHCP, routing, DNS, or security related.

## Example Troubleshooting Scenario — Slow Wireless Performance

**Problem:** Users report slow Wi-Fi performance in one area.

Possible checks include:

1. Measure signal strength.
2. Check the number of connected clients.
3. Identify nearby wireless networks.
4. Check for overlapping channels.
5. Verify access point placement.
6. Review channel width.
7. Check for interference.
8. Compare 2.4 GHz and 5 GHz performance.
9. Review wired connectivity to the access point.
10. Document the results.

## Wireless Security Practices

Common wireless security practices include:

- Prefer WPA3 when supported
- Use WPA2 when WPA3 is unavailable
- Avoid WEP
- Use strong authentication
- Separate guest networks
- Use enterprise authentication where appropriate
- Monitor for rogue access points
- Disable unnecessary legacy protocols
- Use secure management interfaces
- Keep access point firmware updated
- Segment wireless networks appropriately
- Restrict management access

## Wireless Networking and Cybersecurity

Wireless networking connects directly with cybersecurity because Wi-Fi extends network access beyond physical Ethernet ports.

Security considerations include:

- Authentication
- Encryption
- Access control
- Network segmentation
- Rogue devices
- Unauthorized access
- Guest isolation
- Secure wireless management

Understanding wireless networking helps me better understand both network operations and the security controls used to protect modern networks.

## Key Takeaways

Some of the most important concepts I learned include:

- 2.4 GHz generally provides longer range but more interference.
- 5 GHz provides more channel options and higher performance in many environments.
- Channels 1, 6, and 11 are commonly used as non-overlapping 2.4 GHz channels.
- SSIDs identify wireless networks while BSSIDs identify specific access points or radios.
- Infrastructure mode uses access points.
- MIMO and MU-MIMO improve wireless performance.
- OFDMA improves efficiency in Wi-Fi 6.
- Beamforming can improve communication with wireless clients.
- WPA2 and WPA3 provide modern wireless security.
- Guest networks should be isolated from sensitive internal resources.
- Wireless troubleshooting requires checking radio conditions as well as IP addressing, DHCP, DNS, VLANs, routing, and security.

Wireless networking helped connect radio-frequency concepts, network infrastructure, troubleshooting, segmentation, and cybersecurity into one area of study.
