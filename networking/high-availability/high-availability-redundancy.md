# High Availability & Redundancy

This lab documents my study of high availability, redundancy, failover, and fault-tolerant network design from CompTIA Network+ coursework and practice.

The goal is to demonstrate my understanding of how networks reduce single points of failure, maintain connectivity during hardware or link failures, and use technologies such as HSRP, VRRP, STP, and LACP to improve resilience.

## Concepts Practiced

- High availability
- Redundancy
- Fault tolerance
- Single points of failure
- Failover
- Active-active designs
- Active-passive designs
- First Hop Redundancy Protocols
- HSRP
- VRRP
- Virtual IP addresses
- STP
- RSTP
- Redundant switch links
- LACP
- Link aggregation
- EtherChannel concepts
- Load balancing
- Redundant WAN connections
- Redundant network devices
- Redundant power
- Network convergence
- Health monitoring
- High-availability troubleshooting

# High Availability

High availability is the ability of a system or network to remain operational even when individual components fail.

A highly available network is designed so that the failure of one component does not automatically cause a complete outage.

Examples of components that may be made redundant include:

- Routers
- Switches
- Firewalls
- Network links
- WAN connections
- Power supplies
- Servers
- Internet service providers

# Redundancy

Redundancy means providing additional components or paths that can take over when the primary component fails.

Example:

```text
              ISP 1
                |
                v
             Router A
                |
                v
Users ------ Network
                ^
                |
             Router B
                |
                v
              ISP 2
```

If Router A or ISP 1 fails, Router B or ISP 2 may provide an alternate path.

# Single Point of Failure

A single point of failure is a component whose failure causes a larger service or network outage.

Example:

```text
Internet
   |
Router
   |
Switch
   |
Users
```

If the only router fails, every user may lose internet access.

Adding a second router reduces that single point of failure.

# Fault Tolerance

Fault tolerance is the ability of a system to continue operating even when part of the system fails.

Redundancy helps create fault tolerance.

Examples include:

- Multiple routers
- Multiple switches
- Multiple network links
- Multiple power supplies
- Multiple WAN providers

# Failover

Failover occurs when traffic or services move from a failed primary component to a backup component.

Example:

```text
Primary Router
     |
     X  Failure
     |
Backup Router
     |
     v
Traffic Continues
```

Failover may occur automatically depending on the technology being used.

# Active-Passive Design

In an active-passive design, one device actively handles traffic while another waits as a standby.

Example:

```text
Router A
ACTIVE
   |
   v
Network

Router B
STANDBY
```

If Router A fails, Router B can take over.

Advantages may include:

- Simpler failover behavior
- Predictable traffic paths
- Easier troubleshooting

The standby device may remain underused during normal operation.

# Active-Active Design

In an active-active design, multiple devices can handle traffic at the same time.

Example:

```text
        +---- Router A ----+
Users --+                 +---- Network
        +---- Router B ----+
```

Both devices may actively participate in forwarding traffic.

Advantages may include:

- Better resource utilization
- Load distribution
- Redundancy

Active-active environments may require more complex configuration and troubleshooting.

# First Hop Redundancy

End-user devices normally configure a default gateway.

If that gateway fails, users may lose access to remote networks even when another router is available.

First Hop Redundancy Protocols solve this problem by allowing multiple routers to share a **virtual IP address**.

Conceptually:

```text
              Virtual Gateway
               10.10.10.1
                    |
             +------+------+
             |             |
          Router A       Router B
         10.10.10.2     10.10.10.3
```

Clients configure:

`10.10.10.1`

as their default gateway.

The virtual address is maintained by the participating routers.

# HSRP

HSRP stands for **Hot Standby Router Protocol**.

HSRP is a Cisco first-hop redundancy protocol.

Multiple routers participate in an HSRP group and share a virtual IP address.

One router normally acts as the active router while another acts as the standby router.

Example:

```text
Clients
Default Gateway: 192.168.10.1
          |
          v
Virtual IP: 192.168.10.1
       /         \
      /           \
Router A         Router B
Active           Standby
```

If the active router fails, the standby router can take over the virtual gateway function.

# HSRP Virtual Group

HSRP routers operate as part of a virtual group.

The group provides:

- A virtual IP address
- A virtual MAC address
- Active and standby roles

Clients do not need to know which physical router is currently forwarding traffic.

They continue using the same virtual default gateway.

# HSRP Priority

HSRP can use priority values to determine which router should become active.

A higher priority is generally preferred.

Example:

```text
Router A Priority: 110
Router B Priority: 100
```

Router A would normally be preferred as the active router.

