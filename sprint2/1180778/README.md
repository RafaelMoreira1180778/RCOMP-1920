RCOMP 2019-2020 Project - Sprint 2 - Member 1180778 folder
===========================================
## Information
- End user outlets on the ground floor: 40 nodes
- End user outlets on floor one: 40 nodes
- Wi-Fi network: 24 nodes
- Local servers and administration workstations (DMZ): 70 nodes
- VoIP (IP-phones): 20 nodes
- Backbone: 120 nodes


## Distribuction

Available IP values: from 10.166.136.0/20 to 10.166.139.0/20 (4094 nodes).

| VTP Domain  | VLAN ID | Subnet Address  | Net Mask  | Available Address Range  |  Broadcast Address |
|---|---|---|---|---|---|
|  BACKBONE |  290 | 10.166.136.0/25  | 255.255.255.128  | 10.166.136.1 - 10.166.137.126  | 10.166.137.127  |
|  A_DMZ_VLAN |  291 | 10.166.136.128/25  | 255.255.255.128  | 10.166.136.129 - 10.166.136.254  | 10.166.136.255  |
|  A_Floor0_VLAN | 292  | 10.166.137.0/26  | 255.255.255.192  | 10.166.137.1 - 10.166.137.62  | 10.166.137.63  |
|  A_Floor1_VLAN | 293 | 10.166.137.64/26  | 255.255.255.192  | 10.166.137.65 - 10.166.137.126  | 10.166.137.127  |
|  A_Wifi_VLAN | 294 | 10.166.137.128/27   | 255.255.255.224  | 10.166.137.129 - 10.166.137.158  | 10.166.137.159  |
|  A_VoIP_VLAN |  295 | 10.166.137.160/27  | 255.255.255.224 | 10.166.137.161 - 10.166.137.190  |  10.166.137.191 |


I had the task to build the campus.pkt so all the configurations were included in the folder 'configuration dump'. I aknowledge that some pings are faulty but we believe that our configurations of both the static routing tables and the subnets are correct.
