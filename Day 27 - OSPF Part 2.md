# Day 27 - OSPF Part 2

Reviewed: No

### **1. OSPF Metric (Cost):**

- **OSPF Cost Calculation:**
    - OSPF’s metric is called **cost**.
    - **Default Reference Bandwidth:** 100 Mbps.
    - **Formula:** Cost = Reference Bandwidth / Interface Bandwidth.
        - **Ethernet (10 Mbps):** Cost = 100 / 10 = 10.
        - **FastEthernet (100 Mbps):** Cost = 100 / 100 = 1.
        - **Gigabit Ethernet (1000 Mbps):** Cost = 100 / 1000 = 1 (Values less than 1 are rounded to 1).
        - **10 Gigabit Ethernet (10,000 Mbps):** Cost = 100 / 10,000 = 1.
- **Changing the Reference Bandwidth:**
    - **Command:** `auto-cost reference-bandwidth <value>` (in OSPF configuration mode).
    - This command adjusts the reference bandwidth, allowing more accurate cost calculation for high-speed interfaces.
    - Example: Setting reference bandwidth to 100,000 (100 Gbps) for future-proofing.
    - **Important:** Ensure the reference bandwidth is consistent across all routers in the OSPF network.
- **Manual Cost Configuration:**
    - **Command:** `ip ospf cost <value>` (in interface configuration mode).
    - This command manually sets the cost of an interface, overriding the auto-calculated cost.
- **Changing Interface Bandwidth:**
    - **Command:** `bandwidth <value>` (in kilobits per second, in interface configuration mode).
    - This affects OSPF cost calculation and other metrics like EIGRP but does not change the actual interface speed.
- **Summary:**
    - Three methods to modify OSPF cost:
        1. Change the reference bandwidth (`auto-cost reference-bandwidth`).
        2. Manually configure interface cost (`ip ospf cost`).
        3. Change the interface bandwidth (`bandwidth`), though not recommended for OSPF.

### **2. OSPF Neighbor States:**

- **OSPF Neighbor Process Overview:**
    - OSPF routers must go through several states to become neighbors and establish a full adjacency.
- **Neighbor States:**
    1. **Down State:** The router hasn’t received any OSPF Hello packets from its neighbor.
    2. **Init State:** The router has received a Hello packet but hasn’t seen its own Router ID in the neighbor’s Hello packet.
    3. **2-Way State:** Routers see each other’s Router ID in their Hello packets, indicating bidirectional communication.
        - **DR/BDR Election:** Occurs in certain network types during this state (will be covered in Day 28).
    4. **Exstart State:** Routers determine which will be the Master and which will be the Slave for the LSDB exchange.
    5. **Exchange State:** Routers exchange DBD (Database Description) packets listing the LSAs in their LSDB.
    6. **Loading State:** Routers request missing LSAs from each other using LSR (Link State Request) packets.
        - LSUs (Link State Updates) are used to send the requested LSAs, and LSAcks acknowledge receipt.
    7. **Full State:** The routers have identical LSDBs and a full OSPF adjacency.
- **Key Points:**
    - **Hello Timer:** Default is 10 seconds on Ethernet connections.
    - **Dead Timer:** Default is 40 seconds. If no Hello is received within this time, the neighbor is considered down.
- **OSPF Message Types:**
    - **Hello:** Establishes and maintains neighbor relationships. (Type 1)
    - **DBD:** Contains a summary of LSAs in the LSDB. (Type 2)
    - **LSR:** Requests specific LSAs from a neighbor. (Type 3)
    - **LSU:** Sends the requested LSAs. (Type 4)
    - **LSAck:** Acknowledges receipt of LSAs. (Type 5)

### **3. Additional OSPF Configurations:**

- **Enabling OSPF Directly on an Interface:**
    - **Command:** `ip ospf <process-id> area <area-id>` (in interface configuration mode).
    - This method doesn’t require the `network` command and activates OSPF on the specified interface directly.
- **Configuring Passive Interfaces:**
    - **Command:** `passive-interface default` (in OSPF configuration mode).
    - Makes all interfaces passive by default. Use `no passive-interface <interface>` to allow specific interfaces to send OSPF Hello packets.

### **4. Review and Summary:**

- **OSPF Metric (Cost):**
    - Understand how cost is calculated and the methods to modify it (reference bandwidth, manual cost, interface bandwidth).
- **OSPF Neighbor States:**
    - Memorize the sequence of neighbor states and understand the key functions and message types involved.
- **Additional Configurations:**
    - Be familiar with alternative methods for enabling OSPF on interfaces and configuring passive interfaces.