# HSRP Preemption

Preemption allows a router with a higher priority to regain the active role after it returns to service.

Without preemption, the current active router may continue forwarding even when the higher-priority router comes back online.

The exact behavior depends on configuration.

# VRRP

VRRP stands for **Virtual Router Redundancy Protocol**.

VRRP is a standards-based first-hop redundancy protocol.

Like HSRP, VRRP allows multiple routers to share a virtual IP address.

Conceptually:

```text
Clients
   |
Virtual Gateway
   |
+--+--+
|     |
R1    R2
```

If the primary forwarding router fails, another router can take over the virtual gateway.

# HSRP vs VRRP

A simplified comparison:

| Protocol | Type | Purpose |
|---|---|---|
| HSRP | Cisco-developed | Default gateway redundancy |
| VRRP | Standards-based | Default gateway redundancy |

Both reduce the risk of a default gateway becoming a single point of failure.

# Network Convergence

Convergence is the process of network devices recognizing a change and agreeing on updated forwarding information.

For example, when a route or link fails:

1. Devices detect the failure.
2. Routing or redundancy protocols respond.
3. Alternate paths are selected.
4. Network forwarding stabilizes.

Faster convergence generally means less service disruption.

# Redundant Switch Links

Adding multiple physical links between switches can improve redundancy.

However, simply connecting switches with multiple Layer 2 links can create switching loops.

Example:

```text
Switch A
  |   |
  |   |
Switch B
```

Without loop-prevention mechanisms, broadcast traffic could circulate indefinitely.

This is why technologies such as STP are important.

# STP

STP stands for **Spanning Tree Protocol**.

STP prevents Layer 2 loops by logically blocking redundant paths while keeping them available as backups.

Example:

```text
        Switch A
        /      \
       /        \
Switch B ------ Switch C
```

STP may block one redundant path.

If the active path fails, STP can recalculate the topology and activate another path.

# BPDU

STP-enabled switches exchange **Bridge Protocol Data Units**, or BPDUs.

BPDUs help switches:

- Discover the Layer 2 topology
- Elect a root bridge
- Determine preferred paths
- Identify redundant links

# Root Bridge

STP selects one switch as the root bridge.

Other switches calculate their best path toward the root.

The root bridge acts as the reference point for the spanning-tree topology.

# STP Port Roles

Depending on the STP version and topology, ports can perform different roles.

Common concepts include:

- Root port
- Designated port
- Alternate or blocked path

The goal is to create a loop-free Layer 2 topology.

# RSTP

RSTP stands for **Rapid Spanning Tree Protocol**.

RSTP is defined by IEEE 802.1w.

It improves convergence compared with traditional STP.

Faster convergence means the network can respond more quickly to certain topology changes.

# STP and Redundancy

STP allows physical redundancy without allowing all redundant Layer 2 paths to forward simultaneously.

Conceptually:

```text
Normal Operation:

Switch A ===== Switch B
    \          /
     \ BLOCKED
      Switch C

After Failure:

Switch A   X   Switch B
    \          /
     \ ACTIVE /
      Switch C
```

The backup path can become active when the preferred path fails.

# Link Aggregation

Link aggregation combines multiple physical Ethernet links into one logical connection.

Example:

```text
Switch A
 | | | |
 =======
 | | | |
Switch B
```

The group of links behaves as a logical link.

Benefits may include:

- Increased bandwidth
- Link redundancy
- Load distribution

# LACP

LACP stands for **Link Aggregation Control Protocol**.

LACP is defined by IEEE 802.1AX and is commonly associated with link aggregation.

LACP allows devices to negotiate and manage a bundle of physical links.

Example:

```text
Switch A
 |==== Link 1 ====|
 |==== Link 2 ====|  LACP Bundle
 |==== Link 3 ====|
Switch B
```

If one physical link fails, traffic can continue across the remaining links.

# EtherChannel

EtherChannel is a Cisco term for bundling multiple physical Ethernet links into one logical connection.

EtherChannel can use protocols such as LACP.

Benefits may include:

- Additional bandwidth
- Redundancy
- Simplified STP behavior

STP sees the aggregated links as one logical connection rather than multiple independent parallel links.

# LACP and STP

Without link aggregation, STP may block one of several parallel links to prevent a loop.

With LACP, the physical links can operate as one logical bundle.

Example:

```text
Without LACP:

Switch A
 | Link 1 - Forwarding
 | Link 2 - Blocked by STP
Switch B


With LACP:

Switch A
 |==== Logical Bundle ====|
Switch B
```

This allows bandwidth from multiple physical links to be used while maintaining redundancy.

