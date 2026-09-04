# VLANs & Network Segmentation

This lab documents my VLAN and network segmentation practice from CompTIA Network+ coursework and study.

The goal is to demonstrate my understanding of how VLANs separate network traffic, how access and trunk ports work, how devices in different VLANs communicate, and how segmentation can improve network organization, performance, and security.

## Concepts Practiced

- VLANs
- Broadcast domains
- Network segmentation
- Access ports
- Trunk ports
- IEEE 802.1Q
- VLAN tagging
- Native VLANs
- Inter-VLAN routing
- Layer 2 and Layer 3 segmentation
- Subnets and VLANs
- Guest networks
- Voice VLANs
- Management VLANs
- VLAN troubleshooting
- VLAN security concepts

## What Is a VLAN?

A VLAN, or Virtual Local Area Network, logically separates devices into different Layer 2 broadcast domains.

Devices can be connected to the same physical switching infrastructure while still belonging to separate logical networks.

For example:

- VLAN 10 — Employees
- VLAN 20 — Servers
- VLAN 30 — Guest Wi-Fi
- VLAN 40 — Voice
- VLAN 99 — Network Management

Devices in one VLAN do not normally communicate directly with devices in another VLAN without Layer 3 routing.

## Why Use VLANs?

VLANs can provide several benefits:

- Network segmentation
- Smaller broadcast domains
- Improved organization
- Better traffic management
- Separation of departments or device types
- Improved security
- Easier application of access-control policies

Instead of placing every device into one large network, VLANs allow administrators to create smaller logical networks.

## Broadcast Domains

A broadcast domain is the group of devices that receive a Layer 2 broadcast.

Each VLAN represents its own broadcast domain.

For example:

```text
VLAN 10
PC-A
PC-B
PC-C

VLAN 20
Server-A
Server-B
```

A broadcast sent by a device in VLAN 10 stays within VLAN 10 unless a Layer 3 device processes and routes the traffic.

## VLANs and Subnets

VLANs and IP subnets are different concepts, but they are commonly designed together.

A VLAN provides Layer 2 segmentation.

A subnet provides Layer 3 IP segmentation.

Example:

| VLAN | Purpose | Subnet |
|---|---|---|
| VLAN 10 | Employees | 192.168.10.0/24 |
| VLAN 20 | Servers | 192.168.20.0/24 |
| VLAN 30 | Guest | 192.168.30.0/24 |
| VLAN 40 | Voice | 192.168.40.0/24 |

Using a separate subnet for each VLAN makes routing and security policies easier to manage.

## Access Ports

An access port normally belongs to one VLAN and connects to an endpoint device.

Examples include:

- Desktop computers
- Printers
- Cameras
- IP phones
- Servers

A workstation connected to an access port assigned to VLAN 10 becomes part of VLAN 10.

The endpoint normally does not need to understand VLAN tagging.

## Trunk Ports

A trunk port carries traffic for multiple VLANs over one physical link.

Trunks are commonly used between:

- Switches
- Switches and routers
- Switches and Layer 3 switches
- Switches and some wireless access points

Without trunking, separate physical connections could be required for each VLAN.

## IEEE 802.1Q

IEEE 802.1Q is the standard commonly used for VLAN tagging on Ethernet trunk links.

An 802.1Q tag identifies the VLAN associated with a frame as it travels across a trunk.

Example:

```text
Switch 1                   Switch 2
VLAN 10  ───────┐       ┌────── VLAN 10
VLAN 20  ───────┼─ TRUNK ┼────── VLAN 20
VLAN 30  ───────┘       └────── VLAN 30
```

One trunk link can carry traffic for multiple VLANs.

## Native VLAN

On an 802.1Q trunk, the native VLAN is traditionally associated with untagged traffic.

Native VLAN configuration should match on both sides of a trunk.

A mismatch can cause connectivity problems and may create security concerns.

## Inter-VLAN Routing

Devices in different VLANs require Layer 3 routing to communicate.

This can be performed by:

- A router
- A Layer 3 switch
- A firewall or other Layer 3 device

For example:

```text
PC-A
VLAN 10
192.168.10.25
     |
     v
Layer 3 Device
     |
     v
Server-A
VLAN 20
192.168.20.50
```

The Layer 3 device routes traffic between the two VLANs.

Security rules can also determine whether that communication should be allowed.

## Router-on-a-Stick

Router-on-a-stick is a design where one physical router interface handles traffic for multiple VLANs through subinterfaces.

A trunk connects the switch to the router.

The router uses separate logical subinterfaces for different VLANs.

Conceptual example:

```text
Router
   |
   | 802.1Q trunk
   |
Switch
├── VLAN 10
├── VLAN 20
└── VLAN 30
```

This allows inter-VLAN routing without requiring a separate physical router interface for every VLAN.

## Layer 3 Switching

A Layer 3 switch can perform both switching and routing.

Instead of sending VLAN traffic to an external router, a Layer 3 switch can route between VLANs using switched virtual interfaces.

This is common in enterprise networks because it can provide efficient inter-VLAN routing.

