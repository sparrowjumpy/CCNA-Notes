# Day 9 - Switch Interfaces

Reviewed: No

## Key Concepts

### Interface Speed and Duplex

- **Speed:** Data rate in bits per second (e.g., 10, 100, 1000 Mbps).
- **Duplex:** Whether a device can send and receive data simultaneously.
    - **Full Duplex:** Send and receive at the same time.
    - **Half Duplex:** Cannot send and receive at the same time.

### Speed and Duplex Autonegotiation

- Devices negotiate speed and duplex settings automatically.
- **Interface Status:** Using `show ip interface brief` to check Layer 1 and 2 status.

### Interface Counters and Errors

- Cisco devices keep counters for traffic and errors.
- `show interfaces` command provides detailed statistics.

## Network Topology

- Single LAN: 192.168.1.0/24 with 1 router (R1), 2 switches (SW1, SW2), and 4 PCs.
- Focus on SW1 and its interfaces (F0/1 to F0/4).

## CLI Commands

### Initial Configuration

1. Enter privileged exec mode: `enable`
2. Check interface status: `show ip interface brief`
    - Connected interfaces: up/up
    - Unconnected interfaces: down/down
    - Router interfaces: administratively down by default
    - Switch interfaces: enabled by default

### Configuring Interfaces

- **Speed:** `speed {10 | 100 | auto}`
- **Duplex:** `duplex {auto | full | half}`
- **Description:** `description <text>`

### Example Configuration

- Configure interface F0/1:
    
    ```
    interface f0/1
    speed 100
    duplex full
    description ## Connected to R1 ##
    ```
    
- Check configuration: `show interfaces status`

### Handling Unused Interfaces

- Disable unused interfaces for security:
    
    ```
    interface range f0/5 - 12
    description ## Unused ## 
    shutdown
    ```
    

### Interface Errors

- **Common Error Counters:**
    - **Runts:** Frames smaller than 64 bytes.
    - **Giants:** Frames larger than 1518 bytes.
    - **CRC Errors:** Frames with cyclic redundancy check failures.
    - **Frame Errors:** Frames with incorrect format.

## Detailed Topics

### Half Duplex and Full Duplex

- **Half Duplex:** Cannot send and receive simultaneously.
    - Collision domains, handled by CSMA/CD (Carrier Sense Multiple Access with Collision Detection).
- **Full Duplex:** Can send and receive simultaneously.
    - Used in modern networks with switches, reducing collisions.

### Autonegotiation

- Interfaces negotiate best speed and duplex settings.
- If autonegotiation fails, switches default to the lowest speed and half duplex.

### Error Analysis

- Use `show interfaces` to view detailed error statistics.

## Quiz

1. **Question 1:** What results from a duplex mismatch between two interfaces?
    - Answer: B, collisions will occur.
2. **Question 2:** What is used on half-duplex interfaces to detect and avoid collisions?
    - Answer: A, CSMA/CD.
3. **Question 3:** Which command shows various counters of errors detected on an interface?
    - Answer: A, show interfaces.
4. **Question 4:** Which are examples of errors that might occur on a network interface?
    - Answer: D, runts, giants, CRC.
5. **Question 5:** What speed and duplex settings will SW1 use if SW2 has autonegotiation disabled and is set to 100 Mbps full duplex?
    - Answer: B, speed 100 Mbps, duplex half.