# BGP + NAT Lab – Real Configuration, Real Troubleshooting

This lab simulates a realistic edge network using Cisco routers inside EVE-NG. I configured BGP across multiple autonomous systems and used NAT (Static and PAT) on the edge routers to enable internet access for internal private IP subnets.

The lab includes a complete walkthrough of Static NAT and PAT with real packet inspection using Wireshark. I also included my troubleshooting process, mistakes, and how I fixed them—all part of building actual skill, not just typing commands.

---

## Lab Objectives

- Establish BGP peering across three autonomous systems (65005, 65010, 65015)
- Configure Static NAT on EdgeRouter1 for a single VPC host
- Configure PAT (overload) on both edge routers for dynamic NAT
- Use Wireshark to inspect NAT translations and ICMP traffic
- Verify that internal hosts cannot reach the internet without NAT
- Walk through and explain real mistakes and how they were resolved

---

## Environment

- Platform: EVE-NG
- Devices: Cisco IOSv routers, VPCS hosts
- Analysis Tool: Wireshark

---

## IP Scheme and Device Roles

- **EdgeRouter1**
  - Inside Interface: 172.16.10.0/24 (VPC6, VPC7)
  - Outside Interface: 10.0.5.2/30
  - Loopback: 10.0.5.20
- **EdgeRouter2**
  - Inside Interface: 172.16.20.0/24 (VPC8, VPC9)
  - Outside Interface: 10.0.10.2/30
  - Loopback: 10.0.10.20
- **ISPRouter2**
  - Core peering router between Edge routers and ISP
  - BGP AS 65005
- **ISPRouter1**
  - Simulates upstream ISP
  - External interface uses DHCP
  - BGP AS 65015
- **VPC6**: 172.16.10.2 (used for Static NAT testing)

---

## Key Configuration Features

- BGP peering established over Loopback interfaces using `ebgp-multihop` and `update-source`
- Static NAT configured for VPC6 to reach 8.8.8.8
- PAT configured for the rest of the subnet using access-lists and interface overload
- Wireshark capture taken from ISPRouter1's external interface to inspect packet translation

---

## Troubleshooting Moments

1. **Accidentally Advertised LANs into BGP**  
   I originally advertised the 172.16.x.x LANs into BGP, which caused return traffic to route correctly even without NAT. This led to pings working when they shouldn’t have. I removed the network advertisements, and NAT behavior was correctly observed afterward.

2. **Incorrect ACL Mask for NAT**  
   When configuring the PAT access-list, I mistakenly used a subnet mask (`255.255.255.0`) instead of a wildcard mask (`0.0.0.255`). This caused NAT to fail completely until corrected.

These mistakes are shown and explained in the video, along with how I identified and fixed them.

---

## Watch the Full Lab Video

This video is not a polished tutorial—it's a real session. I talk through my thinking, the configs, and the mistakes. You’ll see me troubleshoot in real time, not just paste pre-written commands.

Watch here:  
**[YouTube](https://www.youtube.com/watch?v=0aLSPyd1_pA)**

---

## Read the Full Blog Article

For a full write-up with additional context, configurations, and lessons learned:  
**[BitsofProgress.com](https://bitsofprogress.com/bgp-nat-lab-with-real-troubleshooting-static-nat-pat-and-packet-capture)**

---

## Included Files

- EdgeRouter1.txt  
- EdgeRouter2.txt  
- ISPRouter1.txt  
- ISPRouter2.txt  
- Topology Screenshot

---

## Final Note

This lab is part of the *Bits of Progress* project—documenting the process of learning networking by actually building, breaking, and fixing things. It’s not just about checking off a config—it's about getting better through repetition, inspection, and honest troubleshooting.

