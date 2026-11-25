# Cisco Packet Tracer Network Labs

Network topologies built in Cisco Packet Tracer 8.2 for the Computer Networks course (1st year, Computer Engineering), plus a couple of later cybersecurity labs on ACLs.

Open the `.pkt` files with [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) 8.2 or newer. The `.xlsx` files next to some labs contain the VLSM subnetting calculations used to address them.

| Folder | Topics |
|---|---|
| `01_lan_basics_hub_and_switch` | First LAN: hub vs. switch with 18 PCs |
| `02_multilayer_switch_vlsm_and_dhcp` | 3560 multilayer switch with routed ports, VLSM subnets (/22, /23, /26, /28) and DHCP pools |
| `03_enterprise_departments_and_datacenter` | Company network with two departments (172.16.0.0/21) and a server farm / datacenter, from one to three routers, switch management SVIs, device hardening (`enable secret`, local users, banners) |
| `04_vlans_and_router_on_a_stick` | VLANs, 802.1Q trunks and inter-VLAN routing with router subinterfaces, DHCP per VLAN |
| `05_practical_exam_scenarios` | Practical exam scenarios: school / company networks with VLANs (management, production, teachers, students), VLSM addressing, router-on-a-stick and DHCP |
| `06_access_control_lists` | Standard and extended ACLs on an ISR4331 router |

`cisco_ios_commands_cheatsheet.md` summarises the IOS commands used in these labs (VLANs, router-on-a-stick, DHCP, EtherChannel, STP, device security).
