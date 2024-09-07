# Day 18 - VLANs Part 3

Reviewed: No

### **Dynamic Trunking Protocol (DTP)**

- **Purpose:** Automatically negotiates switchport status (access or trunk) between Cisco switches.
- **Enabled by Default:** On all Cisco switch interfaces.
- **Modes:**
    - **Dynamic Desirable:** Actively tries to form a trunk with another switch.
    - **Dynamic Auto:** Passive mode; forms a trunk if the other end is actively trying.

### **Key Concepts and Commands**

1. **DTP Modes Explained:**
    - **Dynamic Desirable:** Forms a trunk if the connected port is in trunk, dynamic desirable, or dynamic auto mode.
    - **Dynamic Auto:** Forms a trunk if the connected port is in trunk or dynamic desirable mode.
    - **Manual Configuration:** Recommended to disable DTP for security purposes.
    - **`switchport mode dynamic`:** Command to configure DTP mode.
    - **`show interfaces switchport`:** Displays administrative and operational mode details.
2. **Scenarios and Outputs:**
    - **Dynamic Desirable + Trunk:** Forms a trunk.
    - **Dynamic Auto + Trunk:** Forms a trunk.
    - **Dynamic Auto + Dynamic Auto:** Operates as access ports.
    - **Trunk + Access:** Misconfiguration; should not occur in a real network.
3. **DTP Security Considerations:**
    - **Disabling DTP:** Recommended on all interfaces to prevent potential exploits.
    - **`switchport nonegotiate`:** Stops sending DTP frames, effectively disabling DTP on the interface.
4. **Trunk Encapsulation:**
    - **Dot1q vs. ISL:** Trunk encapsulation can be negotiated, with ISL favored if both support it.
    - **DTP Frames:** Sent in VLAN1 (ISL) or native VLAN (dot1q).

### **VLAN Trunking Protocol (VTP)**

- **Purpose:** Centralizes VLAN management, synchronizes VLAN databases across multiple switches.
- **Modes:**
    - **Server:** Default mode; can add, modify, and delete VLANs.
    - **Client:** Cannot modify VLANs; syncs database from server.
    - **Transparent:** Does not participate in VTP domain synchronization; forwards VTP advertisements.

### **Key Concepts and Commands**

1. **VTP Modes Explained:**
    - **Server Mode:** Stores VLAN database in NVRAM, advertises VLANs.
    - **Client Mode:** Syncs VLAN database from server, does not store in NVRAM (except VTPv3).
    - **Transparent Mode:** Maintains independent VLAN database, forwards VTP advertisements without syncing.
2. **VTP Configuration:**
    - **VTP Domain:** Must be the same across switches to sync VLANs.
    - **VTP Version:** Versions 1, 2, and 3; version 3 supports extended VLANs (1006-4094).
    - **`show vtp status`:** Displays VTP domain name, mode, version, revision number, etc.
3. **VTP Synchronization and Risks:**
    - **Revision Number:** Key factor in synchronization; the highest number indicates the most up-to-date VLAN database.
    - **Risk of Old Switches:** Connecting an old switch with a higher revision number can overwrite the network's VLAN database, causing loss of connectivity.
4. **VTP Management:**
    - **Resetting Revision Number:** Change the domain name or set the switch to transparent mode.
    - **Danger of VTP:** Caution needed when adding new switches to prevent unintentional network disruption.

### **Review and Summary**

- **DTP:** Enables dynamic negotiation of trunk/access ports; should be disabled for security.
- **VTP:** Centralized VLAN management; rarely used due to potential risks.
- **Commands Overview:**
    - **DTP Commands:** `switchport mode dynamic`, `switchport nonegotiate`, `show interfaces switchport`
    - **VTP Commands:** `vtp mode`, `vtp domain`, `show vtp status`

### **Commands Used in Day 19**

- **DTP:**
    - `switchport mode dynamic desirable`
    - `switchport mode dynamic auto`
    - `switchport mode access`
    - `switchport mode trunk`
    - `switchport nonegotiate`
    - `show interfaces switchport`
- **VTP:**
    - `vtp mode server`
    - `vtp mode client`
    - `vtp mode transparent`
    - `vtp domain [name]`
    - `show vtp status`
    - `show vlan brief`
