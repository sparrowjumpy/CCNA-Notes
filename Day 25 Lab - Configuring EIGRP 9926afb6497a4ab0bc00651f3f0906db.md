# Day 25 Lab - Configuring EIGRP

Reviewed: No

### **Lab Overview:**

- The lab focused on configuring EIGRP (Enhanced Interior Gateway Routing Protocol) in a network setup.
- The goal was to practice EIGRP configuration, understand EIGRP metric calculation, and explore unequal-cost load-balancing—a unique feature of EIGRP.

### **EIGRP Basic Configuration:**

1. **Enabling EIGRP on Routers:**
    - Enter `router eigrp <AS-number>` mode to start configuring EIGRP.
    - Example: `router eigrp 100` (where 100 is the AS number).
    - The AS (Autonomous System) number must match on all routers within the same EIGRP domain to establish neighbor relationships.
2. **Enabling EIGRP on Interfaces:**
    - The `network <network-address> <wildcard-mask>` command activates EIGRP on specified interfaces.
    - Wildcard masks are used to specify the range of addresses on which EIGRP will be enabled.
3. **Wildcard Mask:**
    - A wildcard mask is the inverse of a subnet mask.
    - Example: Subnet mask `255.255.255.240` becomes `0.0.0.15` in wildcard notation.
    - EIGRP uses wildcard masks to determine which interfaces should run EIGRP.
4. **Auto-Summary:**
    - By default, EIGRP may summarize networks into their classful addresses.
    - This behavior can be disabled with the `no auto-summary` command to prevent automatic summarization.
5. **Passive Interface:**
    - The `passive-interface <interface>` command stops EIGRP from sending updates out of an interface that doesn’t have neighbors, reducing unnecessary traffic.
    - Example: `passive-interface l0` (where `l0` is the loopback interface).

### **EIGRP Metric Calculation:**

- **EIGRP Metric Formula:**
    - The EIGRP metric is calculated primarily using bandwidth and delay.
    - **Formula:** Metric = (10^7 / slowest bandwidth) + (sum of delays)
    - EIGRP considers the slowest bandwidth link in the path and the cumulative delay of all links in the path.
- **Feasible Distance (FD):**
    - The Feasible Distance is the total metric value from the local router to the destination network.
    - It’s the sum of the lowest bandwidth and the total delay across all links in the path.
- **Reported Distance (RD):**
    - Also known as Advertised Distance, this is the metric value reported by a neighboring router for a route.
    - It represents the neighbor’s own Feasible Distance to the destination.

### **EIGRP Path Selection and Load-Balancing:**

- **Successor:**
    - The successor is the best route to a destination based on the lowest Feasible Distance.
    - This route is always placed in the routing table.
- **Feasible Successor:**
    - A feasible successor is an alternate route that meets the Feasibility Condition, ensuring it is loop-free.
    - **Feasibility Condition:** A route is considered a feasible successor if its Reported Distance is less than the Feasible Distance of the current successor.
- **Equal-Cost Multi-Path (ECMP) Load-Balancing:**
    - By default, EIGRP performs load-balancing across multiple paths if they have the same metric (equal-cost).
- **Unequal-Cost Load-Balancing:**
    - EIGRP can load-balance across multiple paths with different metrics using the `variance <value>` command.
    - The variance multiplier allows routes with a metric within the specified multiple of the successor’s FD to be used for load-balancing.
    - Example: With a variance of 2, routes with an FD up to twice the successor’s FD will be included in load-balancing.

### **EIGRP Commands and Their Purpose:**

- **`router eigrp <AS-number>`:** Enters EIGRP configuration mode.
- **`network <network-address> <wildcard-mask>`:** Activates EIGRP on specified interfaces.
- **`no auto-summary`:** Disables automatic summarization of networks.
- **`passive-interface <interface>`:** Disables sending EIGRP updates out of a specified interface.
- **`variance <value>`:** Configures EIGRP for unequal-cost load-balancing.

### **Verification Commands:**

- **`show ip protocols`:** Displays routing protocol configurations and statistics.
- **`show ip eigrp neighbors`:** Lists EIGRP neighbors and their status.
- **`show ip route eigrp`:** Shows routes learned via EIGRP in the routing table.
- **`show ip eigrp topology`:** Displays EIGRP topology table, including successors and feasible successors.

### **Key Concepts to Remember:**

- **Metric Calculation:** EIGRP’s metric is based on bandwidth and delay.
- **Successor vs. Feasible Successor:** The successor is the best route, while the feasible successor is a backup route that meets the feasibility condition.
- **Unequal-Cost Load-Balancing:** Unique to EIGRP, allowing multiple routes with different metrics to be used based on the variance command.