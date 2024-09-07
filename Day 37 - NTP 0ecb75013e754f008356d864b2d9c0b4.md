# Day 37 - NTP

Reviewed: No

### **1. Importance of Time Synchronization on Network Devices**

- **Accurate Time** is essential for:
    - **Accurate logs** for troubleshooting.
    - **Coordinating activities** like authentication and logging across multiple devices.
    - **Syslog:** Logging system events; helps correlate events in troubleshooting.
    - `show logging`: Displays the logs of the device
- **Device Internal Clock:**
    - Can drift over time, resulting in **inaccurate time**.
    - `show clock` command displays the time.
    - `show clock detail` shows the time source (internal hardware calendar by default).

### **2. Manual Time Configuration**

- **Set Time Manually:**
    - `clock set`: Manually set the software clock of the device (done in privileged exec mode, not global config mode).
- **Hardware Clock (Calendar) Configuration:**
    - `calender set`: Manually set the internal hardware clock (calendar).
    - `clock update-calender`: Sync hardware calendar to software clock.
    - `clock read-calender`: Sync software clock to hardware calendar.

### **3. Time Zone Configuration**

- `clock timezone`: Set the time zone (configured in global config mode and part of running configuration).
- **Daylight Saving Time (DST) Configuration**:
    - `clock summer-time`: Configure DST for automatic clock adjustment (e.g., forward in March, backward in November).

### **4. Introduction to NTP (Network Time Protocol)**

- **NTP Purpose:** Automatically synchronize the time between devices in a network.
- **Why NTP:** Manually setting time on multiple devices is inefficient and inaccurate due to clock drift.
- **How NTP Works:**
    - **NTP Servers:** Provide accurate time (devices sync their time with NTP servers).
    - **Stratum Levels:**
        - Stratum 0: Atomic or GPS clocks (reference clocks).
        - Stratum 1: NTP servers directly connected to stratum 0 clocks.
        - Stratum 2+: Sync from stratum 1 and above (closer to stratum 0 means higher accuracy).
    - **NTP Port:** UDP 123.

### **5. NTP Configuration**

- `ntp server <ip>` command: Configure NTP servers for the device to sync with (can specify multiple servers).
- `show ntp associations`: Displays the NTP servers configured and their status.
    - **Asterisk (*)**: Indicates the server the device is syncing to (sys.peer).
    - **Plus sign (+)**: Indicates a candidate server.
- `show ntp status`: Displays the status of NTP synchronization, including stratum level and reference clock.
- **Loopback Interface as NTP Source:**
    - Useful for redundancy and reliability in case a physical interface fails.
    - **`ntp source <loopback>`**: Specify the loopback interface for NTP messages.

### **6. NTP Server Modes**

- **Server Mode:** Device acts as an NTP server for other clients.
- **Client Mode:** Device synchronizes time from NTP servers.
- **Symmetric Active Mode (NTP Peering):** Devices at the same stratum level sync with each other and act as backups.

### **7. NTP Master Mode**

- **`ntp master <stratum level>`**: Makes a device act as an NTP master server, even if it’s not synced to another NTP server.
    - Default stratum is 8 (can be specified with the command).
    - **127.127.1.1**: Loopback address used for the NTP master server.

### **8. NTP Authentication**

- **Purpose:** Ensures NTP clients only sync with authenticated NTP servers.
- `ntp authenticate`: Enable NTP authentication.
- **`ntp authentication-key <key-number> md5 <password>`**: Create an authentication key (MD5 hash).
- **`ntp trusted-key <key-number>`**: Mark a key as trusted.
- **`ntp server <ip> key <key-number>`**: Use authentication when syncing with an NTP server.

### **9. NTP Key Concepts**

- **NTP SERVER:** Configures the device as an NTP client to sync with an NTP server.
- **NTP PEER:** Configures symmetric active mode (NTP peering).
- **NTP MASTER:** Configures the device to operate as an NTP server, even if it’s not syncing to an external server.
- **NTP AUTHENTICATE:** Enables NTP authentication for secure synchronization.

---

### **Key NTP Commands:**

1. **Manually Configure Time:**
    - `clock set HH:MM:SS MONTH DAY YEAR`
    - `calendar set HH:MM:SS MONTH DAY YEAR`
    - `clock update-calendar` or `clock read-calendar`
    - **`clock summer-time <***name>* **recurring <***start> <end>* [*offset*]`
2. **NTP Configuration:**
    - `ntp server <ip>` (to sync with an NTP server)
    - `show ntp associations`
    - `show ntp status`
    - `ntp master [stratum level]` (to set the device as an NTP master)
    - `ntp peer <ip>` (to enable symmetric active mode)
3. **NTP Authentication:**
    - `ntp authenticate`
    - `ntp authentication-key <key-number> md5 <password>`
    - `ntp trusted-key <key-number>`
    - `ntp server <ip> key <key-number>`