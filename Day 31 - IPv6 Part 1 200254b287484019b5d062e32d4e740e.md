# Day 31 - IPv6 Part 1

Reviewed: No

### **1. Introduction to IPv6:**

- **Transition to IPv6:** IPv6 is the future of networking, replacing IPv4 due to the exhaustion of IPv4 addresses.
- **CCNA Exam Focus:** IPv6 is covered under topics 1.8 (configure and verify IPv6 addressing and prefixes) and 1.9 (compare IPv6 address types).
- **Why IPv6?** The primary reason for IPv6 adoption is the shortage of IPv4 addresses. IPv4 addresses are 32 bits long, offering around 4.3 billion addresses, which is insufficient for today’s global internet needs.

### **2. Understanding Numbering Systems:**

- **Binary (Base 2):** Uses two digits, 0 and 1. Indicated by prefix `0b`.
- **Decimal (Base 10):** Uses ten digits, 0 through 9. Indicated by prefix `0d`.
- **Hexadecimal (Base 16):** Uses sixteen digits, 0-9 and A-F. Indicated by prefix `0x`.

### **3. Hexadecimal Review:**

- **Conversion:** Each hexadecimal digit represents 4 binary bits.
- **Conversion Practice:Example Conversions:**
    - **Binary to Hexadecimal:** Split the binary number into groups of 4 bits and convert each group to its hexadecimal equivalent.
    - **Hexadecimal to Binary:** Convert each hexadecimal digit to its 4-bit binary equivalent.
    - Binary `1101 1011` = Hexadecimal `DB`.
    - Hexadecimal `2B` = Binary `0010 1011`.

### **4. Why IPv6 is Necessary:**

- **IPv4 Exhaustion:** IPv4 provides about 4.3 billion addresses, but the modern internet requires more due to the proliferation of devices.
- **IPv6 Solution:** IPv6 uses 128-bit addresses, allowing for approximately `340 undecillion` addresses (a vast number).

### **5. IPv6 Addressing:**

- **IPv6 Structure:**
    - **Length:** 128 bits.
    - **Representation:** Written as 32 hexadecimal digits, divided into 8 groups (quartets) separated by colons.
    - **Example:** `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.
- **IPv6 Notation:**
    - **Prefix Length:** Uses a slash `/` to indicate the network portion (e.g., `/64` means the first 64 bits are the network part).
    - **Shortening Addresses:**
        - **Leading Zeros:** Can be omitted (e.g., `0db8` becomes `db8`).
        - **Double Colons (`::`):** Can replace consecutive quartets of zeros, but only once per address.
- **Practice Shortening:**
    - **Full Address:** `2001:0db8:0000:0000:0000:0000:0000:0001`.
    - **Shortened:** `2001:db8::1`.

### **6. Expanding IPv6 Addresses:**

- **Reverse the Shortening:** When expanding an IPv6 address, replace the double colon with the appropriate number of `0000` quartets.
- **Example Expansion:**
    - **Shortened:** `2001:db8::1`.
    - **Expanded:** `2001:0db8:0000:0000:0000:0000:0000:0001`.

### **7. Finding IPv6 Network Prefix:**

- **Prefix Identification:** Convert the host portion to zeros to find the network prefix.
- **Multiple of 4:** If the prefix length is a multiple of 4, conversion is straightforward by identifying the boundary between network and host portions.

### **8. IPv6 Configuration on Cisco Routers:**

- **Enabling IPv6 Routing:**
    - Command: `ipv6 unicast-routing` in global configuration mode.
- **Assigning IPv6 Addresses:**
    - Command: `ipv6 address [address]/[prefix length]` under the interface configuration.
    - Example: `ipv6 address 2001:db8:0:1::1/64`.
- **Verification:**
    - Command: `show ipv6 interface brief` displays the configured IPv6 addresses and their link-local addresses.

### **9. Link-Local Addresses:**

- **Automatically Assigned:** When an IPv6 address is configured on an interface, a link-local address is automatically assigned. Link-local addresses are used for communication on the same link and are not routable.