RCOMP 2019-2020 Project - Sprint 2 - Member 1180813 folder
===========================================

## Information
- End user outlets on the ground floor: 40 nodes
- End user outlets on floor one: 50 nodes
- Wi-Fi network: 60 nodes
- Local servers and administration workstations (DMZ): 250 nodes
- VoIP (IP-phones): 25 nodes


## Distribuction

The range of addresses to my building is 10.166.140.0 to 10.166.143.0.

| VTP Domain  | VLAN ID | Subnet Address  | Net Mask  | Available Address Range  |  Broadcast Address |
|---|---|---|---|---|---|
|  dmz |  303 | 10.166.140.0/24  | 255.255.255.0 | 10.166.140.1 - 10.166.140.254  |  10.166.140.255 |
|  wifi | 302 | 10.166.141.0/26  | 255.255.255.192  | 10.166.141.1 - 10.166.141.62 | 10.166.141.63  |
|  outlets-floor1 |  301 | 10.166.141.64/26  | 255.255.255.192 | 10.166.141.65 - 10.166.141.126   | 10.166.141.127 |
|  outlets-floor0 | 300  | 10.166.141.128/26   | 255.255.255.192  | 10.166.141.129 - 10.166.141.190  | 10.166.141.191  |
|  voip |  304 | 10.166.141.192/27  | 255.255.255.224  | 10.166.141.193 - 10.166.141.222  | 10.166.141.223  |


## Notes

- The switch called "MainCrossConnect" is the one assuming the server role, because that switch is simulating the connection to the main cross connect.
