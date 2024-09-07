# Day 10 - IPv4 Header

Reviewed: No

### **Key Concepts**

### **Structure of an IPv4 Packet**

1. **Data + Layer 4 Header (TCP/UDP)**: Known as a segment.
2. **Segment + Layer 3 Header (IP)**: Known as a packet.
3. **Packet + Layer 2 Header and Trailer**: Known as a frame.

### **Fields of the IPv4 Header**

1. **Version (4 bits)**
    - Identifies the IP version (4 for IPv4).
    - Binary value for IPv4 is 0100.
2. **Internet Header Length (IHL) (4 bits)**
    - Specifies the header length in 4-byte increments.
    - Minimum value is 5 (20 bytes), and the maximum is 15 (60 bytes).
3. **Differentiated Services Code Point (DSCP) (6 bits)**
    - Used for Quality of Service (QoS) to prioritize certain types of traffic.
4. **Explicit Congestion Notification (ECN) (2 bits)**
    - Signals network congestion without dropping packets.
5. **Total Length (16 bits)**
    - Indicates the total length of the packet (header + data) in bytes.
    - Maximum value is 65,535 bytes.
6. **Identification (16 bits)**
    - Identifies fragments of a packet, allowing reassembly.
7. **Flags (3 bits)**
    - **Bit 0:** Reserved, always 0.
    - **Bit 1:** Don't Fragment (DF) bit. Set to 1 to prevent fragmentation.
    - **Bit 2:** More Fragments (MF) bit. Set to 1 if more fragments follow.
8. **Fragment Offset (13 bits)**
    - Indicates the position of a fragment in the original packet.
9. **Time to Live (TTL) (8 bits)**
    - Limits the lifespan of a packet, preventing infinite loops. Decreased by 1 at each hop.
10. **Protocol (8 bits)**
    - Indicates the protocol of the encapsulated data (6 for TCP, 17 for UDP, 1 for ICMP, 89 for OSPF).
11. **Header Checksum (16 bits)**
    - Error-checking the header. Calculated and verified by routers.
12. **Source IP Address (32 bits)**
    - The IPv4 address of the sender.
13. **Destination IP Address (32 bits)**
    - The IPv4 address of the intended receiver.
14. **Options (0-320 bits)**
    - Optional field for additional information. Rarely used.

### **Key Points**

- **IPv4 Header Size:** The minimum is 20 bytes (no options), and the maximum is 60 bytes (maximum options).
- **Fragmentation:** Handled by the Identification, Flags, and Fragment Offset fields. Fragments reassembled by the receiving host.
- **TTL:** Prevents endless loops by limiting the number of hops a packet can take.
- **Checksum:** Ensures header integrity. If mismatched, the packet is dropped.

### **Wireshark Packet Capture Analysis**

- **Packet Analysis:** Identified and analyzed the different parts of the IPv4 header and the encapsulated data using Wireshark.
- **Fragmentation Example:** Demonstrated packet fragmentation and reassembly, including the use of the DF bit and fragment offset.

### **Quiz Questions**

1. **What is the fixed binary value of the first field of an IPv4 header?**
    - **Answer:** D, 0100 (Version field for IPv4).
2. **Which field will cause the packet to be dropped if it has a value of 0?**
    - **Answer:** A, TTL (Time To Live).
3. **How are errors in an IPv4 packet’s encapsulated data detected?**
    - **Answer:** B, the encapsulated protocol (TCP/UDP) checks for errors.
4. **Which field of an IPv4 header is variable in length?**
    - **Answer:** A, Options.
5. **Which bit will be set to 1 on all IPv4 packet fragments except the last fragment?**
    - **Answer:** B, More Fragments bit.
