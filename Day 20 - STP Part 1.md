# Day 20 - STP Part 1

Reviewed: No

### **Redundancy in Networks**

### **Definition and Importance**

- **Redundancy:** The practice of adding extra components to a network to prevent a single point of failure.
- **Goal:** Ensure network availability and minimize downtime, critical for businesses like e-commerce platforms (e.g., Amazon).
- **Implementation:** Redundancy should be built into all aspects of network design, including devices, connections, and paths.

### **Example: Network Design**

1. **Poor Design:** Single points of failure where a single hardware failure can lead to loss of connectivity.
2. **Better Design:** Multiple paths and connections to ensure that a single failure does not disrupt network operations.
3. **Considerations for Redundancy:** Important devices like servers may have multiple NICs to connect to different switches, whereas typical PCs might have only one NIC.

### **Spanning Tree Protocol (STP)**

### **Purpose and Functionality**

- **Objective:** Prevent Layer 2 loops in a network, which can lead to broadcast storms, network congestion, and MAC address flapping.
- **Broadcast Storms:** Occur when broadcast frames loop endlessly in the network, consuming bandwidth and causing severe congestion.
- **MAC Address Flapping:** Happens when switches repeatedly update their MAC address tables due to frames with the same source MAC address arriving on different interfaces.

### **STP Basics**

1. **IEEE Standard:** 802.1D
2. **Default Behavior:** STP is enabled by default on all switches to prevent Layer 2 loops.
3. **Port States:**
    - **Forwarding:** Ports send and receive normal traffic.
    - **Blocking:** Ports do not send or receive normal traffic but still listen for STP messages (BPDUs).

### **Key STP Concepts**

### **Bridge and BPDUs**

- **Bridge:** In STP terminology, a bridge refers to a switch. The term is historical and stems from early networking equipment.
- **BPDU (Bridge Protocol Data Unit):** Special frames exchanged by switches to share information and maintain a loop-free network topology.

### **STP Operation**

1. **Root Bridge Election:**
    - **Bridge ID:** Combination of bridge priority and MAC address. The switch with the lowest Bridge ID becomes the root bridge.
    - **Bridge Priority:** Default value is 32768. Can be adjusted in increments of 4096.
    - **MAC Address:** Used as a tie-breaker if the bridge priorities are the same.
2. **Bridge ID Structure:**
    - **Original Structure:** 16-bit priority field + 48-bit MAC address.
    - **Updated Structure:** 4-bit bridge priority + 12-bit VLAN ID (extended system ID) + 48-bit MAC address.
    - **PVST (Per-VLAN Spanning Tree):** Runs separate STP instances for each VLAN, using VLAN ID in the bridge ID.
3. **Port Roles:**
    - **Root Ports:** The single port on a non-root bridge with the lowest path cost to the root bridge. Forwarding state.
    - **Designated Ports:** One designated port per collision domain, forwarding state.
    - **Non-Designated Ports:** Blocking state to prevent loops.
4. **Root Port Selection:**
    - **Root Cost:** Calculated as the sum of the path costs from a switch to the root bridge. Lower cost paths are preferred.
    - **Tie-Breakers:** If multiple ports have the same root cost, the switch will select the port connected to the neighbor with the lowest Bridge ID. Further ties are broken using port IDs.

### **STP Path Cost Calculation**

- **Path Cost Values:**
    - **Ethernet (10 Mbps):** Cost 100
    - **Fast Ethernet (100 Mbps):** Cost 19
    - **Gigabit Ethernet (1 Gbps):** Cost 4
    - **10 Gigabit Ethernet:** Cost 2
- **Calculation:** The path cost is the sum of the costs on the path to the root bridge.

### **Port ID**

- **Structure:** 16-bit value composed of an 8-bit priority and an 8-bit port number.
- **Default Priority:** 128
- **Port Number:** Unique identifier for each port on a switch, used as the final tie-breaker in root port selection.

### **Practical Application and Examples**

### **Practice Scenario: Root Bridge and Port Roles**

- **Determine Root Bridge:** The switch with the lowest Bridge ID is selected.
- **Identify Port Roles:** Determine root ports, designated ports, and non-designated (blocking) ports based on STP rules and tie-breakers.

### **Example Network**

1. **Root Bridge Selection:** SW3 has the lowest priority or lowest MAC address if priorities are the same.
2. **Root Port Selection:** Based on the lowest root cost and tie-breakers such as Bridge ID and Port ID.
3. **Designated Ports:** The switch with the lowest root cost to a collision domain will have its port designated. The other port in the collision domain becomes non-designated (blocking).

### **Spanning Tree Protocol Process Summary**

1. **Root Bridge Election:** Switch with the lowest Bridge ID is elected as the root bridge.
2. **Root Port Selection:** Each non-root switch selects one root port, the port with the lowest root cost to the root bridge.
3. **Designated Port Selection:** Each collision domain selects one designated port.
4. **Blocking Ports:** Remaining ports are placed in a blocking state to prevent loops.

### **Commands Used in Day 20**

- **Show Spanning Tree Information:** `show spanning-tree`
- **Configure Bridge Priority:** `spanning-tree vlan [VLAN_ID] priority [PRIORITY]`
- **Enable/Disable PortFast:** `spanning-tree portfast default`
- **Show Interface Details:** `show interface`