# Link Failure in an LACP Bundle

Assume four links are bundled together:

```text
Link 1  ACTIVE
Link 2  ACTIVE
Link 3  ACTIVE
Link 4  ACTIVE
```

If Link 3 fails:

```text
Link 1  ACTIVE
Link 2  ACTIVE
Link 3  FAILED
Link 4  ACTIVE
```

The logical connection can remain operational using the remaining links.

Available bandwidth may decrease, but connectivity can continue.

# Load Balancing

Load balancing distributes traffic across multiple resources.

In networking, load balancing may occur across:

- Multiple servers
- Multiple links
- Multiple WAN connections
- Multiple network paths

Example:

```text
          Load Balancer
          /     |     \
         /      |      \
    Server A Server B Server C
```

The goal is to avoid placing all traffic on a single resource.

# Layer 4 Load Balancing

Layer 4 load balancing can make decisions using transport-layer information such as:

- Source IP
- Destination IP
- TCP port
- UDP port

# Layer 7 Load Balancing

Layer 7 load balancing can make application-aware decisions.

Examples may include:

- HTTP hostnames
- URLs
- Application requests

Layer 7 load balancing provides more application awareness than Layer 4 load balancing.

# Redundant WAN Links

Organizations may use more than one WAN or internet connection.

Example:

```text
             ISP 1
               |
               |
Corporate Network
               |
               |
             ISP 2
```

If one ISP fails, the organization may route traffic through the other connection.

This can improve internet and WAN availability.

# Dual ISP Design

A dual-ISP design can reduce dependence on a single internet provider.

Possible considerations include:

- Routing
- Failover
- BGP
- NAT
- Firewall policies
- DNS
- Bandwidth
- ISP diversity

Using two connections from the same physical carrier path may not provide true physical redundancy.

# Path Diversity

Path diversity means using physically different routes when possible.

For example, two internet connections entering a building through the same underground conduit may both fail if that conduit is damaged.

True redundancy considers physical paths as well as logical network design.

# Redundant Network Devices

Critical network functions may use multiple devices.

Examples include:

- Two routers
- Two core switches
- Two firewalls
- Multiple wireless controllers
- Multiple load balancers

If one device fails, another can continue providing service.

# Redundant Power Supplies

Enterprise network equipment may include multiple power supplies.

Example:

```text
Switch
├── Power Supply A
└── Power Supply B
```

If one supply fails, the device can continue running from the remaining supply.

For greater redundancy, the power supplies may connect to separate power sources.

# UPS

A UPS, or Uninterruptible Power Supply, provides temporary battery power during an electrical outage.

A UPS can:

- Keep equipment operating during short outages
- Protect against some power disturbances
- Provide time for graceful shutdown
- Support network availability

# Generator

A generator can provide longer-term backup power during extended utility outages.

A common design may use:

```text
Utility Power
     |
     v
UPS
     |
     v
Network Equipment
     ^
     |
Generator
```

The UPS provides immediate power while the generator starts.

# Device Clustering

Some network or application systems operate in clusters.

A cluster may allow multiple systems to work together to provide:

- Redundancy
- Load distribution
- Failover
- Higher availability

Cluster behavior depends on the specific platform.

# Heartbeats

High-availability systems may use heartbeat messages to verify that peer devices are still operational.

Conceptually:

```text
Device A ---- heartbeat ---- Device B
Device A <--- heartbeat ---- Device B
```

If heartbeat messages stop, the surviving device may determine that failover is required.

# Health Checks

Load balancers and high-availability systems can perform health checks.

Examples include:

- Ping
- TCP connection test
- HTTP request
- Application-specific check

A failed health check can cause a system to be removed from active service.

# Redundancy Does Not Mean Backup

Redundancy and backup are related to availability but solve different problems.

Redundancy helps keep services operating when a component fails.

Backups help restore lost or damaged data.

Example:

```text
Redundant Server:
Keeps service available after hardware failure

Backup:
Restores data after deletion or corruption
```

A system can have redundancy and still require backups.

# High Availability and Disaster Recovery

High availability focuses on reducing downtime during normal failures.

Disaster recovery focuses on restoring systems after a larger disruption.

Both contribute to organizational resilience.

# Example Design — Redundant Default Gateway

```text
Client Network
192.168.10.0/24
       |
       |
Virtual Gateway
192.168.10.1
     /     \
    /       \
Router A   Router B
Active     Standby
```

Clients continue using:

`192.168.10.1`

even if the physical router handling the virtual gateway changes.

# Example Design — Redundant Core Switching

