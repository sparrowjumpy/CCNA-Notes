# Day 30 - TCP & UDP

Reviewed: No

### **1. Introduction to TCP & UDP:**

- **Layer 4 Protocols:** TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are both Layer 4 protocols in the OSI model, responsible for the transport of data between devices on a network.
- **Exam Focus:** The CCNA exam expects you to compare TCP and UDP, understanding their differences and the services they provide to applications.

### **2. Basics of Layer 4:**

- **Transparent Data Transfer:** Layer 4 protocols provide transparent data transfer between end hosts, meaning the transfer of data is seamless and hidden from the end users.
- **Services Provided by TCP (Not by UDP):**
    - **Reliable Data Transfer:** Ensures all data is delivered correctly to the destination.
    - **Error Recovery:** Resends data if errors are detected during transmission.
    - **Data Sequencing:** Ensures that data arrives in the correct order.
    - **Flow Control:** Manages the pace of data transmission to prevent overwhelming the destination host.

### **3. Layer 4 Addressing - Port Numbers:**

- **Port Numbers:** Layer 4 protocols use port numbers for addressing, which help identify the application layer protocol and manage multiple communication sessions.
    - **Session Multiplexing:** Allows a single device to handle multiple communication sessions simultaneously.
- **IANA Port Ranges:**
    - **Well-known Ports:** 0 - 1023 (e.g., HTTP, FTP).
    - **Registered Ports:** 1024 - 49151 (require registration).
    - **Ephemeral Ports:** 49152 - 65535 (used for dynamic port assignments).

### **4. Transmission Control Protocol (TCP):**

- **Connection-Oriented:** TCP establishes a connection before data is transmitted, ensuring that both the sender and receiver are ready for communication.
- **Reliable Communication:** TCP guarantees that data is delivered without errors and in the correct sequence.
- **Flow Control:** Uses a sliding window mechanism to control the flow of data and prevent overwhelming the destination.
- **TCP Header Fields:**
    - **Source & Destination Ports:** Identify the sending and receiving applications.
    - **Sequence Number & Acknowledgment Number:** Used for sequencing and ensuring reliable communication.
    - **Flags (e.g., SYN, ACK, FIN):** Control the establishment, maintenance, and termination of connections.
    - **Window Size:** Manages the flow of data.
- **TCP Three-Way Handshake:** Establishes a connection using SYN, SYN-ACK, and ACK messages.
- **TCP Four-Way Handshake:** Terminates a connection using FIN and ACK messages.
- **Sequencing & Acknowledgment:** Ensures data is delivered in the correct order and retransmits if segments are lost.

### **5. User Datagram Protocol (UDP):**

- **Connectionless:** UDP does not establish a connection before sending data. Data is simply sent without any handshake process.
- **Best-Effort Delivery:** UDP provides no guarantee of data delivery, order, or error recovery.
- **UDP Header Fields:**
    - **Source & Destination Ports:** Identify the sending and receiving applications.
    - **Length & Checksum:** Simple fields indicating segment length and basic error checking.

### **6. Comparing TCP and UDP:**

- **Header Size:**
    - **TCP:** Larger header with more fields for advanced services.
    - **UDP:** Smaller header with minimal fields, resulting in lower overhead.
- **Use Cases:**
    - **TCP:** Used for applications where reliable communication is essential (e.g., file transfers, web browsing).
    - **UDP:** Preferred for real-time applications where speed is more critical than reliability (e.g., video streaming, VoIP).
- **Examples:**
    - **TCP:** HTTP (Port 80), HTTPS (Port 443), FTP (Ports 20, 21).
    - **UDP:** DNS (Port 53), DHCP (Ports 67, 68), TFTP (Port 69).

### **7. Important Well-Known Port Numbers:**

**TCP:**

- FTP (Data): 20
- FTP (Control): 21
- SSH: 22
- Telnet: 23
- SMTP: 25
- HTTP: 80
- POP3: 110
- HTTPS: 443

**UDP:**

- DHCP (server): 67
- DHCP (client): 68
- TFTP (Trivial FTP): 69
- SNMP (agent): 161
- SNMP (manager): 162
- Syslog: 514
- NTP: 123
- RADIUS: 1812, 1813

**Both TCP and UDP:**

- DNS: 53