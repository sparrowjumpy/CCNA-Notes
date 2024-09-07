# Day 34 - Standard ACLs

Reviewed: No

### **1. Introduction to Access Control Lists (ACLs):**

- **Purpose of ACLs:**
    - ACLs control access to the network by filtering traffic based on specific criteria.
    - They function as packet filters, deciding whether to permit or deny traffic.
- **Main Uses of ACLs:**
    - **Security:** Controlling access between devices on a network.
    - **Traffic Filtering:** Based on IP addresses and Layer 4 port numbers.

### **2. ACL Basics:**

- **ACL Configuration:**
    - Configured globally on the router in global config mode.
    - Made up of an ordered sequence of Access Control Entries (ACEs).
- **Types of ACLs:**
    - **Standard ACLs:** Filter traffic based on the source IP address only.
    - **Extended ACLs:** Filter traffic based on source/destination IP addresses, port numbers, and more (covered in Day 35).
- **ACL Application:**
    - After configuration, ACLs must be applied to an interface in either the **inbound** or **outbound** direction.

### **3. ACL Logic and Processing:**

- **Processing Order:**
    - Entries in an ACL are processed sequentially, from top to bottom.
    - Once a match is found, the specified action (permit or deny) is taken, and no further entries are processed.
- **Importance of Entry Order:**
    - The order of ACEs is critical. Misordering can lead to unintended results.
- **Implicit Deny:**
    - There is an `implicit "deny all"`  at the end of every ACL, meaning any traffic that doesn't match any ACE will be denied.

### **4. Standard ACLs:**

- **Standard Numbered ACLs:**
    - Match traffic based only on the **source IP address**.
    - Identified by a number in the range of **1-99** or **1300-1999**.
    - Use **wildcard masks** to specify address ranges (not subnet masks).
- **Standard Named ACLs:**
    - Similar to numbered ACLs but identified by a **name** instead of a number.
    - Configured in **standard named ACL config mode**.

### **5. Configuring Standard Numbered ACLs:**

- **Command Syntax:**
    
    `access-list <number> {deny | permit} <source IP> <wildcard mask>`
    
    - Examples:
        - `access-list 1 deny 1.1.1.1 0.0.0.0`
        - `access-list 1 permit any`
- **Wildcard Mask:**
    - Used to specify which bits of the IP address should be matched.
- **Applying ACLs to Interfaces:**
    - Use the command:
        
        `ip access-group <number> {in | out}`
        
    - Example:
        
        `ip access-group 1 out`
        

### **6. Configuring Standard Named ACLs:**

- **Entering Named ACL Config Mode:**
    
    `ip access-list standard <name>`
    
    - Configure ACEs within this mode.
- **Example Configuration:**
    
    ```
    ip access-list standard BLOCK_BOB
    deny 1.1.1.1
    permit any
    ```
    
- **Entry Numbers:**
    - You can specify entry numbers manually to control the order.

### **7. ACL Best Practices:**

- **Placement of Standard ACLs:**
    - Apply standard ACLs **as close to the destination as possible** to avoid unintended traffic filtering. **(*RULE OF THUMB*)**

### **8. Quiz Review:**

- **Key Points:**
    - ACLs are processed from top to bottom.
    - An implicit deny at the end of the ACL blocks unmatched traffic.
    - Only one ACL can be applied in each direction (inbound or outbound) on an interface.