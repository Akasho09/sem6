
## 1. 🧭 ARP (Address Resolution Protocol)

**Used to resolve IP address to MAC address.**

Address Resolution Protocol (ARP) is a protocol or procedure that connects an ever-changing Internet Protocol (IP) address to a fixed physical machine address, also known as a media access control (MAC) address, in a local-area network (LAN).
 - This mapping procedure is important because the lengths of the IP and MAC addresses differ, and a translation is needed so that the systems can recognize one another. The most used IP today is IP version 4 (IPv4). An IP address is 32 bits long. However, MAC addresses are 48 bits long. ARP translates the 32-bit address to 48 and vice versa.
![alt text](image.png)
- An ARP request is broadcast;   an ARP reply is unicast. (rarp as well)
- The RARP request packets are  broadcast;  the RARP reply packets are  unicast.

# 📦 Packet Formats for ARP, DHCP, and RIP

---

### 📄 ARP Packet Format (28 bytes):

| Field Name              | Size (bytes) | Description                              |
|-------------------------|--------------|------------------------------------------|
| Hardware Type           | 2            | Type of hardware (Ethernet = 1)          |
| Protocol Type           | 2            | Type of protocol (IP = 0x0800)           |
| Hardware Address Length | 1            | Length of MAC address (usually 6)        |
| Protocol Address Length | 1            | Length of IP address (usually 4)         |
| Operation               | 2            | Request (1) or Reply (2)                 |
| Sender Hardware Address | 6            | MAC address of sender                    |
| Sender Protocol Address | 4            | IP address of sender                     |
| Target Hardware Address | 6            | MAC address of target (0 for request)    |
| Target Protocol Address | 4            | IP address of target                     |

---

- RARP same packet format and encapsulartion.



### 🔹 Ethernet Frame Format Carrying ARP:

| Ethernet Frame Field | Size (bytes) | Description                                  |
|----------------------|--------------|----------------------------------------------|
| Destination MAC      | 6            | Broadcast (`FF:FF:FF:FF:FF:FF`) for request   |
| Source MAC           | 6            | MAC of the sender                            |
| EtherType            | 2            | `0x0806` → Indicates ARP                     |
| ARP Payload          | 28           | The ARP message itself (request or reply)    |
| FCS (CRC)            | 4            | Frame Check Sequence for error checking      |

---


## 2. 📡 DHCP (Dynamic Host Configuration Protocol)

**Used to dynamically assign IP addresses to devices.**

### 📄 DHCP Packet Format (Based on BOOTP, 236+ bytes):

| Field Name            | Size (bytes) | Description                              |
|-----------------------|--------------|------------------------------------------|
| op                    | 1            | Message type: 1 = request, 2 = reply     |
| htype                 | 1            | Hardware type (Ethernet = 1)             |
| hlen                  | 1            | Hardware address length (Ethernet = 6)   |
| hops                  | 1            | Relay agent hops                         |
| xid                   | 4            | Transaction ID                           |
| secs                  | 2            | Seconds since client started trying      |
| flags                 | 2            | Flags                                    |
| ciaddr                | 4            | Client IP address (if already assigned)  |
| yiaddr                | 4            | 'Your' (client) IP address               |
| siaddr                | 4            | Server IP address                        |
| giaddr                | 4            | Gateway IP address                       |
| chaddr                | 16           | Client hardware address                  |
| sname                 | 64           | Optional server host name                |
| file                  | 128          | Boot file name                           |
| options               | variable     | DHCP options (e.g., lease time, router)  |

---


### 📄 RIP Packet Format (20 bytes header + routing entries):

| Field Name     | Size (bytes) | Description                            |
|----------------|--------------|----------------------------------------|
| Command        | 1            | Request (1) or Response (2)            |
| Version        | 1            | RIP version (1 or 2)                   |
| Unused         | 2            | Must be zero                           |
| Route Entries  | 20 * N       | One or more route entries              |

### 📄 Route Entry Format (Each entry: 20 bytes):

| Field Name     | Size (bytes) | Description                            |
|----------------|--------------|----------------------------------------|
| Address Family | 2            | AFI (e.g., 2 for IP)                   |
| Route Tag      | 2            | For inter-domain routing               |
| IP Address     | 4            | Destination IP address                 |
| Subnet Mask    | 4            | Subnet mask                           |
| Next Hop       | 4            | IP address of next hop router         |
| Metric         | 4            | Hop count (1 to 16, where 16 = infinity)|

---