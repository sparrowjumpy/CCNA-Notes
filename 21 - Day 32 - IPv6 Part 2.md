# Day 32 - IPv6 Part 2

Reviewed: No

### **1. Introduction to IPv6 Address Types:**

- **Focus on Exam Topics:**
    - **1.9**: IPv6 address types (Global unicast, unique local, link local, multicast, anycast, etc.).
    - **1.9.f**: Understanding and configuring IPv6 using EUI-64.

### **2. EUI-64 Address Configuration:**

- **EUI-64 Overview:**
    - **EUI-64** stands for Extended Unique Identifier.
    - Converts a 48-bit MAC address into a 64-bit interface identifier.
    - The interface identifier forms the host portion of a /64 IPv6 address.
- **Steps to Convert MAC Address to EUI-64:**
    1. **Divide the MAC address** into two halves.
        - Example: MAC `1234 5678 90AB`, split between `56` and `78`.
    2. **Insert `FFFE` in the middle.**
        - Example: `1234 56FF FE78 90AB`.
    3. **Invert the 7th bit** of the MAC address.
        - The 7th bit is the 3rd bit of the second hex digit.
        - If it’s 0, change it to 1; if 1, change it to 0.
    4. **Form the 64-bit Interface Identifier** by appending it to the network prefix.
- **Command to Configure EUI-64 on a Cisco Router:** `ipv6 address [prefix]/64 eui-64`
    - Automatically generates the interface ID using EUI-64.

### **3. IPv6 Address Types:**

1. **Global Unicast Addresses:**
    - **Public addresses** used over the Internet.
    - **Prefix:** Originally 2000::/3, now includes all non-reserved addresses.
    - **Structure:**
        1. **Global Routing Prefix** (48 bits): Assigned by ISP.
        2. **Subnet Identifier** (16 bits): Used to create subnets.
        3. **Interface Identifier** (64 bits): Can be manually set or generated via EUI-64.
2. **Unique Local Addresses:**
    - **Private addresses** not routable on the Internet.
    - **Prefix:** FC00::/7 (usually starts with FD).
    - **Structure:**
        1. **FD**: Indicates a unique local address.
        2. **Global ID** (40 bits): Should be randomly generated for uniqueness.
        3. **Subnet Identifier** (16 bits).
        4. **Interface Identifier** (64 bits).
3. **Link-Local Addresses:**
    - Automatically generated on IPv6-enabled interfaces using `EUI-64`.
    - **Prefix:** FE80::/10.
    - Used for communication within a single subnet.
    - **Example Uses:** Routing protocol peerings, neighbor discovery protocol (NDP), and next-hop addresses for static routes.
4. **Multicast Addresses:**
    - Used for one-to-many communication.
    - **Prefix:** FF00::/8.
    - **Important Multicast Addresses:**
        - **FF02::1**: All nodes (acts like a broadcast).
        - **FF02::2**: All routers.
        - **FF02::5**: All OSPF routers.
        - **FF02::A**: All EIGRP routers.
    - **Multicast Scopes:**
        - **FF01::/16**: Interface-local (node-local) multicast.
        - **FF02::/16**: Link-local multicast.
        - **FF05::/16**: Site-local multicast.
        - **FF08::/16**: Organization-local multicast.
        - **FF0E::/16**: Global multicast.
5. **Anycast Addresses:**
    - **One-to-one-of-many** communication.
    - Multiple devices share the same anycast address; the routing protocol forwards packets to the nearest device.
    - Configured like a regular IPv6 address but designated as **anycast**.
    - Example configuration: `ipv6 address [address]/128 anycast`
6. **Other IPv6 Addresses:**
    - **Unspecified Address (`::/128`)**: Equivalent to `0.0.0.0` in IPv4, used when a device doesn't know its IPv6 address.
    - **Loopback Address (`::1/128`)**: Equivalent to `127.0.0.1` in IPv4, used to test the local protocol stack.

### Summary of all prefixes:

### **Unicast Prefixes**

1. **Global Unicast**
    - **Prefix:** `2000::/3`
    - **Usage:** Public IPv6 addresses used on the Internet. These addresses are globally unique.
2. **Unique Local**
    - **Prefix:** `FC00::/7`
    - **Usage:** Private IPv6 addresses used within an organization. These addresses are not routable on the public Internet. Typically, they start with `FD`.
3. **Link-Local**
    - **Prefix:** `FE80::/10`
    - **Usage:** Automatically generated addresses used for communication within a local network segment. Not routable beyond the local link.
4. **Loopback Address**
    - **Prefix:** `::1/128`
    - **Usage:** Used by a device to send a packet to itself for testing. Similar to `127.0.0.1` in IPv4.
5. **Unspecified Address**
    - **Prefix:** `::/128`
    - **Usage:** Represents a lack of an address (used during initial setup).

### **Multicast Prefixes**

1. **Multicast**
    - **Prefix:** `FF00::/8`
    - **Usage:** Used to send packets to multiple destinations at once. The scope (local, site, global) is defined by the subsequent bits in the address.
    - **Common Scopes:**
        - **FF01::/16**: Interface-local (Packets don't leave the device).
        - **FF02::/16**: Link-local (Packets stay within the local subnet).
        - **FF05::/16**: Site-local (Packets are routed within a site but not beyond).
        - **FF08::/16**: Organization-local (Packets can be routed across an organization's network).
        - **FF0E::/16**: Global (Packets can be routed globally, including across the public Internet).