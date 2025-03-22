# BGP and NAT Lab – Bits of Progress

This lab demonstrates how to configure BGP peering between multiple Autonomous Systems and perform both Static and Dynamic NAT using Cisco IOS routers. The lab includes multi-AS BGP configuration, IP reachability verification, and NAT configuration at the network edge.

---

## 🧠 Objective
- Establish BGP peerings using Loopback interfaces across 3 ASes (65005, 65010, 65015).
- Configure Static and PAT (Port Address Translation) NAT on the edge routers.
- Validate external reachability using VPCs and packet inspection via Wireshark.

---

## 🛠️ Tools Used
- Cisco IOSv Routers in GNS3
- VPCS Hosts
- Wireshark for packet analysis

---

## 🖧 Topology Overview

- **EdgeRouter1 (AS 65005)** ↔ **ISPRouter2** ↔ **EdgeRouter2 (AS 65010)**
- **ISPRouter2** ↔ **ISPRouter1 (AS 65015)** → NAT Cloud (Internet simulation)
- Two internal LANs:
  - 172.16.10.0/24 behind EdgeRouter1
  - 172.16.20.0/24 behind EdgeRouter2

---

## 🔧 Configuration Steps

1. Configured Loopback interfaces for BGP peering.
2. Static routes to reach peer Loopbacks.
3. BGP configured with `ebgp-multihop` for Loopback-based peering.
4. Static NAT configured on EdgeRouter1 for VPC6 (ping to 8.8.8.8).
5. PAT configured on both EdgeRouters to enable outbound traffic from internal networks.
6. Wireshark capture on ISPRouter1 G0/0 verified IP translation before and after NAT.

---

## 🧪 Testing & Troubleshooting

- VPC6 (172.16.10.2) successfully pinged 8.8.8.8 after Static NAT config.
- Verified NAT translations with `show ip nat translations`.
- Used Wireshark to inspect real-time source/destination IP changes.
- Included troubleshooting during misconfigurations for a realistic demonstration.

---

## 📁 Files

- `EdgeRouter1.txt`  
- `EdgeRouter2.txt`  
- `ISPRouter1.txt`  
- `ISPRouter2.txt`  
- Topology screenshot

---

## 📺 YouTube Video

Watch the full walkthrough including config, NAT demo, packet capture, and real-world troubleshooting:
**[YouTube Video Link Placeholder]**

---

## 🧠 Lessons Learned

- Always verify routes to BGP Loopbacks before forming peerings.
- NAT translations don’t occur without valid `ip nat inside`/`outside` interface pairing.
- Wireshark is a powerful tool to visually confirm NAT behavior.
- Mistakes are part of the learning process—laugh them off and keep moving forward.

---

Stay gritty. Stay consistent. Keep building.  
— **Bits of Progress**
