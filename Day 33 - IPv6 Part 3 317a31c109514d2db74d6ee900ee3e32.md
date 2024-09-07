# Day 33 - IPv6 Part 3

Reviewed: No

### **1. Introduction to IPv6 Static Routing:**

- **Focus on Exam Topic:**
    - **3.3**: Applying IPv4 static routing concepts to IPv6.
- **IPv6 in CCNA:**
    - Many students feel less confident with IPv6 because most courses focus primarily on IPv4. Spending more time on IPv6 will build confidence.

### **2. IPv6 Address Representation Correction:**

- **RFC 5952**: Standardizes IPv6 address text representation.
    - **Leading 0s** MUST be removed.
    - **Double colon (::)** MUST be used to shorten the longest string of all-0 quartets.
    - **Hexadecimal letters (a-f)** MUST be in **lower-case**.

### **3. IPv6 Header Overview:**

- **IPv6 Header Simplification:**
    - **Fixed header size:** 40 bytes, making processing easier for routers compared to the variable IPv4 header (20-60 bytes).
- **Fields in IPv6 Header:**
    - **Version (4 bits):** Indicates IP version 6 (binary 0110).
    - **Traffic Class (8 bits):** Used for Quality of Service (QoS).
    - **Flow Label (20 bits):** Identifies traffic flows (e.g., between a server and a client).
    - **Payload Length (16 bits):** Indicates the length of the encapsulated Layer 4 segment.
    - **Next Header (8 bits):** Indicates the type of the next header (e.g., TCP or UDP).
    - **Hop Limit (8 bits):** Similar to IPv4’s TTL, decrements by 1 at each hop; packet discarded when it reaches 0.
    - **Source and Destination Address (128 bits each):** Contains the IPv6 addresses of the source and destination.

### **4. Neighbor Discovery Protocol (NDP):**

- **NDP Functions:**
    - Replaces ARP in IPv6, using **ICMPv6** messages instead of broadcasts.
- **Solicited-Node Multicast Address:**
    - Formed by combining `ff02::1:ff` with the last 6 hex digits of the unicast address.
- **Key NDP Messages:**
    - **Neighbor Solicitation (NS) - ICMPv6 Type 135:** Equivalent to ARP request, asks for a MAC address.
    - **Neighbor Advertisement (NA) - ICMPv6 Type 136:** Equivalent to ARP reply, provides a MAC address.
    - **Router Solicitation (RS) - ICMPv6 Type 133:** Hosts send to discover routers on the local link.
    - **Router Advertisement (RA) - ICMPv6 Type 134:** Routers respond to RS messages, announcing their presence.
- Command to use instead of ARP table: `show ipv6 neighbor`

### **5. Stateless Address Auto-configuration (SLAAC):**

- **SLAAC Overview:**
    - Allows hosts to automatically configure an IPv6 address without manual configuration.
    - Uses **RS and RA messages** to learn the IPv6 prefix and generate an address (e.g., `ipv6 address autoconfig` on Cisco routers).
- **Duplicate Address Detection (DAD):**
    - Ensures the uniqueness of an IPv6 address on a network by sending an NS to the address itself. If no NA reply is received, the address is considered unique.

### **6. IPv6 Static Routing:**

- **IPv6 Static Route Command Structure:**
    
    `ipv6 route [destination]/[prefix-length] {next-hop-address | exit-interface} [AD]`
    
    - **Directly Attached Route:** Specifies only the exit interface.
    - **Recursive Route:** Specifies only the next-hop address.
    - **Fully Specified Route:** Specifies both the exit interface and next-hop address.
- **Types of IPv6 Static Routes:**
    - **Network Route:** Route to a specific subnet.
    - **Host Route:** Route to a single specific host (e.g., /128 prefix length).
    - **Default Route:** Route for all destinations not in the routing table (`::/0` in IPv6).
    - **Floating Static Route:** Backup route with a higher administrative distance (AD).
- **Important Considerations:**
    - **Directly Attached Routes:** Cannot be used on Ethernet interfaces in IPv6, unlike IPv4. Must use recursive or fully specified routes instead.

### **7. Summary and Review:**

- **IPv6 Address Representation:** Follow the rules from RFC 5952 (e.g., remove leading zeros, use lower-case).
- **IPv6 Header:** Fixed 40-byte header simplifies processing.
- **NDP:** Replaces ARP, uses multicast instead of broadcast for efficiency.
- **SLAAC:** Enables automatic IPv6 address configuration.
- **Static Routes in IPv6:** Similar to IPv4 but with key differences, such as the inability to use directly attached routes on Ethernet interfaces.