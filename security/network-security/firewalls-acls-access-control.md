# Firewalls, ACLs & Access Control

This lab documents my study and practice with firewalls, access control lists (ACLs), traffic filtering, and network access control from CompTIA Network+ and Security+ coursework.

The goal is to demonstrate my understanding of how network traffic can be evaluated, permitted, denied, and restricted according to security requirements and the principle of least privilege.

## Concepts Practiced

- Firewalls
- Stateful and stateless filtering
- Access Control Lists (ACLs)
- Allow and deny rules
- Source and destination addresses
- Source and destination ports
- Protocol-based filtering
- Rule order
- Implicit deny
- `deny any any`
- Ingress and egress filtering
- Network segmentation
- Least privilege
- Default-deny security
- Authentication and authorization
- Role-Based Access Control (RBAC)
- Network Access Control (NAC)
- Zero Trust concepts
- Firewall and ACL troubleshooting

## What Is a Firewall?

A firewall controls network traffic between systems or networks based on configured security rules.

A firewall can evaluate information such as:

- Source IP address
- Destination IP address
- Protocol
- Source port
- Destination port
- Connection state
- Application or service

Firewalls are commonly placed between networks with different levels of trust.

Example:

```text
Internet
   |
   v
Firewall
   |
   v
Internal Network
```

The firewall determines which traffic is allowed to enter or leave the protected network.

## Stateful Firewalls

A stateful firewall tracks active network connections.

For example, if an internal client creates a legitimate outbound HTTPS connection, the firewall can recognize the return traffic as part of that established session.

This allows the firewall to make decisions based on the state of a connection rather than evaluating each packet independently.

## Stateless Filtering

Stateless filtering evaluates individual packets using configured rules without maintaining awareness of the overall connection state.

Decisions may be based on:

- IP addresses
- Ports
- Protocols
- Traffic direction

Stateless filtering can be efficient, but it does not provide the same connection awareness as a stateful firewall.

## Access Control Lists

An Access Control List, or ACL, is a set of rules used to permit or deny traffic.

ACL rules commonly evaluate:

- Source
- Destination
- Protocol
- Port or service

Conceptual example:

```text
ALLOW TCP from Internal_Network to Web_Server port 443
ALLOW UDP from Internal_Network to DNS_Server port 53
DENY  ANY from Guest_Network to Internal_Network
DENY  ANY from ANY to ANY
```

The exact syntax varies between networking platforms, but the underlying logic is similar.

## Rule Order

ACL and firewall rule order is important.

Many rule sets are processed from the top down.

When traffic matches a rule, that rule's action may be applied and processing stops.

Example:

```text
1. ALLOW TCP port 443
2. DENY ANY ANY
```

HTTPS traffic is allowed because it matches rule 1 before reaching the deny rule.

If the order were reversed:

```text
1. DENY ANY ANY
2. ALLOW TCP port 443
```

The traffic would be denied before the firewall ever reached the HTTPS allow rule.

This is why rule placement matters.

## `deny any any`

A rule such as:

`deny any any`

means traffic matching any source and any destination is denied.

This type of rule is commonly placed at the end of a rule set so that traffic that was not specifically permitted earlier is blocked.

Conceptually:

```text
ALLOW required traffic
ALLOW required traffic
ALLOW required traffic
DENY ANY ANY
```

This supports a **default-deny** approach.

Only traffic with an explicit business or technical requirement is allowed.

## Example — Missing Web Access Rule

Assume a firewall contains only these allow rules:

```text
ALLOW TCP port 21
ALLOW TCP port 25
ALLOW TCP port 110
DENY ANY ANY
```

These ports correspond to services such as:

- 21 — FTP
- 25 — SMTP
- 110 — POP3

A user then tries to browse normal websites.

HTTP and HTTPS use:

- TCP 80 — HTTP
- TCP 443 — HTTPS

Because ports 80 and 443 were never allowed, the final `deny any any` rule blocks the web traffic.

To permit normal web browsing, appropriate HTTP and HTTPS rules would need to be added before the final deny rule.

Example:

```text
ALLOW TCP port 80
ALLOW TCP port 443
DENY ANY ANY
```

