RCOMP 2019-2020 Project - Sprint 2 - Member 1171060 folder
===========================================

## Information
- End user outlets on the ground floor: 60 nodes
- End user outlets on floor one: 70 nodes
- Wi-Fi network: 100 nodes
- Local servers and administration workstations (DMZ): 12 nodes
- VoIP (IP-phones): 35 nodes


## Distribuction

The range of addresses to my building is 10.166.132.0 to 10.166.135.0.

| VTP Domain  | VLAN ID | Subnet Address  | Net Mask  | Available Address Range  |  Broadcast Address |
|---|---|---|---|---|---|
|  B_Wifi_VLAN | 282  | 10.166.132.0/25   | 255.255.255.128  | 10.166.132.1 - 10.166.132.126  | 10.166.132.127  |
|  B_Floor1_VLAN |  281 | 10.166.132.128/25  | 255.255.255.128 | 10.166.132.129 - 10.166.132.254   | 10.166.132.255 |
|  B_Floor0_VLAN | 280  | 10.166.133.0/26  | 255.255.255.192  | 10.166.133.1 - 10.166.133.62  | 10.166.133.63  |
|  B_VoIP_VLAN |  284 | 10.166.133.64/26  | 255.255.255.192 | 10.166.133.65 - 10.166.133.126  |  10.166.133.127 |
|  B_DMZ_VLAN |  283 | 10.166.133.128/28  | 255.255.255.240  | 10.166.133.129 - 10.166.133.142  | 10.166.133.143  |


## Notes

- The switch called "ConnectionSwitch" is the one assuming the server role, because that switch is simulating the connection to the main cross connect.
