RCOMP 2019-2020 Project - Sprint 2 - Member 1170617 folder
===========================================

## Information
- End user outlets on the ground floor: 40 nodes
- End user outlets on floor one: 44 nodes
- Wi-Fi network: 60 nodes
- Local servers and administration workstations (DMZ): 250 nodes
- VoIP (IP-phones): 40 nodes


## Distribuction

The range of addresses to my building is 10.166.128.0 to 10.166.131.0

| VTP Domain  | VLAN ID | Subnet Address  | Net Mask  | Available Address Range  |  Broadcast Address |
|---|---|---|---|---|---|
|  C_DMZ_VLAN |  273 | 10.166.128.0/24  | 255.255.255.0  | 10.166.128.1 - 10.166.128.254  | 10.166.128.255  |
|  C_Wifi_VLAN | 272  | 10.166.129.0/26   | 255.255.255.192  | 10.166.129.1 - 10.166.129.62  | 10.166.129.63  |
|  C_Floor1_VLAN |  271 | 10.166.129.64/26  | 255.255.255.192 | 10.166.129.65 - 10.166.129.126   | 10.166.129.127 |
|  C_Floor0_VLAN | 270  | 10.166.129.128/26  | 255.255.255.192  | 10.166.129.129 - 10.166.129.190  | 10.166.129.191  |
|  C_VoIP_VLAN |  274 | 10.166.129.192/26  | 255.255.255.192 | 10.166.129.193 - 10.166.129.254  |  10.166.129.255 |