```text
          Core Switch A
          /           \
         /             \
Access Switch       Access Switch
         \             /
          \           /
          Core Switch B
```

Multiple core devices and links reduce dependence on a single switch.

Technologies such as STP and link aggregation must be configured appropriately to prevent loops and manage redundant paths.

# Example Troubleshooting Scenario — Default Gateway Failure

**Problem:** Users lose access to remote networks after Router A fails.

Possible checks:

1. Confirm Router A is unavailable.
2. Verify Router B is operational.
3. Check the first-hop redundancy protocol.
4. Verify the virtual IP address.
5. Check active and standby roles.
6. Verify HSRP or VRRP communication.
7. Check whether failover occurred.
8. Test connectivity through Router B.
9. Review relevant logs.
10. Document the failure.

If both routers are operational but the virtual gateway does not move correctly, the FHRP configuration may be the issue.

# Example Troubleshooting Scenario — Redundant Link Not Working

**Problem:** One switch uplink fails and the backup link does not begin forwarding traffic.

Possible checks:

1. Verify physical link status.
2. Review STP topology.
3. Check which switch is the root bridge.
4. Review port roles.
5. Look for BPDU-related issues.
6. Verify VLANs are allowed on the backup link.
7. Check interface configuration.
8. Review logs.
9. Test after correcting the issue.
10. Document the results.

# Example Troubleshooting Scenario — LACP Bundle Degraded

**Problem:** A four-link LACP bundle is operating with only three active links.

Possible checks:

1. Identify the failed physical interface.
2. Check cable and transceiver status.
3. Verify speed and duplex settings.
4. Check LACP configuration on both devices.
5. Confirm all links belong to the correct bundle.
6. Check interface errors.
7. Replace or repair the failed link.
8. Verify the link rejoins the bundle.
9. Confirm total bandwidth is restored.
10. Document the change.

# Example Troubleshooting Scenario — ISP Failure

**Problem:** The primary internet connection fails but users do not automatically move to the backup ISP.

Possible checks:

1. Confirm the primary ISP is unavailable.
2. Verify the backup circuit is operational.
3. Review routing configuration.
4. Check route priorities or metrics.
5. Verify health monitoring.
6. Check firewall and NAT policies.
7. Test outbound connectivity through the backup path.
8. Review logs.
9. Confirm automatic failover behavior.
10. Document the findings.

# Availability Monitoring

High availability depends on detecting failures.

Monitoring may include:

- SNMP
- Syslog
- Interface monitoring
- Routing protocol status
- Device health
- Power supply status
- WAN availability
- CPU and memory utilization
- Heartbeat status

Monitoring helps administrators identify when a redundant component has failed even if users have not experienced an outage yet.

# Hidden Redundancy Failure

A redundant system can appear healthy even after one component has failed.

Example:

```text
Normal:
Primary Link + Backup Link

After Failure:
Primary Link only
```

Users may still have connectivity, but the network has lost its redundancy.

If the remaining link fails, an outage will occur.

Monitoring is important for identifying these degraded states.

# High Availability Troubleshooting Process

When troubleshooting redundancy or failover, I use a structured process:

1. Identify the failed component.
2. Determine whether a backup exists.
3. Verify the backup component is operational.
4. Check physical connectivity.
5. Review protocol status.
6. Verify virtual IP or gateway configuration.
7. Check routing tables.
8. Review STP or LACP status where applicable.
9. Review monitoring and log information.
10. Test failover behavior.
11. Confirm normal service has been restored.
12. Verify redundancy has also been restored.
13. Document the findings and changes.

# Key Takeaways

Some of the most important concepts I learned include:

- High availability reduces service disruption when components fail.
- Redundancy removes or reduces single points of failure.
- Failover moves service or traffic to a backup component.
- Active-passive designs use a standby resource.
- Active-active designs allow multiple resources to operate simultaneously.
- HSRP and VRRP provide default gateway redundancy using virtual IP addresses.
- STP prevents Layer 2 loops while allowing redundant switch paths.
- RSTP improves spanning-tree convergence.
- LACP combines multiple links into a logical connection.
- Link aggregation can provide both additional bandwidth and redundancy.
- Redundant WAN connections can reduce dependence on a single ISP.
- Physical path diversity is important when designing true redundancy.
- Redundant power supplies, UPS systems, and generators improve infrastructure availability.
- Monitoring is necessary to identify failed redundant components before another failure causes an outage.
- Restoring service is not enough; redundancy should also be restored after a failure.

Understanding high availability and redundancy helped me connect routing, switching, STP, LACP, first-hop redundancy, monitoring, WAN connectivity, and physical infrastructure into a more resilient network design.
