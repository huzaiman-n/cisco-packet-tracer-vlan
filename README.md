# 🏆 Multi-Switch VLAN Segmentation & VTP Configuration
### Diploma Networking Practical Examination (Amali) — 100% Perfect Score (66/66)

---

## 📊 1. Network Topology Diagram
Below is the verified network architecture designed in Cisco Packet Tracer.

![Network Topology Diagram](topology.png)

---

## 📝 2. System Documentation & Design Specifications

This network uses a hierarchical design across three main switch blocks to isolate traffic broadcast domains and manage subnets efficiently.

### 🏢 VLAN Mapping & Host Allocation

| Block Location | Switch Name | Assigned VLAN | Department Name | Target Hosts | Connected Ports |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Pejabat Pentadbir** | `SW-PEJABAT` | VLAN 11 <br> VLAN 22 <br> VLAN 33 | Admin 11 <br> Admin 22 <br> Admin 33 | Management | `Fa0/6` <br> `Fa0/11` <br> `Fa0/1` |
| **Blok 1** | `SW-BLOK1` | VLAN 11 | JTM (Teknologi Maklumat) | 100 Hosts | `Fa0/1`, `Fa0/5` |
| **Blok 2** | `SW-BLOK2` | VLAN 22 <br> VLAN 33 | JU (Usahawan) <br> JP (Perniagaan) | 50 Hosts <br> 25 Hosts | `Fa0/4`, `Fa0/6` <br> `Fa0/15`, `Fa0/11` |

### 🔗 Backbone Trunk Links
To allow traffic from all VLANs to travel between the switches, high-speed **802.1Q Trunk Links** were configured on the following interconnection ports:
* **`SW-PEJABAT`** ➔ Connects to downstream switches via trunk ports **`Fa0/23`** and **`Fa0/24`**.
* **`SW-BLOK1`** ➔ Uplinks to core via trunk port **`Fa0/23`**.
* **`SW-BLOK2`** ➔ Uplinks to core via trunk port **`Fa0/24`**.

---

## 🧪 3. Connectivity Verification (Ping Tests)

End-to-end communication was successfully verified using internet control message protocol (ICMP) echo requests between the administrative core and host nodes:

| Source Node | Destination Node | Target IP Address | Test Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **ADMIN 11** | PC 11 A | `192.168.0.5` | 4 Packets Sent, 4 Received (0% Loss) | ✅ SUCCESS |
| **ADMIN 22** | PC 22 A | `192.168.0.133` | 4 Packets Sent, 4 Received (0% Loss) | ✅ SUCCESS |
| **ADMIN 33** | PC 33 A | `192.168.0.197` | 4 Packets Sent, 4 Received (0% Loss) | ✅ SUCCESS |

---

## 🔒 4. Applied Switch Security Protocols
To match enterprise compliance requirements, the following security baseline parameters were applied directly via the Cisco IOS CLI:
1. **Console Line Protection:** Secured with local authentication passwords.
2. **Privileged Mode Security:** Configured `Enable Secret` hashing to protect configuration access.
3. **Password Encryption:** Activated `service password-encryption` globally to prevent plain-text viewing within configuration files (`show run`).
4. **VLAN Automation:** Configured **VTP (VLAN Trunking Protocol)** Domain Name, Modes, and Passwords to automatically update database files securely across the architecture.
