# DNS & DHCP Network Services

This lab documents my study of DNS and DHCP from CompTIA Network+ coursework and practice.

The goal is to demonstrate my understanding of how DNS provides name resolution, how DHCP automatically distributes network configuration, how these services interact with clients and network infrastructure, and how to troubleshoot common DNS and DHCP problems.

## Concepts Practiced

- DNS
- Forward and reverse lookups
- DNS record types
- DNS zones
- Recursive and iterative queries
- DNS caching
- DNS troubleshooting
- DHCP
- DHCP scopes
- DHCP leases
- DHCP reservations
- DHCP options
- DORA
- DHCP relay
- APIPA
- IPv4 and IPv6 addressing
- SLAAC
- DHCPv6
- Network service troubleshooting

# DNS

DNS stands for **Domain Name System**.

DNS allows users and applications to use names instead of having to remember IP addresses.

For example:

```text
www.example.com
        |
        v
DNS Resolution
        |
        v
192.0.2.25
```

Without DNS, users would often need to connect directly using IP addresses.

## Forward Lookup

A forward DNS lookup translates a hostname into an IP address.

Example:

```text
server.example.com
        |
        v
192.168.10.25
```

Forward lookup zones commonly contain records such as:

- A
- AAAA
- CNAME
- MX
- TXT
- SRV

## Reverse Lookup

A reverse lookup attempts to map an IP address back to a hostname.

Example:

```text
192.168.10.25
        |
        v
server.example.com
```

Reverse DNS commonly uses **PTR records**.

## Common DNS Record Types

| Record | Purpose |
|---|---|
| A | Maps a hostname to an IPv4 address |
| AAAA | Maps a hostname to an IPv6 address |
| CNAME | Creates an alias for another hostname |
| MX | Identifies mail servers for a domain |
| TXT | Stores text-based information such as SPF data |
| PTR | Maps an IP address back to a hostname |
| NS | Identifies authoritative DNS servers |
| SRV | Identifies services and the hosts providing them |

## A Record

An A record maps a hostname to an IPv4 address.

Example:

```text
server.example.com -> 192.168.10.25
```

## AAAA Record

An AAAA record maps a hostname to an IPv6 address.

Example:

```text
server.example.com -> 2001:db8::25
```

## CNAME Record

A CNAME creates an alias that points to another hostname.

Example:

```text
portal.example.com -> webserver.example.com
```

Instead of maintaining separate IP address records for both names, the alias points to the canonical hostname.

## MX Record

An MX record identifies the mail servers responsible for receiving email for a domain.

Example:

```text
example.com -> mail.example.com
```

MX records can also include priorities when multiple mail servers exist.

## TXT Record

TXT records store text-based information associated with a domain.

They are commonly used for items such as:

- SPF
- Domain verification
- Email security information

## PTR Record

A PTR record is used for reverse DNS lookups.

Example:

```text
192.168.10.25 -> server.example.com
```

## NS Record

An NS record identifies the authoritative name servers for a DNS zone.

These servers are responsible for maintaining authoritative DNS information for the domain.

## SRV Record

An SRV record identifies a service and the system providing it.

SRV records can include:

- Service
- Protocol
- Port
- Host
- Priority
- Weight

They are commonly used by enterprise applications and services.

# DNS Zones

A DNS zone is an administrative portion of the DNS namespace.

Zones contain records for systems and services within that portion of the namespace.

Common examples include:

- Forward lookup zones
- Reverse lookup zones

## Authoritative DNS Server

An authoritative DNS server contains the official DNS records for a zone.

If it is authoritative for `example.com`, it can provide authoritative answers for records within that zone.

## Recursive DNS Query

In a recursive query, the DNS resolver is expected to return a final answer to the client.

Conceptually:

```text
Client
  |
  v
Recursive DNS Server
  |
  v
Other DNS Servers
  |
  v
Final Answer Returned to Client
```

## Iterative DNS Query

In an iterative query, a DNS server may respond with the best information it currently has, including a referral to another DNS server.

The resolver can then continue querying other servers until it reaches the authoritative answer.

## DNS Resolution Process

A simplified DNS lookup might occur like this:

1. The client checks its local DNS cache.
2. The client sends a query to its configured DNS resolver.
3. The resolver checks its cache.
4. If necessary, the resolver queries other DNS servers.
5. The authoritative answer is located.
6. The IP address is returned to the client.
7. The answer may be cached for future use.

# DNS Caching

DNS caching stores recently resolved information temporarily.

Caching can improve performance by reducing the need to repeat the entire DNS resolution process.

However, outdated cached information can sometimes cause troubleshooting problems.

On Windows, the DNS cache can be cleared with:

`ipconfig /flushdns`

# DNS TTL

TTL stands for **Time to Live**.

A DNS record's TTL determines how long a resolver may cache the record before requesting updated information.

A longer TTL can reduce DNS query traffic.

A shorter TTL allows DNS changes to propagate more quickly but can increase the number of queries.

# DNS Troubleshooting

Common DNS problems may include:

