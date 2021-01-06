RCOMP 2019-2020 Project - Sprint 3 - Member 1180813 folder
===========================================

## Building D

In this document the commands used in the CLI to configure the many devices will be shown.

Please take in consideration the following table from the previous sprint:

| VTP Domain  | VLAN ID | Subnet Address  | Net Mask  | Available Address Range  |  Broadcast Address |
|---|---|---|---|---|---|
|  dmz |  303 | 10.166.140.0/24  | 255.255.255.0 | 10.166.140.1 - 10.166.140.254  |  10.166.140.255 |
|  wifi | 302 | 10.166.141.0/26  | 255.255.255.192  | 10.166.141.1 - 10.166.141.62 | 10.166.141.63  |
|  outlets-floor1 |  301 | 10.166.141.64/26  | 255.255.255.192 | 10.166.141.65 - 10.166.141.126   | 10.166.141.127 |
|  outlets-floor0 | 300  | 10.166.141.128/26   | 255.255.255.192  | 10.166.141.129 - 10.166.141.190  | 10.166.141.191  |
|  voip |  304 | 10.166.141.192/27  | 255.255.255.224  | 10.166.141.193 - 10.166.141.222  | 10.166.141.223  |

And take in account these commands ran to configure all the VLANs in the router for Building D:

D_DMZ_VLAN:  
interface FastEthernet 1/0.303  
encapsulation dot1Q 303  
ip address 10.166.140.0 255.255.255.0  
no shutdown  
exit  

D_Floor0_VLAN:  
interface FastEthernet 1/0.300  
encapsulation dot1Q 300  
ip address 10.166.141.128 255.255.255.192  
no shutdown  
exit  

D_Floor1_VLAN:  
interface FastEthernet 1/0.301  
encapsulation dot1Q 301  
ip address 10.166.141.64 255.255.255.192  
no shutdown  
exit  

D_WiFi_VLAN:  
interface FastEthernet 1/0.302  
encapsulation dot1Q 302  
ip address 10.166.141.0 255.255.255.192  
no shutdown  
exit  

D_VoIp_VLAN:  
interface FastEthernet 1/0.304  
encapsulation dot1Q 304  
ip address 10.166.141.192 255.255.255.224  
no shutdown  
exit  

## OSPF Commands

router ospf 101  
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.128.0 255.255.254.0 area 1  

router ospf 202  
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.132.0 255.255.254.0 area 2  

router ospf 303  
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.136.0 255.255.254.0 area 3  

router ospf 404  
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.140.0 255.255.254.0 area 4  

## DNS Commands

ip dhcp pool floor0D  
network 10.166.141.128 255.255.255.192  
default-router 10.166.141.129  
domain-name building-D.rcomp-19-20-de-g3  
dns-server 10.166.140.1  

ip dhcp pool floor1D  
network 10.166.141.64 255.255.255.192  
default-router 10.166.141.65  
domain-name building-D.rcomp-19-20-de-g3  
dns-server 10.166.140.1  

ip dhcp pool wifiD  
network 10.166.141.0 255.255.255.192  
default-router 10.166.141.1  
domain-name building-D.rcomp-19-20-de-g3  
dns-server 10.166.140.1  

ip dhcp pool voipD  
default-router 10.166.141.193  
option 150 ip 10.166.137.161  
network 10.166.141.192 255.255.255.224  
domain-name building-D.rcomp-19-20-de-g3  
dns-server 10.166.140.1  

ip dhcp excluded-address 10.166.141.1  
ip dhcp excluded-address 10.166.141.65  
ip dhcp excluded-address 10.166.141.129  
ip dhcp excluded-address 10.166.141.193  

## VoIP Commands

interface Gig8/1  
switchport mode access  
switchport voice vlan 304  
no switchport access vlan  

interface Gig7/1  
switchport mode access  
switchport voice vlan 304  
no switchport access vlan  

telephony-service  
auto-reg-ephone  
ip source-address 10.166.141.193 port 2000  
max-ephones 25  
max-dn 25  

ephone-dn 1  
number 4001  

ephone-dn 2  
number 4002  

ephone 1  
mac-address 0060.5C42.27CD  
button 1:1  

ephone 2  
mac-address 00D0.9765.E2B0  
button 1:2  

//CAMPUS GERAL (NEW MAC ADRESSES)  
ephone 1  
mac-address 0060.2FD2.17BB  
button 1:1  

ephone 2  
mac-address 00D0.BC35.8444 
button 1:2 
