# Day 26 - OSPF Part 1

Reviewed: No

### **Introduction to OSPF (Open Shortest Path First):**

- **OSPF Overview:**
    - OSPF is the only dynamic routing protocol explicitly listed in the CCNA exam topics.
    - It’s a Link State protocol, meaning routers create a complete map of the network using a process called the Shortest Path First (SPF) algorithm.
    - The algorithm was created by Dutch computer scientist Edsger Dijkstra, and it's also known as Dijkstra’s algorithm.
    - There are three versions of OSPF:
        - Version 1 (1989) – no longer in use.
        - Version 2 (1998) – commonly used in IPv4 networks.
        - Version 3 – developed for IPv6 but can also be used for IPv4.
- **OSPF Concepts:**
    - **Link State Advertisements (LSAs):** Routers advertise information about their connected networks using LSAs.
    - **Link State Database (LSDB):** LSAs are organized in the LSDB, which is identical across all routers in the OSPF area.
    - **Flooding:** LSAs are flooded across the network until all routers in the area have the same LSDB.
    - **SPF Algorithm:** Each router independently calculates the best route to each destination using the SPF algorithm.

### **OSPF Areas:**

- **Single-Area vs. Multi-Area OSPF:**
    - **Single-Area OSPF:** Suitable for small networks. All routers are in a single area (usually area 0, the backbone area).
    - **Multi-Area OSPF:** Necessary for larger networks to avoid the negative effects of a large single-area network (e.g., increased SPF calculation time, higher memory usage).
- **Important OSPF Terms:**
    - **Area:** A set of routers and links that share the same LSDB.
    - **Backbone Area (Area 0):** The core area in OSPF, to which all other areas must connect.
    - **Internal Router:** A router with all interfaces in the same OSPF area.
    - **Area Border Router (ABR):** A router with interfaces in multiple OSPF areas, acting as a border between areas. ABRs maintain a separate LSDB for each area.
    - **Backbone Router:** A router connected to the backbone area (Area 0).
    - **Intra-Area Route:** A route to a destination within the same OSPF area.
    - **Interarea Route:** A route to a destination in a different OSPF area.
- **OSPF Area Rules:**
    - **Contiguous Areas:** Each area should be connected (contiguous), not split up into non-contiguous sections.
    - **ABR Connection to Area 0:** All non-backbone areas must have an ABR connected to Area 0.
    - **Interfaces in the Same Subnet:** Interfaces in the same subnet must be in the same OSPF area to become neighbors.

### **Basic OSPF Configuration:**

- **Configuring OSPF:**
    - Enter OSPF configuration mode using `router ospf <process-id>`.
        - The process ID is locally significant and doesn’t need to match between routers.
    - Use the `network <network-address> <wildcard-mask> area <area-id>` command to activate OSPF on interfaces within the specified area.
- **Passive Interface:**
    - Use `passive-interface <interface>` to prevent sending OSPF hello packets out of an interface, while still advertising the subnet.
- **Advertising a Default Route in OSPF:**
    - Configure a default route using `ip route 0.0.0.0 0.0.0.0 <next-hop>`.
    - Advertise the default route into OSPF using the `default-information originate` command.

### **Verification Commands and Concepts:**

- **`show ip protocols`:**
    - Displays information about the OSPF process, including router ID, number of areas, and OSPF neighbors.
    - The router ID is determined by the highest IP address on a loopback interface, the highest IP address on a physical interface, or manually configured using `router-id <id>`.
    - **Autonomous System Boundary Router (ASBR):** A router that connects the OSPF network to an external network.
    - **Administrative Distance (AD):** The default AD for OSPF is 110, which can be changed using the `distance <distance>`  command.
    - Configure the **maximum number of paths** an OSPF router will use to perform ECMP load-balancing: `maximum-paths <number>`
    - **Reset** the OSPF process on the local router: `clear ip ospf process`
    - Manually configure the OSPF **router ID**: `router-id <a.b.c.d>`