- Incorrect DNS server configuration
- DNS server unavailable
- Missing DNS records
- Incorrect DNS records
- Stale cache entries
- Network connectivity problems
- Firewall rules blocking DNS
- Incorrect zone configuration

## DNS Troubleshooting Commands

### `nslookup`

Used to query DNS information.

Example:

```text
nslookup example.com
```

This can help identify:

- Which DNS server answered
- Which IP address was returned
- Whether name resolution succeeds

### `ipconfig /all`

Displays detailed Windows network configuration, including configured DNS servers.

### `ipconfig /flushdns`

Clears the local Windows DNS resolver cache.

### `ping`

Can help determine whether name resolution and connectivity are working.

Example:

```text
ping server.example.com
```

If the hostname resolves to an IP address but the ping fails, DNS may still be functioning even if the destination does not respond to ICMP.

# Example DNS Troubleshooting Scenario

**Problem:** A workstation can reach `8.8.8.8` but cannot access websites by name.

Possible troubleshooting process:

1. Confirm IP connectivity.
2. Check the configured DNS server.
3. Run `nslookup`.
4. Test another hostname.
5. Check whether the DNS server responds.
6. Flush the local DNS cache.
7. Verify firewall rules allow DNS traffic.
8. Check DNS records if the problem affects only one hostname.
9. Document the results.

If IP connectivity works but name resolution fails, DNS becomes a likely area to investigate.

---

# DHCP

DHCP stands for **Dynamic Host Configuration Protocol**.

DHCP automatically provides network configuration to clients.

DHCP can provide information such as:

- IP address
- Subnet mask
- Default gateway
- DNS servers
- Lease duration
- Other network options

Without DHCP, administrators may need to manually configure each client.

## DHCP Scope

A DHCP scope defines the pool of addresses and configuration available for a subnet.

Example:

```text
Network: 192.168.10.0/24

DHCP Pool:
192.168.10.50 - 192.168.10.200
```

Addresses outside the DHCP pool may be reserved for infrastructure or statically configured systems.

## DHCP Lease

A DHCP lease allows a client to use an IP address for a specific period of time.

The address is not necessarily permanently assigned to that client.

Clients attempt to renew their leases before expiration.

## DHCP Reservation

A DHCP reservation allows a specific device to consistently receive the same IP address from DHCP.

Reservations are commonly associated with a device's MAC address.

This can be useful for:

- Printers
- Servers
- Network appliances
- Devices that need predictable addresses

The address is still managed through DHCP rather than being manually configured on the endpoint.

# DORA

The traditional IPv4 DHCP address-assignment process is remembered as **DORA**:

1. Discover
2. Offer
3. Request
4. Acknowledge

## DHCP Discover

The client initially does not know which DHCP server is available.

It sends a DHCP Discover message looking for a DHCP server.

## DHCP Offer

A DHCP server responds with an offer containing proposed network configuration.

This may include:

- IP address
- Subnet mask
- Lease duration
- Gateway
- DNS information

## DHCP Request

The client sends a DHCP Request indicating that it wants to accept an offered address.

## DHCP Acknowledge

The DHCP server sends an acknowledgment confirming the lease.

The client can then use the assigned network configuration.

Conceptually:

```text
Client                         DHCP Server
  |                                |
  |---- DHCP Discover ------------>|
  |<--- DHCP Offer ----------------|
  |---- DHCP Request ------------->|
  |<--- DHCP Acknowledge ----------|
```

# DHCP Options

DHCP options provide additional network configuration.

Common examples include:

- Default gateway
- DNS servers
- Domain information
- NTP servers
- Other network service information

This allows administrators to centrally distribute configuration to clients.

# DHCP Relay

DHCP clients often use broadcasts when initially requesting configuration.

Routers normally do not forward Layer 2 broadcasts between subnets.

A **DHCP relay** allows DHCP requests from one subnet to reach a DHCP server located on another network.

Conceptually:

```text
Client VLAN
   |
   v
Router / DHCP Relay
   |
   v
Central DHCP Server
```

This prevents organizations from needing a separate DHCP server on every subnet.

Some network devices may refer to this functionality as an **IP helper**.

# Example DHCP Relay Design

Assume:

```text
VLAN 10
192.168.10.0/24

VLAN 20
192.168.20.0/24

DHCP Server
192.168.100.10
```

Clients in VLAN 10 and VLAN 20 need DHCP addresses.

The router or Layer 3 switch can relay DHCP requests from each VLAN to:

`192.168.100.10`

The DHCP server then provides addresses from the correct scope.

# APIPA

APIPA stands for **Automatic Private IP Addressing**.

When a Windows client configured for DHCP cannot obtain an IPv4 address from a DHCP server, it may assign itself an address in:

`169.254.0.0/16`

Example:

`169.254.27.18`

Seeing a `169.254.x.x` address is an important troubleshooting clue.

It may indicate:

- DHCP server unavailable
- DHCP scope exhausted
- DHCP relay problem
- VLAN problem
- Network connectivity problem
- Firewall or ACL issue

An APIPA address generally allows only limited local communication and does not provide normal routed network access.

# DHCP Troubleshooting Commands

## `ipconfig /all`

Displays:

