# Day 36 - CDP & LLDP

Reviewed: No

### **1. Introduction to Layer 2 Discovery Protocols**

- **Purpose:** Used to share information between directly connected devices, such as hostname, IP address, and device type.
- **Layer 2 Operation:** These protocols function at Layer 2, meaning they don't use IP addresses.
- **Protocols:**
    - **CDP (Cisco Discovery Protocol):** Cisco proprietary protocol.
    - **LLDP (Link Layer Discovery Protocol):** Industry-standard protocol, IEEE 802.1AB.

### **2. CDP (Cisco Discovery Protocol)**

- **Default State:**
    - Enabled by default on Cisco devices (routers, switches, firewalls, IP phones).
    - Uses multicast MAC address `0100.0CCC.CCCC`.
- **Message Timers:**
    - **Message Interval:** 60 seconds.
    - **Holdtime:** 180 seconds (entry removed if no message is received in this time).
    - **Version:** CDP v2 is used by default.

### **CDP CLI Commands:**

- **View CDP Status:**
    - `show cdp` – Shows CDP status, including message interval and holdtime.
    - `show cdp traffic` – Displays CDP packet statistics.
    - `show cdp interface` – Shows CDP status per interface, including message timer and holdtime.
- **View Neighbor Information:**
    - `show cdp neighbors` – Lists CDP neighbors and their details.
    - **Columns:**
        - **Device ID:** Hostname of the neighbor.
        - **Local Interface:** Interface on this device (e.g., G0/0).
        - **Holdtime:** Time before the neighbor is removed.
        - **Capabilities:** Type of device (e.g., R for Router, S for Switch).
        - **Platform:** Model of the neighboring device.
        - **Port ID:** Interface on the neighboring device.
- **Detailed Neighbor Information:**
    - `show cdp neighbors detail` – Displays additional details like software version, IP address, native VLAN, and duplex settings.
    - `show cdp entry <neighbor>` – Shows detailed information for a specific neighbor.

### **CDP Configuration Commands:**

- **Enable/Disable CDP:**
    - **Global:** `cdp run` to enable, `no cdp run` to disable.
    - **Interface:** `cdp enable` to enable, `no cdp enable` to disable.
- **Configure Timers:**
    - **Message Timer:** `cdp timer <seconds>` (default 60).
    - **Holdtime:** `cdp holdtime <seconds>` (default 180).

### **3. LLDP (Link Layer Discovery Protocol)**

- **LLDP Overview:**
    - Industry-standard protocol supported by various vendors (Cisco, Juniper, Palo Alto).
    - Disabled by default on Cisco devices.
    - **Multicast MAC Address:** `0180.C200.000E`.
    - **Message Interval:** 30 seconds.
    - **Holdtime:** 120 seconds.
- **Additional Timer:**
    - **Reinitialization Timer:** Prevents rapid enable/disable (default 2 seconds).

### **LLDP CLI Commands:**

- **View LLDP Status:**
    - `show lldp` – Shows LLDP status and timers.
    - `show lldp traffic` – Displays LLDP packet statistics.
    - `show lldp interface` – Shows LLDP status for each interface (Tx and Rx).
- **View Neighbor Information:**
    - `show lldp neighbors` – Lists LLDP neighbors.
    - `show lldp neighbors detail` – Displays detailed neighbor information, similar to CDP.
    - `show lldp entry <neighbor>` – Shows detailed information for a specific LLDP neighbor.

### **LLDP Configuration Commands:**

- **Enable/Disable LLDP:**
    - **Global:** `lldp run` to enable, `no lldp run` to disable.
    - **Interface:**
        - `lldp transmit` – Enable transmission of LLDP messages.
        - `lldp receive` – Enable reception of LLDP messages.
- **Configure Timers:**
    - **Message Timer:** `lldp timer <seconds>` (default 30).
    - **Holdtime:** `lldp holdtime <seconds>` (default 120).
    - **Reinitialization Timer:** `lldp reinit <seconds>` (default 2).

### **4. CDP vs. LLDP:**

- **CDP:** Cisco proprietary, enabled by default on Cisco devices, shares more detailed information (e.g., VTP settings).
- **LLDP:** Industry-standard, requires manual configuration on Cisco devices, compatible with non-Cisco devices.

### **5. Best Practices:**

- **Security Risk:** Both protocols can share sensitive network information (hostname, IP, etc.). Many admins disable them to reduce security risks.
- **Use Cases:** CDP is useful in all-Cisco environments, while LLDP is necessary in multi-vendor environments.

### **6. Wireshark Captures:**

- **CDP Capture:** Shows the multicast MAC address, CDP version, and detailed device information.
- **LLDP Capture:** Shows similar information but uses a different multicast MAC address and slightly different fields.

### **Quiz Summary:**

1. **CDP Timers:**
    - Commands: `show cdp` and `show cdp interface` display CDP timers.
2. **CDP Default State:**
    - CDP enabled on interfaces by default (`cdp enable`) and uses a 60-second message timer.
3. **LLDP Capabilities:**
    - A multilayer switch (SW1) shows system capabilities `B, R` (Bridge and Router).
4. **LLDP Configuration:**
    - LLDP requires separate `lldp transmit` and `lldp receive` commands for each interface.
    - LLDP can be used to discover the OS version of a neighboring device.