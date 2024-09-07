# Day 16 - VLANs Part 1

Reviewed: No

### **What is a LAN?**

- **Definition:** A LAN (Local Area Network) is a single broadcast domain where all devices receive a broadcast frame.
- **Broadcast Domain:** A group of devices receiving a broadcast frame (destination MAC of all Fs).
- **LAN Composition:** Includes PCs, servers, routers, switches, etc., typically in a single location (home, office).

### **Understanding Broadcast Domains**

1. **Behavior of Broadcast Frames:**
    - Sent by a device (e.g., PC) and flooded by switches.
    - Routers do not forward broadcast frames, thus ending the domain.
2. **Example Network Analysis:**
    - **Scenario:** Multiple PCs connected through switches and routers.
    - **Broadcast Domain Count:** Four distinct domains identified based on the propagation of broadcast frames.

### **Introduction to VLANs**

- **Definition:** VLANs are logical subdivisions within a LAN that segment the network into multiple broadcast domains at Layer 2.
- **Purpose:** Improve network performance and security by controlling broadcast traffic and access.

### **Benefits of VLANs**

1. **Performance:** Reduces unnecessary broadcast traffic, improving overall network efficiency.
2. **Security:** Limits access and controls traffic between different parts of the network.

### **VLAN Configuration Basics**

- **Assigning VLANs:** Configured on switch interfaces to assign devices to specific VLANs.
- **Separation:** VLANs create separate broadcast domains, preventing traffic from crossing VLAN boundaries without routing.

### **Scenario: Company Network**

- **Departments:** Engineering, Sales, and Human Resources.
- **Network Segmentation:** Initially all in one subnet (192.168.1.0/24), causing security and performance issues.
- **Solution:** Separate departments into distinct subnets (e.g., Engineering - 192.168.1.0/26, HR - 192.168.1.64/26, Sales - 192.168.1.128/26) and assign VLANs (VLAN10, VLAN20, VLAN30).

### **Detailed VLAN Configuration on Cisco Switches**

1. **Default VLANs:** VLAN1 and VLANs 1002-1005 exist by default and cannot be deleted.
2. **Access Ports:** Configured to connect end hosts; belong to a single VLAN.
3. **Trunk Ports:** Carry multiple VLANs; discussed in detail in Day 17.
4. **Commands:**
    - `interface range G1/0 - G1/3`: Select interfaces.
    - `switchport mode access`: Set interfaces to access mode.
    - `switchport access vlan [VLAN_ID]`: Assign VLAN to interfaces.
    - `show vlan brief`: Display VLAN information on the switch.

### **VLAN Name Customization**

- **VLAN Naming:** Assign meaningful names (e.g., Engineering, HR, Sales) for clarity.
- **Command:** `vlan [VLAN_ID]` followed by `name [NAME]`.

### **Review and Summary**

- **LAN vs. VLAN:** A LAN is a broadcast domain, while a VLAN is a virtual segment of a LAN creating multiple broadcast domains.
- **Purpose of VLANs:** Enhances network performance and security by limiting broadcast domains and controlling access.
- **VLAN Configuration:** Focus on access ports, with trunk ports to be covered later.

### **Commands Used in Day 16**

- **VLAN Creation and Assignment:**
    - `show vlan brief`
    - `interface range [INTERFACES]`
    - `switchport mode access`
    - `switchport access vlan [VLAN_ID]`
    - `vlan [VLAN_ID]`
    - `name [NAME]`
