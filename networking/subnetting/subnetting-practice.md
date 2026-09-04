# Subnetting Practice

This lab documents my subnetting practice from CompTIA Network+ study and networking coursework.

The goal is to demonstrate how I determine subnet masks, network IDs, broadcast addresses, usable host ranges, block sizes, and host capacity using CIDR notation.

## Concepts Practiced

- CIDR notation
- Subnet masks
- Network and host portions of an IPv4 address
- Network IDs
- Broadcast addresses
- First and last usable host addresses
- Block sizes
- Total and usable host calculations
- Determining CIDR prefixes from subnet masks
- Subnetting within the third and fourth octets
- Selecting subnet sizes based on host requirements

## Quick Subnetting Method

When solving a subnetting problem, I generally work through these steps:

1. Identify the CIDR prefix.
2. Convert the prefix to a subnet mask if needed.
3. Find the interesting octet where subnetting occurs.
4. Calculate the block size using:

   `256 - subnet mask value`

5. Determine which subnet range contains the IP address.
6. The first address in the range is the network ID.
7. The last address in the range is the broadcast address.
8. The addresses between them are usable host addresses.

## Host Calculation

For traditional IPv4 subnets:

`Total addresses = 2^(host bits)`

`Usable hosts = total addresses - 2`

The two traditionally reserved addresses are:

- Network address
- Broadcast address

## Common Prefix Examples

| CIDR | Subnet Mask | Total Addresses | Usable Hosts |
|---|---|---:|---:|
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 6 |
| /30 | 255.255.255.252 | 4 | 2 |

## Practice Example 1 — /29

**Host address:** `192.168.0.123/29`

A `/29` uses the subnet mask:

`255.255.255.248`

Block size:

`256 - 248 = 8`

The fourth-octet subnet ranges increase by 8:

`0, 8, 16, 24, ... 112, 120, 128`

The address `123` falls inside the `120-127` subnet.

**Results:**

- Network ID: `192.168.0.120`
- First usable host: `192.168.0.121`
- Last usable host: `192.168.0.126`
- Broadcast address: `192.168.0.127`
- Total addresses: `8`
- Usable hosts: `6`

## Practice Example 2 — /26

**Host address:** `172.16.200.130/26`

A `/26` uses the subnet mask:

`255.255.255.192`

Block size:

`256 - 192 = 64`

The fourth-octet ranges are:

- `0-63`
- `64-127`
- `128-191`
- `192-255`

The address `130` falls inside the `128-191` subnet.

**Results:**

- Network ID: `172.16.200.128`
- First usable host: `172.16.200.129`
- Last usable host: `172.16.200.190`
- Broadcast address: `172.16.200.191`
- Total addresses: `64`
- Usable hosts: `62`

## Practice Example 3 — /27

**Host address:** `192.168.1.146/27`

A `/27` uses the subnet mask:

`255.255.255.224`

Block size:

`256 - 224 = 32`

The fourth-octet ranges are:

- `0-31`
- `32-63`
- `64-95`
- `96-127`
- `128-159`
- `160-191`
- `192-223`
- `224-255`

The address `146` falls inside the `128-159` subnet.

**Results:**

- Network ID: `192.168.1.128`
- First usable host: `192.168.1.129`
- Last usable host: `192.168.1.158`
- Broadcast address: `192.168.1.159`
- Total addresses: `32`
- Usable hosts: `30`

## Practice Example 4 — /28

**Host address:** `10.0.5.219/28`

A `/28` uses the subnet mask:

`255.255.255.240`

Block size:

`256 - 240 = 16`

The address `219` falls inside the `208-223` subnet.

**Results:**

- Network ID: `10.0.5.208`
- First usable host: `10.0.5.209`
- Last usable host: `10.0.5.222`
- Broadcast address: `10.0.5.223`
- Total addresses: `16`
- Usable hosts: `14`

## Practice Example 5 — Subnetting in the Third Octet

**Host address:** `172.16.70.25/20`

A `/20` uses the subnet mask:

`255.255.240.0`

Subnetting occurs in the third octet.

Block size:

`256 - 240 = 16`

The third-octet ranges are:

- `0-15`
- `16-31`
- `32-47`
- `48-63`
- `64-79`
- `80-95`

The third octet `70` falls inside the `64-79` subnet.

**Results:**

- Network ID: `172.16.64.0`
- First usable host: `172.16.64.1`
- Last usable host: `172.16.79.254`
- Broadcast address: `172.16.79.255`
- Total addresses: `4096`
- Usable hosts: `4094`

## Choosing a Subnet for a Host Requirement

When choosing a subnet size, I look for the smallest subnet that provides enough usable host addresses.

### Example: 5 Hosts

A `/30` provides only 2 usable hosts, so it is too small.

A `/29` provides:

- 8 total addresses
- 6 usable hosts

Therefore, `/29` is the smallest traditional subnet that supports 5 hosts.

### Example: 13 Hosts

A `/29` provides 6 usable hosts, which is too small.

A `/28` provides:

- 16 total addresses
- 14 usable hosts

Therefore, `/28` supports 13 hosts.

## Key Takeaways

Subnetting became much easier for me once I stopped trying to memorize every possible subnet and instead focused on:

- Identifying the interesting octet
- Calculating the block size
- Finding the range containing the host address
- Recognizing the first address as the network ID
- Recognizing the last address as the broadcast address
- Calculating usable host capacity from the remaining host bits

Practicing subnetting in both the third and fourth octets helped strengthen my understanding of IPv4 addressing and network design.