This example helped me understand that a deny-all rule is only effective when all necessary legitimate traffic has already been explicitly permitted.

## Implicit Deny

Many ACL and firewall implementations have an implicit deny behavior.

This means traffic that does not match an allow rule may be denied even when a visible `deny any any` rule is not shown.

A manually configured final deny rule can make the policy easier to understand and document.

The exact behavior depends on the platform and configuration.

## Default-Allow vs Default-Deny

### Default-Allow

Traffic is permitted unless a rule specifically blocks it.

This may be easier to manage initially but can expose services that were never intentionally approved.

### Default-Deny

Traffic is denied unless a rule specifically permits it.

This approach generally provides stronger security because access must be intentionally granted.

Default-deny aligns closely with the principle of least privilege.

## Least Privilege

Least privilege means users, systems, and applications should receive only the access necessary to perform their required functions.

For network traffic, this can mean allowing:

- Only required protocols
- Only required ports
- Only approved source systems
- Only approved destinations

Instead of allowing:

```text
ANY source
ANY destination
ANY service
```

a more restrictive policy may allow only a specific application flow.

## Source and Destination Filtering

Firewall and ACL rules can restrict traffic based on where it comes from and where it is going.

Example:

```text
Guest Network
10.10.30.0/24
        |
        X
        |
Server Network
10.10.20.0/24
```

A policy could prevent guest users from directly accessing internal servers.

At the same time, the guest network could still be permitted to access the internet.

## Port-Based Filtering

Ports identify many common network services.

Examples include:

| Port | Protocol | Service |
|---|---|---|
| 22 | TCP | SSH |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 80 | TCP | HTTP |
| 110 | TCP | POP3 |
| 443 | TCP | HTTPS |
| 3389 | TCP/UDP | RDP |

A firewall can use this information to restrict access to particular services.

For example, RDP on port 3389 may be allowed only from an approved management network rather than from every network.

## Ingress Filtering

Ingress filtering controls traffic entering an interface or network.

Examples include:

- Blocking unsolicited internet traffic
- Restricting guest traffic entering an internal network
- Blocking unauthorized management connections

## Egress Filtering

Egress filtering controls traffic leaving a network.

This can help restrict:

- Unauthorized outbound connections
- Traffic to prohibited destinations
- Unexpected application traffic
- Some forms of data exfiltration

Security controls are therefore not limited to incoming traffic.

## Firewall Zones

Firewalls can separate networks into security zones.

Example:

```text
Internet
   |
   v
[ External Zone ]
   |
Firewall
   |
   +------ DMZ
   |
   +------ Internal Network
```

Different rules can be applied depending on which zones the traffic moves between.

## DMZ

A DMZ is a network segment used for systems that need to provide services to less-trusted networks while remaining separated from the internal network.

Examples might include:

- Public web servers
- Public-facing application systems
- Other externally accessible services

A firewall can tightly control traffic between:

- Internet and DMZ
- DMZ and internal network
- Internal network and internet

This reduces the need to expose internal systems directly.

## Network Segmentation and Firewalls

VLANs create logical network separation, but firewalls and ACLs determine what traffic is allowed to cross between those segments.

Example:

```text
VLAN 10 - Employees
VLAN 20 - Servers
VLAN 30 - Guests
VLAN 99 - Management
```

Possible policies:

```text
Employees -> Approved Servers     ALLOW
Guests -> Internet                ALLOW
Guests -> Internal Networks       DENY
Management -> Network Devices     ALLOW
Users -> Management Network       DENY
```

This combines network segmentation with access control.

## Authentication vs Authorization

Authentication answers:

**Who are you?**

Examples include:

- Passwords
- MFA
- Certificates
- Smart cards

Authorization answers:

**What are you allowed to do?**

A user may successfully authenticate but still be restricted from certain systems or resources.

## Role-Based Access Control

Role-Based Access Control, or RBAC, grants permissions according to a user's assigned role.

Example:

```text
Help Desk
- Reset passwords
- Unlock user accounts

Network Administrator
- Configure switches
- Configure routers
- Modify network policies

Security Administrator
- Review security events
- Manage security controls
```

RBAC makes access easier to manage than assigning every permission individually.

## Network Access Control

