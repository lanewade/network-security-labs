# Routing & Switching Fundamentals

This lab documents my routing and switching practice from CompTIA Network+ coursework and study.

The goal is to demonstrate my understanding of how switches move traffic within a LAN, how routers move traffic between networks, how routing decisions are made, and how redundancy and loop prevention are handled in modern networks.

## Concepts Practiced

- Layer 2 switching
- Layer 3 routing
- MAC address tables
- ARP
- Default gateways
- Routing tables
- Static and dynamic routing
- Longest prefix match
- Default routes
- RIP
- OSPF
- Route convergence
- VLANs
- Trunking
- Spanning Tree Protocol (STP)
- BPDUs
- Link aggregation
- LACP
- First-hop redundancy
- HSRP
- Network troubleshooting

## Switching Fundamentals

Switches primarily operate at Layer 2 of the OSI model and use MAC addresses to forward Ethernet frames within a local network.

A switch learns which devices are connected to its ports by examining the source MAC addresses of incoming frames.

The learned information is stored in a MAC address table, sometimes called a CAM table.

### Basic Switching Process

1. A frame enters a switch port.
2. The switch examines the source MAC address.
3. The switch learns which port is associated with that MAC address.
4. The switch checks the destination MAC address.
5. If the destination is known, the frame is forwarded to the correct port.
6. If the destination is unknown, the switch floods the frame out appropriate ports except the port it arrived on.

## ARP

ARP is used in IPv4 networks to discover the MAC address associated with a known IP address on the local network.

A simplified ARP process:

1. A device determines that the destination is on the local subnet.
2. It checks its ARP cache.
3. If the MAC address is unknown, it sends an ARP request.
4. The device that owns the requested IP responds with its MAC address.
5. The information is stored temporarily in the ARP cache.

ARP is important because Ethernet communication ultimately uses MAC addresses on the local network.

## Routing Fundamentals

Routers primarily operate at Layer 3 and use IP addresses to move packets between different networks.

When a device needs to communicate with a destination outside its local subnet, it normally sends the traffic to its default gateway.

The router then checks its routing table to determine where the packet should go next.

## Routing Table

A routing table contains information about known networks and how to reach them.

Routes may come from:

- Directly connected networks
- Static routes
- Dynamic routing protocols
- A default route

A routing table may include:

- Destination network
- Prefix length
- Next-hop address
- Exit interface
- Route source
- Administrative information or metrics

## Longest Prefix Match

When multiple routes could reach the same destination, routers prefer the route with the most specific prefix.

For example:

- `10.0.0.0/8`
- `10.1.0.0/16`
- `10.1.5.0/24`

For a destination of:

`10.1.5.25`

The `/24` route is preferred because it is the most specific match.

This is known as **longest prefix match**.

## Default Route

A default route is used when no more specific route exists.

IPv4 default route:

`0.0.0.0/0`

IPv6 default route:

`::/0`

The default route is often described as the route of last resort.

## Static Routing

A static route is manually configured by an administrator.

Advantages include:

- Predictable routing behavior
- Low protocol overhead
- Simple configuration in small networks

Disadvantages include:

- Manual maintenance
- Poor scalability
- No automatic adaptation when topology changes

## Dynamic Routing

Dynamic routing protocols allow routers to exchange network information and update their routing tables automatically.

Dynamic routing is useful in larger networks where manually maintaining every route would be inefficient.

## RIP

Routing Information Protocol (RIP) is a distance-vector routing protocol.

RIP primarily uses **hop count** as its routing metric.

Important characteristics:

- Distance-vector protocol
- Maximum usable hop count of 15
- 16 hops represents an unreachable network
- Selects routes based primarily on lowest hop count
- Generally suited to smaller or simpler networks
- Slower convergence than more modern routing protocols

One limitation of RIP is that a route with fewer hops may be selected even when another path would otherwise be more efficient.

## OSPF

Open Shortest Path First (OSPF) is a link-state routing protocol.

OSPF builds a view of the network topology and calculates efficient paths through the network.

Important concepts include:

- Link-state routing
- Cost-based metric
- Areas
- Area 0 backbone
- Faster convergence than RIP
- Scalable design for larger networks

### Area 0

OSPF uses **Area 0** as the backbone area.

Other OSPF areas normally connect through Area 0 so routing information can be exchanged properly across the OSPF environment.

## Convergence

Convergence is the process of routers reaching agreement about the current network topology after a change occurs.

For example, if a network link fails:

1. The failure is detected.
2. Routing information is updated.
3. Routers calculate new paths.
4. Routing tables are updated.
5. Traffic begins using the new path.

