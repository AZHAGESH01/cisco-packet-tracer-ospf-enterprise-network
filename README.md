# Enterprise Multi-Branch OSPF Network with Automatic Failover

## 📘 Overview

This project demonstrates the implementation of an Enterprise Multi-Branch Network using Cisco Packet Tracer and OSPF (Open Shortest Path First).

The network consists of a Chennai Head Office connected to Coimbatore, Salem, and Madurai Branch Offices. OSPF dynamic routing provides automatic route learning, shortest-path selection, and failover capabilities when network links become unavailable.

---

## 🏢 1. Network Topology

### Head Office

* Chennai HQ

### Branch Offices

* Coimbatore Branch
* Salem Branch
* Madurai Branch

### LAN Networks

| Location   | Network        |
| ---------- | -------------- |
| Chennai HQ | 192.168.1.0/24 |
| Coimbatore | 192.168.2.0/24 |
| Salem      | 192.168.3.0/24 |
| Madurai    | 192.168.4.0/24 |

---

## 🌐 2. WAN Link Configuration

### Chennai ↔ Coimbatore

```bash
10.0.1.0/24
```

### Coimbatore ↔ Salem

```bash
10.0.2.0/24
```

### Salem ↔ Madurai

```bash
10.0.3.0/24
```

### Chennai ↔ Madurai

```bash
10.0.4.0/24
```

### Chennai ↔ Salem

```bash
10.0.5.0/24
```

### Coimbatore ↔ Madurai

```bash
10.0.6.0/24
```

---

## ⚙️ 3. OSPF Configuration

### Chennai Head Office Router

```bash
router ospf 1
 network 10.0.1.0 0.0.0.255 area 0
 network 10.0.4.0 0.0.0.255 area 0
 network 10.0.5.0 0.0.0.255 area 0
 network 192.168.1.0 0.0.0.255 area 0
```

### Coimbatore Branch Router

```bash
router ospf 1
 network 10.0.1.0 0.0.0.255 area 0
 network 10.0.2.0 0.0.0.255 area 0
 network 10.0.6.0 0.0.0.255 area 0
 network 192.168.2.0 0.0.0.255 area 0
```

### Salem Branch Router

```bash
router ospf 1
 network 10.0.2.0 0.0.0.255 area 0
 network 10.0.3.0 0.0.0.255 area 0
 network 10.0.5.0 0.0.0.255 area 0
 network 192.168.3.0 0.0.0.255 area 0
```

### Madurai Branch Router

```bash
router ospf 1
 network 10.0.3.0 0.0.0.255 area 0
 network 10.0.4.0 0.0.0.255 area 0
 network 10.0.6.0 0.0.0.255 area 0
 network 192.168.4.0 0.0.0.255 area 0
```

---

## 🖥️ 4. FTP Server Configuration

FTP Server Location:

```text
Chennai Head Office
IP Address: 192.168.1.3
```

Services Enabled:

```text
FTP
ICMP Reachability
```

All branch offices can access the FTP Server through OSPF routing.

---

## 🧪 5. Connectivity Testing

### Ping Test

From Coimbatore PC

```cmd
ping 192.168.1.3
```

From Salem PC

```cmd
ping 192.168.1.3
```

From Madurai PC

```cmd
ping 192.168.1.3
```

Expected Result:

```text
Reply from 192.168.1.3
Packets: Sent = 4, Received = 4, Lost = 0
```

---

## 🔄 6. OSPF Failover Testing

The network was tested by disconnecting various WAN links.

### Test Scenarios

```text
Chennai ↔ Coimbatore Link Failure
Chennai ↔ Salem Link Failure
Chennai ↔ Madurai Link Failure
Coimbatore ↔ Salem Link Failure
Coimbatore ↔ Madurai Link Failure
Salem ↔ Madurai Link Failure
```

### Expected OSPF Behavior

```text
1. Detect Link Failure
2. Recalculate Routing Table
3. Select Alternate Shortest Path
4. Restore Connectivity Automatically
```

---

## 🧰 7. Verification Commands

### Verify OSPF Neighbors

```bash
show ip ospf neighbor
```

### Verify OSPF Routes

```bash
show ip route ospf
```

### Verify Routing Table

```bash
show ip route
```

### Verify Interfaces

```bash
show ip interface brief
```

---

## 📸 8. Screenshots

### Network Topology

```text
Add Screenshot: topology.png
```

### OSPF Failover Test

```text
Add Screenshot: failover-test.png
```

### Successful Ping Verification

```text
Add Screenshot: ping-test.png
```

### FTP Connectivity Verification

```text
Add Screenshot: ftp-connectivity.png
```

---

## 📜 Notes

* OSPF Area 0 used throughout the network.
* Full mesh WAN connectivity implemented.
* Automatic failover tested successfully.
* FTP Server reachable from all branch offices.
* Designed to simulate a real enterprise WAN environment.

---

## ✅ Expected Result

| Feature                 | Status     |
| ----------------------- | ---------- |
| OSPF Neighbor Formation | Successful |
| Route Advertisement     | Successful |
| Ping Connectivity       | Successful |
| FTP Connectivity        | Successful |
| Automatic Failover      | Successful |
| Route Convergence       | Successful |
| High Availability       | Successful |

All branch offices maintain connectivity even when individual WAN links fail through OSPF automatic route recalculation.
