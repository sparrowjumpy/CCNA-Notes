# Day 21 - STP Part 2

Reviewed: No

### **Spanning Tree Port States and Timers**

### **Port States**

1. **Blocking State**
    - **Purpose:** Prevents loops by blocking non-designated ports.
    - **Characteristics:**
        - No regular traffic sent/received.
        - Receives but does not forward BPDUs.
        - Does not learn MAC addresses.
2. **Listening State**
    - **Purpose:** Transitional state before forwarding.
    - **Duration:** 15 seconds (default, determined by Forward Delay timer).
    - **Characteristics:**
        - Only processes BPDUs.
        - Does not send/receive regular traffic.
        - Does not learn MAC addresses.
3. **Learning State**
    - **Purpose:** Prepares for forwarding by learning MAC addresses.
    - **Duration:** 15 seconds (default, determined by Forward Delay timer).
    - **Characteristics:**
        - Only processes BPDUs.
        - Does not send/receive regular traffic.
        - Learns MAC addresses.
4. **Forwarding State**
    - **Purpose:** Normal operation for sending/receiving traffic.
    - **Characteristics:**
        - Sends/receives BPDUs and regular traffic.
        - Learns MAC addresses.
5. **Disabled State**
    - **Purpose:** Administratively shutdown port, not involved in STP.
    - **Characteristics:**
        - Does not participate in STP or forward traffic.

### **Spanning Tree Timers**

1. **Hello Timer**
    - **Function:** Interval at which the root bridge sends BPDUs.
    - **Default Value:** 2 seconds.
    - **Importance:** Maintains topology information and updates other switches.
2. **Forward Delay Timer**
    - **Function:** Duration of Listening and Learning states.
    - **Default Value:** 15 seconds each.
    - **Importance:** Ensures safe transition to Forwarding state without causing loops.
3. **Max Age Timer**
    - **Function:** Duration a switch will wait without receiving a BPDU before recalculating STP topology.
    - **Default Value:** 20 seconds.
    - **Importance:** Ensures network stability by maintaining current topology until a change is confirmed.

### **Spanning Tree Protocol Data Unit (BPDU)**

- **Fields and Importance:**
    - **Destination MAC Address:** Identifies BPDU frames.
        - **PVST+:** 0100.0ccc.cccd
        - **Regular STP:** 0180.c200.0000
    - **Root Identifier:** Contains root bridge priority, VLAN ID, and MAC address.
    - **Root Path Cost:** Path cost from the switch to the root bridge.
    - **Bridge Identifier:** Bridge ID of the sending switch.
    - **Port Identifier:** Identifies the port that sent the BPDU.
    - **Timers:** Message Age, Max Age, Hello, Forward Delay.

### **Optional Spanning Tree Features (Spanning Tree Toolkit)**

1. **PortFast**
    - **Function:** Allows ports connected to end hosts to skip Listening and Learning states.
    - **Purpose:** Reduces the delay for end hosts to access the network.
    - **Configuration:** `spanning-tree portfast` on interfaces or `spanning-tree portfast default` globally.
2. **BPDU Guard**
    - **Function:** Disables ports that receive BPDUs, preventing potential loops.
    - **Configuration:**
        - **Interface Level:** `spanning-tree bpduguard enable`
        - **Global Level:** `spanning-tree portfast bpduguard default`
3. **Root Guard**
    - **Function:** Prevents an interface from becoming the root bridge by ignoring superior BPDUs.
    - **Purpose:** Maintains the intended STP topology.
4. **Loop Guard**
    - **Function:** Prevents a port from moving to the Forwarding state if it stops receiving BPDUs.
    - **Purpose:** Prevents loops caused by unidirectional links.

### **Spanning Tree Configuration**

1. **Setting the Spanning Tree Mode**
    - **Command:** `spanning-tree mode [pvst|rapid-pvst|mst]`
    - **PVST:** Classic STP with Cisco’s per-VLAN addition.
    - **Rapid-PVST:** Improved version, default on modern Cisco switches.
2. **Configuring the Root Bridge**
    - **Primary Root:** `spanning-tree vlan [vlan_number] root primary`
    - **Secondary Root:** `spanning-tree vlan [vlan_number] root secondary`
    - **Manually Setting Priority:** `spanning-tree vlan [vlan_number] priority [priority_value]`
3. **Spanning Tree Port Configuration**
    - **Cost:** `spanning-tree [vlan vlan_number] cost [cost_value]`
    - **Port Priority:** `spanning-tree [vlan vlan_number] port-priority [priority_value]`