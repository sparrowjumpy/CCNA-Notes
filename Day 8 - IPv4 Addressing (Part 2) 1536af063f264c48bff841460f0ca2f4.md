# Day 8 - IPv4 Addressing (Part 2)

Reviewed: No

## Lecture Overview

- 8th lecture, part 2 on IPv4 addresses.
- Review IPv4 classes and cover previously missed points.
- Learn to calculate:
    - Maximum number of hosts
    - Network address
    - Broadcast address
    - First and last usable addresses
- Configure IP addresses on Cisco devices.

## IPv4 Address Classes

### Class A

- Range: 0-127 (0 and 127 reserved, usable range: 1-126).
- Leading bits: 0
- Prefix length: 8 bits
- Host bits: 24
- Networks: 128
- Addresses per network: 16,777,216

### Class B

- Range: 128-191
- Leading bits: 10
- Prefix length: 16 bits
- Host bits: 16
- Networks: 16,384
- Addresses per network: 65,536

### Class C

- Range: 192-223
- Leading bits: 110
- Prefix length: 24 bits
- Host bits: 8
- Networks: 2,097,152
- Addresses per network: 256

## Calculating Usable Addresses

- Formula: 2N−2 (N = number of host bits)
    
    2N−22^N - 2
    
- Reserved addresses: Network address (all host bits 0), Broadcast address (all host bits 1)

### Examples

1. **Class C Network (192.168.1.0/24)**
    - Total: 256 addresses
    - Usable: 256 - 2 = 254
    - First usable: 192.168.1.1
    - Last usable: 192.168.1.254
2. **Class B Network (172.16.0.0/16)**
    - Total: 65,536 addresses
    - Usable: 65,536 - 2 = 65,534
    - First usable: 172.16.0.1
    - Last usable: 172.16.255.254
3. **Class A Network (10.0.0.0/8)**
    - Total: 16,777,216 addresses
    - Usable: 16,777,216 - 2 = 16,777,214
    - First usable: 10.0.0.1
    - Last usable: 10.255.255.254

## Configuring IP Addresses on Cisco Devices

### Network Setup

- Example: Three small networks connected to a single router (R1) in GNS3.
- Assign first and last usable addresses to PCs and router interfaces.

### CLI Commands

1. Enter privileged exec mode:
    - `EN`
2. Check interface status:
    - `show ip interface brief`
3. Configure interface:
    - Enter interface configuration mode: `interface <name>`
    - Assign IP address: `ip address <address> <subnet mask>`
    - Enable interface: `no shutdown`

### Interface Status

- `show ip interface brief` output:
    - Interface, IP Address, OK?, Method, Status, Protocol columns.
    - Status: Layer 1 status (up/down).
    - Protocol: Layer 2 status (up/down).

### Additional Commands

- `show interfaces`: Detailed Layer 1 and Layer 2 information.
- `show interfaces description`: Shows descriptions of interfaces.

## Quiz and Review

### Questions on Calculations

1. Find the network address, maximum hosts, broadcast address, first and last usable addresses based on given IP addresses and prefixes.

### Example Questions

1. **PC1: IP Address 43.109.23.12/8**
    - Network address: 43.0.0.0
    - Maximum hosts: 16,777,214
    - Broadcast address: 43.255.255.255
    - First usable: 43.0.0.1
    - Last usable: 43.255.255.254
2. **PC4: IP Address 129.221.23.13/16**
    - Network address: 129.221.0.0
    - Maximum hosts: 65,534
    - Broadcast address: 129.221.255.255
    - First usable: 129.221.0.1
    - Last usable: 129.221.255.254
3. **PC8: IP Address 209.211.3.22/24**
    - Network address: 209.211.3.0
    - Maximum hosts: 254
    - Broadcast address: 209.211.3.255
    - First usable: 209.211.3.1
    - Last usable: 209.211.3.254
4. **PC5: IP Address 2.71.209.233/8**
    - Network address: 2.0.0.0
    - Maximum hosts: 16,777,214
    - Broadcast address: 2.255.255.255
    - First usable: 2.0.0.1
    - Last usable: 2.255.255.254
5. **PC6: IP Address 155.200.201.141/16**
    - Network address: 155.200.0.0
    - Maximum hosts: 65,534
    - Broadcast address: 155.200.255.255
    - First usable: 155.200.0.1
    - Last usable: 155.200.255.254