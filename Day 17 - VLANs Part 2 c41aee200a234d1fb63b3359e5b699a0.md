# Day 17 - VLANs Part 2

Reviewed: No

### **Key Concepts**

### **Trunk Ports**

- **Definition:** Trunk ports carry traffic from multiple VLANs over a single physical interface, unlike access ports, which belong to a single VLAN.
- **Purpose:** Used to connect switches and to a router for inter-VLAN routing.

### **802.1Q Encapsulation**

- **Function:** Adds a tag to Ethernet frames to identify the VLAN to which the frame belongs.
- **Structure:**
    - **Tag Protocol Identifier (TPID):** 16 bits, value 0x8100.
    - **Priority Code Point (PCP):** 3 bits, used for Class of Service (CoS).
    - **Drop Eligible Indicator (DEI):** 1 bit, indicates frames that can be dropped in congestion.
    - **VLAN Identifier (VID):** 12 bits, identifies the VLAN, allows 1 to 4094 VLANs.

### **Trunk Port Configuration**

- **Setting Encapsulation:** On switches supporting both ISL and 802.1Q, encapsulation must be manually set to 802.1Q.
    - **Command:** `switchport trunk encapsulation dot1q`
- **Mode Configuration:**
    - **Command:** `switchport mode trunk`
- **Allowed VLANs:**
    - **Command:** `switchport trunk allowed vlan [add|remove|except|none]`
    - **Default:** All VLANs (1-4094) are allowed.
- **Native VLAN:**
    - **Definition:** The VLAN that sends and receives untagged frames.
    - **Configuration:** `switchport trunk native vlan [vlan_number]`

### **Router on a Stick (ROAS)**

- **Definition:** A method for inter-VLAN routing using a single physical interface on a router with multiple sub-interfaces, each representing a different VLAN.
- **Configuration:**
    - **Sub-interface creation:** `interface g0/0.10` (Sub-interface number typically matches VLAN number)
    - **Encapsulation:** `encapsulation dot1q 10`
    - **IP Address Assignment:** `ip address 192.168.1.1 255.255.255.0`

### **Detailed Review**

1. **What is a Trunk Port?**
    - A trunk port is a switch interface that carries traffic for multiple VLANs, distinguishing them using 802.1Q tags.
    - **Use Case:** Reduces the need for multiple physical connections between switches and routers for each VLAN.
2. **802.1Q Tag Structure**
    - **TPID:** Identifies the frame as tagged with 802.1Q.
    - **PCP:** Prioritizes traffic.
    - **DEI:** Marks frames that can be dropped in congestion.
    - **VID:** Identifies the VLAN.
3. **Trunk Port Configuration Commands**
    - **Setting Encapsulation:** `switchport trunk encapsulation dot1q`
    - **Setting Mode:** `switchport mode trunk`
    - **Allowed VLANs Configuration:**
        - Add VLAN: `switchport trunk allowed vlan add [vlan_list]`
        - Remove VLAN: `switchport trunk allowed vlan remove [vlan_list]`
        - All VLANs: `switchport trunk allowed vlan all`
        - Except: `switchport trunk allowed vlan except [vlan_list]`
        - None: `switchport trunk allowed vlan none`
4. **Router on a Stick Configuration**
    - **Sub-interface Creation:** `interface g0/0.10`
    - **Encapsulation:** `encapsulation dot1q 10`
    - **IP Address:** `ip address 192.168.1.1 255.255.255.0`
    - **Purpose:** Provides a logical separation of networks using a single physical router interface.