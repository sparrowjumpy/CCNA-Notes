# Day 35 - Extended ACLs

Reviewed: No

### **1. Introduction to Extended ACLs:**

- **Extended ACLs vs. Standard ACLs:**
    - Extended ACLs offer more granular control than standard ACLs.
    - They can filter traffic based on multiple parameters including source and destination IP addresses, Layer 4 protocol (TCP, UDP), and port numbers.
- **Numbered and Named ACLs:**
    - Extended ACLs can be either numbered or named.
    - Numbered ACLs use ranges 100-199 and 2000-2699.
    - Named ACLs are configured similarly but offer enhanced editing capabilities.

### **2. Configuring Numbered ACLs in Named Mode:**

- **Benefits:**
    - **Easier Editing:** You can delete individual entries using `NO <sequence number>`.
    - **Insert Entries:** New entries can be inserted at specific positions using sequence numbers.
    - **Resequencing:** Sequence numbers can be adjusted to create gaps for future entries.
- **Commands:**
    - **Configuring ACL:** `ip access-list standard <ACL_ID>`
    - **Deleting an Entry:** `no <sequence number>`
    - **Resequencing:** `ip access-list resequence <ACL_ID> <start sequence> <increment>`
    - **Example:**
        
        ```
        ip access-list resequence 1 10 10 
        
        // sequencing now in 10, 20, 30 etc.
        ```
        

### **3. Extended ACL Configuration:**

- **Command Structure:**
    - **Global Config Mode (Numbered):** `access-list <number> {permit | deny} <protocol> <source IP> <wildcard mask> <destination IP> <wildcard mask>`
    - **Named ACL Config Mode:** `ip access-list extended <name>`
    - **Example:**
        
        ```
        deny tcp any host 10.0.1.1 eq 80
        ```
        
- **Matching Criteria:**
    - **Protocol:** TCP, UDP, ICMP, IP, etc.
    - **Source IP and Port:** Specify source IP, wildcard mask, and port (if needed).
    - **Destination IP and Port:** Specify destination IP, wildcard mask, and port (if needed).
    - **Port Matching Options:**
        - `eq`: Equal to
        - `gt`: Greater than
        - `lt`: Less than
        - `neq`: Not equal to
        - `range`: Range of ports

### **4. Advanced Extended ACL Features:**

- **Layer 4 Matching:**
    - Match based on TCP or UDP port numbers.
    - Example:
        
        ```
        deny tcp any host 10.0.1.1 eq 443
        ```
        
- **Additional Matching Options:**
    - **TCP Flags:** ACK, SYN, FIN
    - **TTL:** Time to live value in the IPv4 header.
    - **DSCP:** Differentiated services code point value.

### **5. Best Practices for Applying ACLs *(*RULES OF THUMB)**:**

- **Standard ACLs:** Apply close to the destination.
- **Extended ACLs:** Apply close to the source to prevent unwanted traffic from traversing the network.

### **6. Example Scenarios:**

- **Scenario 1:**
    - **Requirement:** Hosts in `192.168.1.0/24` cannot use HTTPS to access `SRV1`.
    - **Solution:**
        
        ```
        deny tcp 192.168.1.0 0.0.0.255 host 10.0.1.100 eq 443
        permit ip any any
        ```
        
    - **Applied on:** R1’s G0/1 interface, inbound.
- **Scenario 2:**
    - **Requirement:** Hosts in `192.168.2.0/24` cannot access `10.0.2.0/24`.
    - **Solution:**
        
        ```
        deny ip 192.168.2.0 0.0.0.255 10.0.2.0 0.0.0.255
        permit ip any any
        ```
        
    - **Applied on:** R1’s G0/2 interface, inbound.
- **Scenario 3:**
    - **Requirement:** Prevent pings from `192.168.1.0/24` and `192.168.2.0/24` to `10.0.1.0/24` or `10.0.2.0/24`.
    - **Solution:**
        
        ```
        deny icmp 192.168.1.0 0.0.0.255 10.0.1.0 0.0.0.255
        deny icmp 192.168.1.0 0.0.0.255 10.0.2.0 0.0.0.255
        deny icmp 192.168.2.0 0.0.0.255 10.0.1.0 0.0.0.255
        permit ip any any
        ```
        
    - **Applied on:** R1’s G0/0 interface, outbound.

### **7. Verification and Resequencing:**

- **Verifying ACLs:**
    - Use `show ip interface` to check ACL application on interfaces.
- **Resequencing:**
    - Adjust sequence numbers for better management.