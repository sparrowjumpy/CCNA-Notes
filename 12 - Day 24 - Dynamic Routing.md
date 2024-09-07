# Day 24 - Dynamic Routing

Reviewed: No

**Introduction:**

- **Dynamic routing** contrasts with **static routing** by automating the route discovery and path selection processes.
- Instead of manually configuring routes, dynamic routing protocols allow routers to discover and update routes based on network changes.
- This session covers a general overview of dynamic routing protocols, their types, metrics, and administrative distance.

---

**Key Concepts:**

1. **Dynamic Routing Basics:**
    - **Dynamic Routing Protocols**: Allow routers to automatically discover and maintain optimal paths to destination networks.
    - **Benefits**: Automatic updates to routing tables in response to network changes (e.g., link failures).
2. **Network Topology Example:**
    - Four routers (R1, R2, R3, R4) are connected in a network.
    - Without dynamic routing, each router only knows about its directly connected networks.
3. **Dynamic Routing Process:**
    - Routers exchange information about their known routes with neighbors.
    - For example, R4 advertises its connected network (192.168.4.0/24) to R2, which then shares it with R1, and so on.
4. **Routing Table Updates:**
    - When a network change occurs (e.g., a link goes down), dynamic routing protocols automatically update the routing tables to reflect the best available paths.

---

**Types of Dynamic Routing Protocols:**

1. **Interior Gateway Protocols (IGPs)**:
    - Used within a single autonomous system (AS).
    - Examples: OSPF, EIGRP, RIP.
2. **Exterior Gateway Protocols (EGPs)**:
    - Used between different autonomous systems (AS).
    - Example: BGP (Border Gateway Protocol), the only EGP in use today.
3. **Algorithm Types:**
    - **Distance Vector Protocols**: Use simple metrics like hop count. Examples: RIP, EIGRP.
    - **Link State Protocols**: Develop a complete network map and calculate the best paths. Examples: OSPF, IS-IS.
    - **Path Vector Protocols**: Used by EGPs like BGP.

---

**Distance Vector vs. Link State Protocols:**

1. **Distance Vector Protocols**:
    - Operate by sharing route information with directly connected neighbors.
    - Known as “**routing by rumor**” because routers only know about routes their neighbors tell them about.
    - Examples: RIP, EIGRP.
2. **Link State Protocols**:
    - Routers create a complete map of the network.
    - Each router calculates the best routes independently.
    - Requires more CPU and memory resources but provides faster convergence.
    - Examples: OSPF, IS-IS.

---

**Routing Metrics:**

1. **Metric**:
    - A value used by routers to determine the best route to a destination.
    - Lower metrics are preferred.
    - **Different protocols use different metrics**:
        - **RIP**: Hop count.
        - **EIGRP**: Composite metric based on bandwidth and delay (can include other factors).
        - **OSPF**: Cost based on link bandwidth.
        - **IS-IS**: Cost (default is 10 for all links unless manually configured).
2. **Equal Cost MultiPath (ECMP)**:
    - If multiple routes to the same destination have the same metric, both can be added to the routing table, and traffic will be load-balanced between them.

---

**Administrative Distance (AD):**

1. **AD Definition**:
    - A value used to rank the trustworthiness of routes learned via different routing protocols.
    - Lower AD values are preferred.
2. **Common AD Values**:
    - **Connected routes**: 0
    - **Static routes**: 1
    - **eBGP**: 20
    - **EIGRP**: 90
    - **IGRP**: 100
    - **OSPF**: 110
    - **IS-IS**: 115
    - **RIP**: 120
    - **Unusable routes**: 255
3. **Floating Static Routes**:
    - Static routes with a higher AD than dynamic routes, used as backups if the dynamic route fails.

---

**Quiz Review:**

1. **AD Comparison**:
    - When routes from different protocols compete, the route with the lower AD is chosen.
    - Example: EIGRP (AD 90) is preferred over OSPF (AD 110).
2. **Longest Prefix Match**:
    - When multiple routes to the same destination exist, the route with the longest prefix match (most specific) is chosen.

---

**Summary of Key Commands:**

- **`SHOW IP ROUTE**: Displays the current routing table, including metrics and AD.`
- **`IP ROUTE <destination> <mask> <next-hop>**: Configures a static route.`
- **`IP ROUTE <destination> <mask> <next-hop> [AD]**: Configures a floating static route with a specified AD.`