- IP address
- Subnet mask
- Default gateway
- DNS servers
- DHCP status
- DHCP server
- Lease information

## `ipconfig /release`

Releases the current DHCP lease.

## `ipconfig /renew`

Requests a new DHCP lease.

These commands can be useful when troubleshooting client addressing.

# Example DHCP Troubleshooting Scenario

**Problem:** A workstation shows:

`169.254.15.22`

Possible troubleshooting process:

1. Verify the physical or wireless connection.
2. Run `ipconfig /all`.
3. Confirm DHCP is enabled.
4. Check whether other devices are affected.
5. Verify the correct VLAN.
6. Check DHCP server availability.
7. Check the DHCP scope for available addresses.
8. Verify DHCP relay configuration if the server is on another subnet.
9. Run `ipconfig /release`.
10. Run `ipconfig /renew`.
11. Document the findings.

The APIPA address suggests the workstation was unable to complete the DHCP process successfully.

# DHCP Scope Exhaustion

A DHCP scope can run out of available addresses.

Example:

```text
Scope:
192.168.10.100 - 192.168.10.150
```

If all available addresses are already leased, additional clients may be unable to obtain valid configuration.

Possible solutions may include:

- Expanding the DHCP scope
- Adjusting lease duration
- Reviewing unused leases
- Redesigning the subnet if additional capacity is needed

# DHCP and VLANs

Organizations commonly use a separate DHCP scope for each VLAN or subnet.

Example:

| VLAN | Subnet | DHCP Range |
|---|---|---|
| VLAN 10 | 192.168.10.0/24 | 192.168.10.50-200 |
| VLAN 20 | 192.168.20.0/24 | 192.168.20.50-200 |
| VLAN 30 | 192.168.30.0/24 | 192.168.30.50-200 |

A DHCP relay can forward each subnet's requests to a centralized DHCP server.

# DHCP Security Considerations

An unauthorized DHCP server can provide incorrect configuration to clients.

A rogue DHCP server could potentially provide:

- Incorrect default gateway
- Malicious DNS server
- Incorrect addressing
- Network configuration controlled by an attacker

Switch security features such as **DHCP snooping** can help reduce rogue DHCP risks in supported environments.

---

# IPv6 Address Configuration

IPv6 can use several methods for address configuration.

These may include:

- Static addressing
- SLAAC
- DHCPv6

# SLAAC

SLAAC stands for **Stateless Address Autoconfiguration**.

SLAAC allows IPv6 devices to generate their own addresses using information advertised by a router.

The router can provide information about the network prefix.

This allows clients to configure IPv6 addresses without requiring a traditional stateful DHCP process.

# DHCPv6

DHCPv6 can also provide IPv6 configuration.

Depending on the network design, DHCPv6 may provide:

- IPv6 addresses
- DNS information
- Other configuration information

IPv6 networks can use different combinations of router advertisements, SLAAC, and DHCPv6.

# DNS and DHCP Working Together

DNS and DHCP perform different jobs but often work closely together.

DHCP provides clients with network configuration.

DNS allows those clients to locate services by name.

Example:

```text
Client Starts
     |
     v
DHCP Provides:
IP Address
Subnet
Gateway
DNS Server
     |
     v
Client Queries DNS
     |
     v
DNS Resolves Hostname
     |
     v
Client Connects to Destination
```

A client may have valid DHCP configuration but still experience problems if DNS is unavailable.

Likewise, DNS may be functioning normally while a client cannot reach it because DHCP supplied incorrect network configuration.

# Example Combined Troubleshooting Scenario

**Problem:** A user reports that they cannot reach internal websites.

Client configuration:

```text
IP Address: 192.168.20.75
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.20.1
DNS Server: 192.168.20.10
```

Possible troubleshooting process:

1. Verify the DHCP-assigned address.
2. Confirm the correct subnet.
3. Ping the default gateway.
4. Test connectivity to the DNS server.
5. Run `nslookup`.
6. Verify the hostname resolves correctly.
7. Check whether the destination IP is reachable.
8. Review DHCP and DNS configuration if necessary.
9. Document the results.

This helps separate addressing problems from name-resolution problems.

# Key Takeaways

Some of the most important concepts I learned include:

- DNS translates names into IP addresses.
- A and AAAA records map hostnames to IPv4 and IPv6 addresses.
- PTR records support reverse lookups.
- MX records identify mail servers.
- TXT records can contain information such as SPF data.
- SRV records identify network services.
- DNS caching improves performance but can sometimes cause stale results.
- DHCP automatically provides client network configuration.
- DORA represents Discover, Offer, Request, and Acknowledge.
- DHCP reservations provide predictable addresses while remaining centrally managed.
- DHCP relay allows centralized DHCP servers to support multiple subnets.
- APIPA addresses can indicate a DHCP connectivity problem.
- VLANs and subnets commonly use separate DHCP scopes.
- SLAAC and DHCPv6 provide IPv6 configuration options.
- DNS and DHCP are separate services but both are critical to normal network operation.

Understanding DNS and DHCP helped me connect addressing, routing, VLANs, network services, troubleshooting, and client configuration into a more complete understanding of how users and systems communicate across a network.
