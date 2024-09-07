# Day 23 - EtherChannel

Reviewed: No

**Introduction:**

- **EtherChannel** allows grouping multiple physical interfaces into a single logical interface.
- Benefits include increased bandwidth, redundancy, and simplified management.
- The CCNA exam requires understanding how to configure and verify both Layer 2 and Layer 3 EtherChannels using the **Link Aggregation Control Protocol (LACP)**.

---

**Key Concepts:**

1. **Problem Solved by EtherChannel:**
    - Adding multiple links between switches without EtherChannel leads to only one link being active due to **Spanning Tree Protocol (STP)**, which disables other links to prevent Layer 2 loops.
    - **EtherChannel** solves this by grouping multiple physical interfaces, treating them as a single logical interface, which STP then treats as one interface.
2. **EtherChannel Functionality:**
    - **EtherChannel** is represented in network diagrams by a circle around grouped interfaces.
    - Traffic is **load-balanced** across the physical interfaces in the EtherChannel using an algorithm based on “flows” between nodes.
    - **Load balancing inputs** can be the source MAC address, destination MAC address, source IP address, destination IP address, or both source and destination MAC/IP addresses.

---

**EtherChannel Load Balancing:**

- **Flow-Based Load Balancing:** Traffic in the same flow uses the same physical interface to avoid out-of-order packet delivery.
- **Load Balancing Methods:**
    - **Source MAC Address**
    - **Destination MAC Address**
    - **Source and Destination MAC Addresses**
    - **Source IP Address**
    - **Destination IP Address**
    - **Source and Destination IP Addresses**
- **Changing Load-Balancing Method:**
    - Use the command `PORT-CHANNEL LOAD-BALANCE <method>` in global configuration mode.
    - Example: `PORT-CHANNEL LOAD-BALANCE src-dst-mac`.

---

**EtherChannel Configuration Methods:**

1. **PAgP (Port Aggregation Protocol):**
    - Cisco proprietary protocol.
    - **Modes:**
        - **Desirable:** Actively negotiates the formation of an EtherChannel.
        - **Auto:** Forms an EtherChannel if the other side is set to desirable.
2. **LACP (Link Aggregation Control Protocol):**
    - IEEE 802.3ad standard.
    - **Preferred method** due to cross-vendor compatibility.
    - **Modes:**
        - **Active:** Actively negotiates the formation of an EtherChannel.
        - **Passive:** Forms an EtherChannel if the other side is set to active.
3. **Static EtherChannel:**
    - No negotiation protocol is used.
    - Interfaces are manually configured to form an EtherChannel using the `on` mode.

---

**Commands for EtherChannel:**

- **SHOW Commands:**
    - `SHOW ETHERCHANNEL LOAD-BALANCE`: Displays the current load-balancing method.
    - `SHOW ETHERCHANNEL SUMMARY`: Displays a summary of all EtherChannels on the switch, including status flags for both port-channel interfaces and physical member interfaces.
    - `SHOW ETHERCHANNEL PORT-CHANNEL`: Provides more detailed information about the port-channel interfaces.
    - `SHOW INTERFACES TRUNK`: Verifies the trunk status of the port-channel interface.
    - `SHOW RUNNING-CONFIG`: Checks configurations applied to both port-channel and physical interfaces.
- **Configuration Commands:**
    - `INTERFACE RANGE <range>`: Configures multiple interfaces at once.
    - `CHANNEL-GROUP <number> MODE <mode>`: Configures interfaces to be part of an EtherChannel. Mode options include `desirable`, `auto`, `active`, `passive`, and `on`.
    - `CHANNEL-PROTOCOL <protocol>`: Manually sets the EtherChannel protocol (LACP or PAgP) but is generally unnecessary.
    - `NO SWITCHPORT`: Configures Layer 3 EtherChannel by converting interfaces to routed ports.
    - `INTERFACE PORT-CHANNEL <number>`: Enters the configuration mode for the virtual port-channel interface to configure additional settings like IP addressing or trunking.

---

**Layer 3 EtherChannel:**

- **Configuration:**
    - Convert physical interfaces to routed ports using `NO SWITCHPORT`.
    - Create the EtherChannel with the `CHANNEL-GROUP` command.
    - Configure the IP address on the port-channel interface.
    - Example commands:
        - `INTERFACE RANGE <range>`
        - `NO SWITCHPORT`
        - `CHANNEL-GROUP <number> MODE <mode>`
        - `INTERFACE PORT-CHANNEL <number>`
        - `IP ADDRESS <address> <subnet>`
- **Verification:**
    - `SHOW ETHERCHANNEL SUMMARY` will display the Layer 3 EtherChannel with an `R` flag, indicating it’s a routed port-channel.

---

**Summary of Key Commands:**

- `PORT-CHANNEL LOAD-BALANCE <method>`: Configures load-balancing method.
- `SHOW ETHERCHANNEL LOAD-BALANCE`: Displays load-balancing method.
- `CHANNEL-GROUP <number> MODE <mode>`: Configures EtherChannel on interfaces.
- `SHOW ETHERCHANNEL SUMMARY`: Summary of EtherChannel status.
- `SHOW ETHERCHANNEL PORT-CHANNEL`: Detailed EtherChannel information.
- `NO SWITCHPORT`: Converts interfaces to Layer 3 for Layer 3 EtherChannel.
- `INTERFACE PORT-CHANNEL <number>`: Configures the port-channel interface.