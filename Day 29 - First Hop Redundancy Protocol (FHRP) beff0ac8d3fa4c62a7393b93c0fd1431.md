# Day 29 - First Hop Redundancy Protocol (FHRP)

Reviewed: No

### **1. Introduction to FHRPs:**

- **Purpose:**
    - FHRPs ensure that hosts in a network have a redundant default gateway in case the primary gateway fails.
    - FHRPs allow multiple routers to back up a single gateway IP address, so if the primary router fails, another router takes over without any disruption.
- **Common FHRPs for CCNA:**
    - **HSRP (Hot Standby Router Protocol)** - Cisco proprietary.
    - **VRRP (Virtual Router Redundancy Protocol)** - Open standard.
    - **GLBP (Gateway Load Balancing Protocol)** - Cisco proprietary.

### **2. How FHRPs Work:**

- **Virtual IP and MAC Addresses:**
    - FHRPs use a **Virtual IP (VIP)** address that is shared between routers. Hosts on the network use this VIP as their default gateway.
    - A **Virtual MAC Address** is also used to respond to ARP requests.
- **Router Roles:**
    - **Active Router (HSRP)/Master Router (VRRP):**
        - This router handles all traffic for the VIP.
    - **Standby Router (HSRP)/Backup Router (VRRP):**
        - This router takes over if the active router fails.
- **ARP and Gratuitous ARP:**
    - **ARP Requests:** Sent by hosts to find out the MAC address corresponding to the VIP.
    - **Gratuitous ARP:** Sent by the standby router when it takes over to update the MAC address tables in switches, ensuring traffic is directed correctly.

### **3. Specific FHRPs Overview:**

- **HSRP (Hot Standby Router Protocol):**
    - **Cisco Proprietary:** Runs only on Cisco devices.
    - **Versions:**
        - **HSRP Version 1:** Uses multicast address `224.0.0.2`.
        - **HSRP Version 2:** Uses multicast address `224.0.0.102`, adds support for IPv6 and more groups.
    - **Virtual MAC Address Format:**
        - **Version 1:** `0000 0c07 acXX` (XX is the group number in hexadecimal).
        - **Version 2:** `0000 0c9F FXXX` (XXX is the group number in hexadecimal).
    - **Preemption:** Can be enabled to allow a router with a higher priority to take over as the active router when it comes back online. Command: `standby <group-number> preempt`
- **VRRP (Virtual Router Redundancy Protocol):**
    - **Open Standard:** Can be used on any device that supports it.
    - **Roles:**
        - **Master:** Equivalent to the active router.
        - **Backup:** Equivalent to the standby router.
    - **Multicast Address:** `224.0.0.18`.
    - **Virtual MAC Address Format:** `0000 5e00 01XX` (XX is the group number in hexadecimal).
- **GLBP (Gateway Load Balancing Protocol):**
    - **Cisco Proprietary:** Runs only on Cisco devices.
    - **Load Balancing:** Can load balance traffic across multiple routers in the same subnet.
    - **Roles:**
        - **AVG (Active Virtual Gateway):** Manages the assignment of virtual MAC addresses to routers (AVFs).
        - **AVF (Active Virtual Forwarder):** Forwards traffic for a portion of the hosts in the subnet.
    - **Multicast Address:** `224.0.0.102` (same as HSRP v2).
    - **Virtual MAC Address Format:** `0007 b400 XXXXYY` (XXXX is the group number and YY is the AVF number in hexadecimal).
    
    ![image.png](Day%2029%20-%20First%20Hop%20Redundancy%20Protocol%20(FHRP)%20beff0ac8d3fa4c62a7393b93c0fd1431/image.png)
    

### **4. Basic Configuration of HSRP:**

- **Commands:**
    - `standby version 2`: Configures HSRP version 2.
    - `standby <group-number> ip <virtual-ip>`: Sets the virtual IP address for the HSRP group.
    - `standby <group-number> priority <value>`: Sets the priority for the router (default is 100).
    - `standby <group-number> preempt`: Enables preemption, allowing a router with a higher priority to take over as the active router.
- **Example Configuration for R1:**
    
    ```
    interface GigabitEthernet0/0
     standby version 2
     standby 1 ip 172.16.0.254
     standby 1 priority 200
     standby 1 preempt
    ```
    
- **Example Configuration for R2:**
    
    ```
    interface GigabitEthernet0/0
     standby version 2
     standby 1 ip 172.16.0.254
    ```
    

### **5. Summary and Key Points:**

- **HSRP, VRRP, and GLBP** are the three FHRPs to know for the CCNA.
- **HSRP and GLBP** are Cisco proprietary, while **VRRP** is an open standard.
- **HSRP** uses terms like **Active** and **Standby**, while **VRRP** uses **Master** and **Backup**.
- **GLBP** can load balance within a single subnet, while HSRP and VRRP cannot.
- **Preemption** allows a router with a higher priority to take over as the active router.
- **Gratuitous ARP** is used to update MAC address tables when the active router changes.

---

### **Commands Used in Day 29:**

1. **Configure HSRP Version 2:**`standby version 2`
2. **Set the Virtual IP Address:**`standby <group-number> ip <virtual-ip>`
3. **Set Priority:**`standby <group-number> priority <value>`
4. **Enable Preemption:**`standby <group-number> preempt`
5. **Verify HSRP Configuration:**`show standby`