# ## Important Commands ##

Reviewed: No

### Basic Configuration Commands

1. **Entering Global Configuration Mode:**
    
    ```
    configure terminal
    
    ```
    
2. **Setting the Router Hostname:**
    
    ```
    hostname [name]
    
    ```
    
3. **Setting Up a Password for Privileged EXEC Mode:**
    
    ```
    enable secret [password]
    
    ```
    
4. **Setting a Console Password:**
    
    ```
    line console 0
    password [password]
    login
    
    ```
    
5. **Setting a Password for VTY Lines:**
    
    ```
    line vty 0 4
    password [password]
    login
    
    ```
    
6. **Setting a Banner Message:**
    
    ```
    banner motd #[Your Message]#
    
    ```
    

### Interface Configuration

1. **Configuring an Interface:**
    
    ```
    interface [type] [number]
    ip address [ip-address] [subnet-mask]
    no shutdown
    
    ```
    
2. **Setting a Description for an Interface:**
    
    ```
    description [description]
    
    ```
    
3. **Configuring a Switch Port for Access Mode:**
    
    ```
    interface [type] [number]
    switchport mode access
    switchport access vlan [vlan-id]
    
    ```
    
4. **Configuring a Switch Port for Trunk Mode:**
    
    ```
    interface [type] [number]
    switchport mode trunk
    switchport trunk allowed vlan [add | all | except | none | remove] [vlan-list]
    
    ```
    

### VLAN Configuration

1. **Creating a VLAN:**
    
    ```
    vlan [vlan-id]
    name [vlan-name]
    
    ```
    
2. **Assigning a VLAN to a Port:**
    
    ```
    interface [type] [number]
    switchport access vlan [vlan-id]
    
    ```
    

### Routing Configuration

1. **Configuring Static Routing:**
    
    ```
    ip route [destination-network] [mask] [next-hop-address | exit-interface]
    
    ```
    
2. **Configuring RIP:**
    
    ```
    router rip
    version [1 | 2]
    network [network-address]
    
    ```
    
3. **Configuring OSPF:**
    
    ```
    router ospf [process-id]
    network [network-address] [wildcard-mask] area [area-id]
    
    ```
    
4. **Configuring EIGRP:**
    
    ```
    router eigrp [autonomous-system]
    network [network-address] [wildcard-mask]
    
    ```
    

### Security Configuration

1. **Configuring Standard ACL:**
    
    ```
    access-list [access-list-number] permit|deny [source] [wildcard-mask]
    
    ```
    
2. **Applying ACL to an Interface:**
    
    ```
    interface [type] [number]
    ip access-group [access-list-number] in|out
    
    ```
    

### Troubleshooting Commands

1. **Ping:**
    
    ```
    ping [ip-address]
    
    ```
    
2. **Traceroute:**
    
    ```
    traceroute [ip-address]
    
    ```
    
3. **Show IP Interface Brief:**
    
    ```
    show ip interface brief
    
    ```
    
4. **Show Running Configuration:**
    
    ```
    show running-config
    
    ```
    
5. **Show IP Route:**
    
    ```
    show ip route
    
    ```
    
6. **Show VLANs:**
    
    ```
    show vlan brief
    
    ```
    
7. **Show Interfaces:**
    
    ```
    show interfaces
    
    ```
    
8. **Show Version:**
    
    ```
    show version
    
    ```
    

### NAT Configuration

1. **Configuring Static NAT:**
    
    ```
    ip nat inside source static [inside-local] [inside-global]
    
    ```
    
2. **Configuring Dynamic NAT:**
    
    ```
    ip nat pool [name] [start-ip] [end-ip] netmask [netmask]
    access-list [access-list-number] permit [source] [wildcard-mask]
    ip nat inside source list [access-list-number] pool [name]
    
    ```
    
3. **Configuring PAT (NAT Overload):**
    
    ```
    access-list [access-list-number] permit [source] [wildcard-mask]
    ip nat inside source list [access-list-number] interface [type] [number] overload
    
    ```
    

### DHCP Configuration

1. **Configuring a DHCP Server:**
    
    ```
    ip dhcp pool [pool-name]
    network [network] [mask]
    default-router [default-router]
    dns-server [dns-server]
    
    ```
    
2. **Excluding IP Addresses from DHCP Pool:**
    
    ```
    ip dhcp excluded-address [start-ip] [end-ip]
    
    ```
    

### Spanning Tree Protocol (STP)

1. **Enabling STP:**
    
    ```
    spanning-tree mode [pvst | rapid-pvst]
    
    ```
    
2. **Setting the Root Bridge:**
    
    ```
    spanning-tree vlan [vlan-id] root primary|secondary
    
    ```
    
3. **Configuring PortFast:**
    
    ```
    interface [type] [number]
    spanning-tree portfast
    
    ```
    

### Miscellaneous Commands

1. **Saving the Configuration:**
    
    ```
    copy running-config startup-config
    
    or
    
    write
    ```
    
2. **Erasing the Configuration:**
    
    ```
    erase startup-config
    
    ```
    
3. **Reloading the Device:**
    
    ```
    reload
    
    ```