Faster convergence generally means less disruption after a topology change.

## VLANs

A VLAN logically separates devices into different Layer 2 broadcast domains.

Devices can be grouped into separate networks even when they are connected to the same physical switch infrastructure.

Benefits include:

- Network segmentation
- Reduced broadcast domains
- Improved organization
- Improved security
- Easier traffic management

Devices in different VLANs normally require a Layer 3 device to communicate with each other.

## Access Ports

An access port normally carries traffic for a single VLAN.

A typical end-user device such as a workstation connects to an access port.

## Trunk Ports

A trunk carries traffic for multiple VLANs between network devices.

Trunks are commonly used between:

- Switches
- Switches and routers
- Switches and Layer 3 switches

IEEE 802.1Q tagging identifies which VLAN a frame belongs to while traveling across a trunk.

## Spanning Tree Protocol

Spanning Tree Protocol (STP) helps prevent Layer 2 switching loops.

Redundant switch links are useful for availability, but unmanaged redundant paths can create loops.

Possible effects of Layer 2 loops include:

- Broadcast storms
- Duplicate frames
- MAC address table instability
- Severe network performance problems

STP creates a loop-free logical topology by placing some redundant links into a blocking state.

## BPDUs

STP switches exchange **Bridge Protocol Data Units (BPDUs)**.

BPDUs help switches:

- Elect a root bridge
- Compare network paths
- Determine forwarding and blocking ports
- Detect topology changes

## Link Aggregation

Link aggregation combines multiple physical network links into one logical connection.

Benefits can include:

- Increased bandwidth
- Redundancy
- Improved availability

## LACP

Link Aggregation Control Protocol (LACP) is used to negotiate and manage aggregated Ethernet links.

LACP is associated with IEEE 802.3ad and later 802.1AX standards.

Instead of relying on a single physical link, multiple links can operate together as one logical connection.

## First-Hop Redundancy

First-hop redundancy protocols provide gateway redundancy for hosts on a LAN.

Instead of depending on a single physical router as the default gateway, multiple routers can participate in a virtual gateway configuration.

## HSRP

Hot Standby Router Protocol (HSRP) provides gateway redundancy.

Multiple routers share a virtual IP address.

Hosts use the virtual IP address as their default gateway rather than depending directly on one physical router.

If the active router fails, another router can take over the gateway role.

This helps reduce disruption caused by a single router failure.

## Example Routing Decision

Assume a router has these routes:

`192.168.0.0/16`

`192.168.10.0/24`

`192.168.10.128/25`

The destination is:

`192.168.10.150`

All three routes technically match the destination.

The router selects:

`192.168.10.128/25`

because `/25` is the longest and most specific prefix.

## Example Switching Scenario

A workstation sends a frame to another device on the same VLAN.

The switch checks its MAC address table.

If the destination MAC address is already known, the switch forwards the frame only through the port associated with that destination.

If the destination MAC address is unknown, the switch floods the frame within the VLAN until the destination is discovered.

## Basic Routing Troubleshooting Process

When troubleshooting routing problems, I work through a structured process:

1. Check the device IP address.
2. Verify the subnet mask or prefix.
3. Verify the default gateway.
4. Test local connectivity.
5. Test connectivity to the gateway.
6. Review routing information.
7. Verify the destination network is known.
8. Check for VLAN or segmentation issues.
9. Use tools such as `ping` and `tracert` / `traceroute`.
10. Document the results.

## Basic Switching Troubleshooting Process

When troubleshooting switching or LAN connectivity:

1. Verify the physical connection.
2. Check link status.
3. Verify the device is connected to the correct switch port.
4. Check VLAN membership.
5. Verify IP addressing.
6. Check for MAC address learning.
7. Verify trunking when multiple VLANs are involved.
8. Check for STP-related issues.
9. Test connectivity.
10. Document findings.

## Key Takeaways

Routing and switching work together to move traffic through a network.

Switching focuses primarily on communication within local Layer 2 networks, while routing allows communication between different IP networks.

Some of the most important concepts I learned include:

- Switches learn and forward traffic using MAC addresses.
- Routers make forwarding decisions using routing tables and IP prefixes.
- Longest prefix match determines the most specific route.
- Dynamic routing protocols exchange network information automatically.
- RIP uses hop count.
- OSPF uses a link-state design and Area 0 as its backbone.
- VLANs provide logical network segmentation.
- STP prevents Layer 2 switching loops.
- LACP provides link aggregation.
- HSRP provides gateway redundancy.

Understanding these concepts helped connect network design, redundancy, troubleshooting, and traffic flow into a more complete picture of how modern networks operate.
