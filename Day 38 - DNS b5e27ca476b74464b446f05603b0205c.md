# Day 38 - DNS

Reviewed: No

### **1. Purpose of DNS**

- **DNS (Domain Name System):** Translates human-readable domain names (e.g., `youtube.com`) into IP addresses that devices use to communicate over networks.
- **DNS Resolution:** Allows us to use names instead of remembering IP addresses, which are harder to remember.
- **Client-Server Interaction:**
    - Client sends a **DNS query** to a **DNS server**.
    - DNS server responds with the **IP address** associated with the requested domain name.

### **2. DNS Functions**

- **DNS Query:** The client asks the DNS server for the IP address corresponding to a domain name (e.g., `youtube.com`).
- **DNS Cache:** Devices store DNS server responses locally so they don’t have to query the DNS server every time.
- **Hosts File:** A simple local file that can store IP addresses and domain names, used before DNS was developed.

### **3. How DNS Works**

- **PC1 Example:**
    - **NSLOOKUP Command:** Used to query the DNS server for the IP address of a domain (e.g., `youtube.com`).
    - **Ping Command:** Allows PC1 to send data to the resolved IP address of the domain.
- **DNS Query Steps:**
    - PC1 sends a DNS query to **Google’s DNS server** (`8.8.8.8`).
    - The DNS server responds with **youtube.com’s IP address**.
    - PC1 can now communicate with `youtube.com` using its IP address.

### **4. DNS Record Types**

- **A Record:** Maps a domain name to an **IPv4 address**.
- **AAAA Record (Quadruple A):** Maps a domain name to an **IPv6 address**.
- **CNAME Record (Canonical Name):** Maps a domain name to another domain name.

### **5. DNS Protocols**

- **UDP and TCP Ports:**
    - **DNS queries and responses:** Use **UDP port 53** (usually for messages < 512 bytes).
    - **TCP port 53**: Used for DNS messages **greater than 512 bytes**.

### **6. Viewing DNS Cache (Windows Commands)**

- **IPCONFIG /DISPLAYDNS:** Shows the local DNS cache of a Windows PC.
- **IPCONFIG /FLUSHDNS:** Clears the DNS cache.

### **7. Cisco IOS DNS Configuration**

- **Router as a DNS Server:**
    - **IP DNS SERVER:** Configures the router as a DNS server.
    - **IP HOST <hostname> <IP address>:** Configures static host-to-IP mappings in the router’s host table.
    - **IP NAME-SERVER <DNS server IP>:** Specifies an external DNS server (e.g., Google’s `8.8.8.8`) that the router will use to resolve DNS queries.
    - **IP DOMAIN LOOKUP:** Enables the router to perform DNS lookups (enabled by default).
- **Router as a DNS Client:**
    - **IP NAME-SERVER <DNS server IP>:** Configures the router to use an external DNS server to resolve names.
    - **IP DOMAIN NAME <domain name>:** Sets a default domain name for the router (e.g., `jeremysitlab.com`).

### **8. DNS Query Process Example**

- **PC1 pings `youtube.com`:**
    - PC1 queries its DNS server, **R1**.
    - **R1** doesn’t have the IP for `youtube.com`, so it queries Google’s DNS server (`8.8.8.8`).
    - Google’s DNS server responds with the IP address of `youtube.com`.
    - **R1** replies to PC1 with the IP address, and PC1 is now able to ping `youtube.com`.

### **9. Commands Overview**

- **Windows Commands:**
    - `IPCONFIG /ALL`: Shows detailed IP configuration, including DNS server.
    - `IPCONFIG /DISPLAYDNS`: Displays DNS cache.
    - `IPCONFIG /FLUSHDNS`: Clears DNS cache.
    - `NSLOOKUP <domain>`: Queries DNS server for the IP of a domain.
- **Cisco IOS Commands:**
    - `IP DNS SERVER`: Configures the router as a DNS server.
    - `IP HOST <hostname> <IP>`: Adds a host-to-IP mapping in the router’s host table.
    - `IP NAME-SERVER <DNS server IP>`: Configures an external DNS server for the router.
    - `IP DOMAIN LOOKUP`: Enables DNS lookups (default command).
    - `SHOW HOSTS`: Displays both static and learned DNS entries.