Network Access Control, or NAC, can evaluate devices or users before allowing network access.

A NAC solution may check characteristics such as:

- Authentication status
- Device identity
- Security posture
- Compliance status
- Network location

A device that does not meet requirements may be:

- Denied access
- Placed into a restricted network
- Sent to a remediation environment

## Zero Trust

Zero Trust is based on the idea that access should not automatically be trusted simply because a user or device is located inside a network.

Common principles include:

- Verify explicitly
- Apply least privilege
- Continuously evaluate access
- Limit unnecessary trust
- Segment resources
- Assume compromise is possible

Network access decisions can therefore consider identity, device status, resource sensitivity, and other factors.

## Example ACL Design

Assume an organization has:

```text
Employee Network:   10.10.10.0/24
Server Network:     10.10.20.0/24
Guest Network:      10.10.30.0/24
Management Network: 10.10.99.0/24
```

A simplified policy might be:

```text
ALLOW Employees -> Approved Server Services
ALLOW Management -> Network Infrastructure
ALLOW Guests -> Internet
DENY  Guests -> Internal Networks
DENY  Users -> Management Network
DENY  ANY -> ANY
```

The final deny rule blocks traffic that was not specifically approved earlier.

## Example Troubleshooting Scenario — Website Access Blocked

**Problem:** Users can send email but cannot access websites.

Firewall rules:

```text
ALLOW TCP 25
ALLOW TCP 110
DENY ANY ANY
```

Troubleshooting process:

1. Identify which services work.
2. Identify which services fail.
3. Determine the ports used by the failed service.
4. Review the firewall rule set.
5. Check rule order.
6. Verify whether TCP 80 and 443 are permitted.
7. Add only the required rules.
8. Retest connectivity.
9. Document the change.

The problem occurs because the required web ports were never permitted before the final deny rule.

## Example Troubleshooting Scenario — RDP Blocked

**Problem:** An administrator cannot remotely connect to a server using RDP.

Possible checks include:

1. Verify IP connectivity.
2. Confirm the server is reachable.
3. Verify RDP is enabled.
4. Check whether TCP/UDP 3389 is permitted.
5. Check the source network.
6. Review firewall or ACL rule order.
7. Verify the connection is allowed only from approved management systems.
8. Retest after correcting the policy.

A secure solution should avoid opening RDP to unnecessary networks.

## Firewall Troubleshooting Process

When troubleshooting traffic that may be blocked by a firewall or ACL:

1. Identify the source IP.
2. Identify the destination IP.
3. Identify the protocol.
4. Identify the destination port or service.
5. Determine the direction of traffic.
6. Review the applicable firewall or ACL rules.
7. Check rule order.
8. Check for an implicit or explicit deny.
9. Verify routing and VLAN configuration.
10. Confirm the destination service is actually listening.
11. Test the connection.
12. Review logs if available.
13. Document the findings and any changes.

## Security Considerations

Firewall and ACL rules should be specific enough to meet operational requirements without unnecessarily expanding access.

Good practices include:

- Use least privilege
- Prefer default-deny policies
- Document firewall rules
- Remove unnecessary rules
- Review rules periodically
- Restrict administrative services
- Segment sensitive networks
- Log important security events
- Restrict both inbound and outbound traffic where appropriate
- Avoid overly broad `any-to-any` allow rules
- Verify rule order after changes

## Key Takeaways

Some of the most important concepts I learned include:

- Firewalls control traffic according to security policies.
- Stateful firewalls track active connections.
- ACLs use permit and deny rules to filter traffic.
- Rule order can completely change the outcome of a policy.
- A final `deny any any` blocks traffic that was not explicitly permitted earlier.
- Many systems also use some form of implicit deny.
- Default-deny supports least privilege.
- Ports and protocols can be used to restrict access to services.
- Segmentation and access control work together.
- Authentication identifies a user or device, while authorization determines permitted access.
- RBAC assigns permissions according to roles.
- NAC can control whether users and devices are allowed onto a network.
- Zero Trust avoids automatically trusting traffic simply because it originates inside the network.

Understanding firewalls and ACLs helped me connect networking concepts such as ports, protocols, routing, and segmentation with the cybersecurity principles of least privilege, access control, and defense in depth.