## Guest Network Segmentation

Guest networks are commonly isolated from internal organizational resources.

For example:

```text
Internal Network
VLAN 10
192.168.10.0/24

Guest Network
VLAN 30
192.168.30.0/24
```

The guest VLAN may be allowed to reach the internet while being blocked from accessing:

- Internal servers
- Employee workstations
- Management interfaces
- Printers
- Other sensitive resources

This demonstrates how segmentation can support security.

## Voice VLANs

IP phones may be placed into a dedicated voice VLAN.

Benefits can include:

- Separating voice and user traffic
- Applying QoS policies
- Easier troubleshooting
- Improved organization
- Applying voice-specific security policies

A workstation and IP phone may sometimes share the same physical switch connection while their traffic remains logically separated.

## Management VLAN

Network infrastructure management interfaces may be placed into a dedicated management VLAN.

Examples include management access for:

- Switches
- Routers
- Wireless access points
- Firewalls

Management networks should generally be restricted to authorized administrators and management systems.

## VLAN Security

VLANs help create logical separation, but VLANs alone should not be treated as complete security controls.

Additional protections may include:

- ACLs
- Firewalls
- Authentication
- Port security
- Secure management protocols
- Proper trunk configuration
- Disabling unused ports
- Limiting allowed VLANs on trunks

Segmentation is most effective when combined with access-control policies.

## VLAN Hopping

VLAN hopping refers to techniques that attempt to gain unauthorized access to traffic from another VLAN.

Two concepts covered in networking and security studies include:

### Switch Spoofing

An attacker attempts to make a device appear to be a switch and negotiate a trunk connection.

Mitigation can include manually configuring user-facing ports as access ports instead of allowing unnecessary trunk negotiation.

### Double Tagging

A specially crafted Ethernet frame contains multiple VLAN tags.

The goal is to cause traffic to cross VLAN boundaries under certain network configurations.

Proper native VLAN configuration and network design help reduce this risk.

## Example Segmentation Design

Assume a small organization has:

- Employees
- Servers
- Guests
- IP phones
- Network administrators

A possible design could be:

| VLAN | Name | Subnet |
|---|---|---|
| 10 | Employees | 10.10.10.0/24 |
| 20 | Servers | 10.10.20.0/24 |
| 30 | Guests | 10.10.30.0/24 |
| 40 | Voice | 10.10.40.0/24 |
| 99 | Management | 10.10.99.0/24 |

Traffic could then be controlled between VLANs based on business requirements.

For example:

- Employees → Servers: Allowed as required
- Guests → Internet: Allowed
- Guests → Internal VLANs: Blocked
- Management → Network devices: Allowed
- General users → Management VLAN: Blocked

## VLAN Troubleshooting Process

When troubleshooting VLAN connectivity, I use a structured process:

1. Verify the endpoint IP address and subnet.
2. Verify the default gateway.
3. Confirm the device is connected to the expected switch port.
4. Check the VLAN assigned to the access port.
5. Verify the VLAN exists on the switch.
6. Check trunk links between switches.
7. Confirm the required VLAN is allowed across the trunk.
8. Check native VLAN configuration.
9. Verify inter-VLAN routing if communication crosses VLANs.
10. Check ACL or firewall rules.
11. Test connectivity with tools such as `ping`.
12. Document the results.

## Example Troubleshooting Scenario

**Problem:** A workstation in VLAN 20 cannot reach its default gateway.

Possible checks include:

1. Verify the workstation IP address.
2. Verify the subnet mask.
3. Confirm the configured default gateway.
4. Check the physical switch connection.
5. Verify the switch port belongs to VLAN 20.
6. Verify VLAN 20 exists.
7. Confirm the Layer 3 gateway interface for VLAN 20 is available.
8. Check for trunking problems if the gateway is reached through another switch.

This helps separate host configuration issues from switching, VLAN, trunking, and routing problems.

## Segmentation and Cybersecurity

Network segmentation is also an important cybersecurity concept.

Segmentation can help:

- Limit unnecessary communication
- Reduce exposure of sensitive systems
- Restrict guest access
- Separate management traffic
- Control access between departments
- Reduce the potential impact of a compromised device
- Support least-privilege network design

This is one area where my Network+ knowledge connects directly with the security concepts I am continuing to study through Security+.

## Key Takeaways

Some of the most important concepts I learned include:

- VLANs create separate Layer 2 broadcast domains.
- VLANs are commonly paired with separate IP subnets.
- Access ports normally carry one VLAN.
- Trunk ports carry multiple VLANs.
- IEEE 802.1Q provides VLAN tagging.
- Inter-VLAN communication requires Layer 3 routing.
- Segmentation can improve organization, performance, and security.
- Guest, voice, server, and management networks can be logically separated.
- VLAN security requires proper configuration and additional access controls.
- Troubleshooting VLANs requires checking addressing, port assignments, trunks, routing, and security policies.

Understanding VLANs helped me connect switching, subnetting, routing, and cybersecurity into a more complete network design model.
