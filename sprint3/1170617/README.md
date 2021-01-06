RCOMP 2019-2020 Project - Sprint 3 - Member 1170617 folder
===========================================
# BUILDING C

In this document there will be all the commands I used to configurate different devices.

| VTP Domain  | VLAN ID | Subnet Address  | Net Mask  | Available Address Range  |  Broadcast Address |
|---|---|---|---|---|---|
|  C_DMZ_VLAN |  273 | 10.166.128.0/24  | 255.255.255.0  | 10.166.128.1 - 10.166.128.254  | 10.166.128.255  |
|  C_Wifi_VLAN | 272  | 10.166.129.0/26   | 255.255.255.192  | 10.166.129.1 - 10.166.129.62  | 10.166.129.63  |
|  C_Floor1_VLAN |  271 | 10.166.129.64/26  | 255.255.255.192 | 10.166.129.65 - 10.166.129.126   | 10.166.129.127 |
|  C_Floor0_VLAN | 270  | 10.166.129.128/26  | 255.255.255.192  | 10.166.129.129 - 10.166.129.190  | 10.166.129.191  |
|  C_VoIP_VLAN |  274 | 10.166.129.192/26  | 255.255.255.192 | 10.166.129.193 - 10.166.129.254  |  10.166.129.255 |



C_DMZ_VLAN:
interface FastEthernet 1/0.273
encapsulation dot1Q 273
ip address 10.166.128.1 255.255.255.0
no shutdown
exit

C_Wifi_VLAN:
interface FastEthernet 1/0.272
encapsulation dot1Q 272
ip address 10.166.129.1 255.255.255.192
no shutdown
exit

C_Floor1_VLAN:
interface FastEthernet 1/0.271
encapsulation dot1Q 271
ip address 10.166.129.65 255.255.255.192
no shutdown
exit

C_Floor0_VLAN:
interface FastEthernet 1/0.270
encapsulation dot1Q 270
ip address 10.166.129.129 255.255.255.192
no shutdown
exit

C_VoIP_VLAN:
interface FastEthernet 1/0.274
encapsulation dot1Q 274
ip address 10.166.129.193 255.255.255.192
no shutdown
exit


# OSPF COMMANDS #

#### BUILDING C:
no router ospf 1
router ospf 1
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.128.0 255.255.254.0 area 3


# DHCP / DNS COMMANDS #

ip dhcp pool C_DMZ_VLAN  
network 10.166.133.128 255.255.255.240
default-router 10.166.133.129
domain-name rcomp-19-20-de-g3  
dns-server 10.166.128.1  

ip dhcp pool C_Wifi_VLAN  
network 10.166.129.1 255.255.255.192
default-router 10.166.129.2
domain-name rcomp-19-20-de-g3  
dns-server 10.166.128.1  

ip dhcp pool C_Floor0_VLAN  
network 10.166.129.129 255.255.255.192
default-router 10.166.129.130
domain-name rcomp-19-20-de-g3  
dns-server 10.166.128.1

ip dhcp pool C_Floor1_VLAN  
network 10.166.129.65 255.255.255.192
default-router 10.166.129.66
domain-name rcomp-19-20-de-g3  
dns-server 10.166.128.1

ip dhcp pool C_VoIP_VLAN  
default-router 10.166.129.194
option 150 ip 10.166.129.194
network 10.166.129.193 255.255.255.192
domain-name rcomp-19-20-de-g3  
dns-server 10.166.128.1  

ip dhcp excluded-address 10.166.133.129
ip dhcp excluded-address 10.166.129.2
ip dhcp excluded-address 10.166.129.130
ip dhcp excluded-address 10.166.129.66    
ip dhcp excluded-address 10.166.129.194


# VoIP COMMANDS #

interface FastEthernet7/1  
switchport mode access  
switchport voice vlan 284  
no switchport access vlan


interface FastEthernet5/1  
switchport mode access  
switchport voice vlan 295  
no switchport access vlan  



telephony-service  
auto-reg-ephone  
ip source-address 10.166.129.193 port 2000  
max-ephones 25
max-dn 20  
auto assign 1 to 2


ephone-dn 1  
number 3001  
ephone-dn 2  
number 3002

dial-peer voice 3000 voip
destination-pattern 3...
session target ipv4:10.166.129.193

# DNS #



# NAT COMMANDS #

ip nat inside source static tcp 10.166.133.130 80 10.166.136.0 8081
ip nat inside source static tcp 10.166.133.130 443 10.166.136.0 8082
