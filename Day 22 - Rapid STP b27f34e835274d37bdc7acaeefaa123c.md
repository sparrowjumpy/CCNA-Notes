# Day 22 - Rapid STP

Reviewed: No

### **Key Concepts**

### **Different Versions of Spanning Tree Protocol**

1. **802.1D (Classic STP)**
    - **Original IEEE standard** created to prevent Layer 2 loops.
    - **Single STP instance** for all VLANs (no load balancing).
    - **Slow convergence** (up to 50 seconds).
2. **PVST+ (Per-VLAN Spanning Tree Plus)**
    - **Cisco's enhancement** of 802.1D.
    - **Separate STP instance** for each VLAN, allowing load balancing.
    - **Slow convergence** similar to classic STP.
3. **802.1w (Rapid STP or RSTP)**
    - **Faster convergence** than 802.1D, typically within seconds.
    - **Single STP instance** for all VLANs (no load balancing).
4. **Rapid PVST+**
    - **Cisco's enhancement** of 802.1w.
    - **Separate STP instance** for each VLAN with rapid convergence.
    - **Supports load balancing** by blocking different ports in each VLAN.
5. **802.1s (Multiple Spanning Tree Protocol - MSTP)**
    - **Groups VLANs** into different instances to perform load balancing.
    - **Superior to Cisco's Rapid PVST+** for large networks with many VLANs.
    - **Cisco switches run the industry standard 802.1s** without proprietary modifications.

### **Key Features of Rapid Spanning Tree Protocol (RSTP)**

- **Purpose:** Prevent Layer 2 loops by blocking specific ports.
- **Root Bridge Election:** Same rules as in STP; lowest Bridge ID becomes the root bridge.
- **Root and Designated Ports:** Similar to classic STP, with a focus on the lowest root cost.

### **RSTP Port Roles**

1. **Root Port:**
    - Closest to the root bridge.
    - One per non-root switch.
2. **Designated Port:**
    - Sends the best BPDU on a segment.
    - One per collision domain (segment).
3. **Alternate Port:**
    - A discarding port that receives a superior BPDU from another switch.
    - Functions as a backup to the root port, ready to move to forwarding state if needed.
4. **Backup Port:**
    - A discarding port that receives a superior BPDU from another interface on the same switch.
    - Rarely encountered in modern networks due to the obsolescence of hubs.

### **RSTP Port States**

- **Discarding:** Combines the blocking, listening, and disabled states of classic STP.
- **Learning:** Learns MAC addresses but does not forward frames.
- **Forwarding:** Forwards frames and learns MAC addresses.

### **RSTP Features**

- **Immediate Transition to Forwarding:**
    - **Handshake Mechanism:** Allows rapid transition to the forwarding state.
    - **Built-in Features:** Includes functionalities of classic STP optional features like UplinkFast, BackboneFast, and PortFast.

### **RSTP Link Types**

1. **Edge:**
    - Connected to end hosts.
    - Functions like PortFast, moving directly to forwarding state.
2. **Point-to-Point:**
    - Direct connection between two switches.
    - Operates in full-duplex mode.
3. **Shared:**
    - Connection to a hub.
    - Operates in half-duplex mode (rarely used in modern networks).

### **BPDU Differences in RSTP**

- **Protocol Version:** 2 for RSTP (compared to 0 in classic STP).
- **BPDU Type:** 2 for RSTP.
- **BPDU Flags:** All 8 bits are used in RSTP for faster negotiation and convergence.
- **BPDU Generation:** All switches in RSTP generate their own BPDUs, unlike classic STP where only the root bridge generates BPDUs.

### **Quiz Questions Overview**

1. **IEEE 802.1D Optional Features in 802.1w:**
    - **Correct Answers:** PortFast, UplinkFast, BackboneFast.
    - These features allow rapid port transitions to the forwarding state in RSTP.
2. **Configuring an 802.1w Edge Port:**
    - **Correct Command:** `spanning-tree portfast`.
    - Configures a port connected to end hosts to move directly to the forwarding state.
3. **Identifying Root Bridge, Port Roles, and Link Types:**
    - **Root Bridge:** Switch with the lowest priority.
    - **Port Roles:** Root ports, designated ports, alternate ports, and backup ports.
    - **Link Types:** Edge, point-to-point, and shared.

### **Summary**

- **RSTP:** An evolution of classic STP with faster convergence using negotiation rather than timers.
- **Port Roles and States:** Simplified and optimized for rapid recovery and loop prevention.
- **Link Types:** Introduces the concept of edge, point-to-point, and shared links.
- **Compatibility:** RSTP is compatible with classic STP, with mixed environments possible but slower convergence on classic STP interfaces.

### Commands Used in Day 22 (Rapid Spanning Tree Protocol)

1. **Set RSTP mode on a switch:**
    
    ```
    spanning-tree mode rapid-pvst
    ```
    
    - **Purpose:** Configures the switch to use Rapid PVST+.
2. **Show Spanning Tree information:**
    
    ```
    show spanning-tree
    ```
    
    - **Purpose:** Displays the current spanning tree information, including protocol (RSTP), port roles, and states.
3. **Configure an Edge Port (PortFast):**
    
    ```
    interface [interface_id]
    spanning-tree portfast
    ```
    
    - **Purpose:** Configures a port as an edge port to immediately move to the forwarding state when connected to an end device.
4. **Manually Configure Point-to-Point Link Type:**
    
    ```
    interface [interface_id]
    spanning-tree link-type point-to-point
    ```
    
    - **Purpose:** Explicitly configures an interface as a point-to-point link, typically between two switches.
5. **Manually Configure Shared Link Type:**
    
    ```
    interface [interface_id]
    spanning-tree link-type shared
    ```
    
    - **Purpose:** Configures an interface as a shared link type, usually connected to a hub (though rarely used in modern networks).
6. **Verify Spanning Tree Configuration:**
    
    ```
    show spanning-tree interface [interface_id] detail
    ```
    
    - **Purpose:** Provides detailed information about the spanning tree status of a specific interface, including its role, state, and link type.