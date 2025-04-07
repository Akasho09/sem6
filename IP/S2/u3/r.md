# Routing Information Protocol (RIP)

## 🧠 Overview

**Routing Information Protocol (RIP)** is one of the oldest **distance-vector** routing protocols, used in both LANs and WANs. It helps routers dynamically exchange routing information and determine the best path to reach a destination based on **hop count**.

---

## 📌 Key Characteristics

- **Type**: Distance Vector
- **Metric**: Hop count
- **Maximum Hop Count**: 15 (16 = unreachable)
- **Update Frequency**: Every 30 seconds
- **Transport Protocol**: UDP (Port 520)

---

## 🧰 How RIP Works

1. Each router maintains a **routing table**.
2. Routers periodically **broadcast** their routing tables to neighboring routers.
3. Routers update their own tables based on neighbors’ info using **Bellman-Ford algorithm**.
4. Routes with fewer hops are preferred.
5. If no update is received for 180 seconds, the route is considered **invalid**.

---

## 📦 Types of RIP

| Version | Description                          |
|---------|--------------------------------------|
| RIP v1  | Classful, no subnet info, no authentication |
| RIP v2  | Classless (supports CIDR), supports authentication |
| RIPng   | RIP for IPv6 networks                |

---

## 🔐 Loop Prevention Techniques

| Technique         | Description                                       |
|------------------|---------------------------------------------------|
| Split Horizon     | Prevents route info from being sent back the way it came |
| Route Poisoning   | Marks failed route with a hop count of 16 (infinite) |
| Hold-down Timer   | Prevents immediate updates to avoid flapping     |
| Triggered Updates | Sends updates immediately when a route changes   |

---

## ⚠️ Limitations of RIP

- **Scalability Issues**: Not suitable for large networks (due to 15-hop limit)
- **Slow Convergence**: Takes time to detect failures and update routes
- **No QoS Support**: Can't differentiate traffic based on priority
- **Only One Metric**: Considers only hop count, not bandwidth or delay

---

## ✅ Use Cases

- Small to medium-sized networks
- Educational environments
- Legacy systems

---

## 📖 Conclusion

RIP is a simple and easy-to-configure routing protocol but is largely outdated for modern, large-scale networks. It's primarily used today for **teaching**, **labs**, or **legacy systems**, with more advanced protocols like **OSPF**, **EIGRP**, and **BGP** preferred for production use.



### 📄 RIP Packet Format (20 bytes header + routing entries):
RIP is one of the oldest distance-vector routing protocols used to help routers exchange information about network paths.

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