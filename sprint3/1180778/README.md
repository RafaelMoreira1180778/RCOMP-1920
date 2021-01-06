RCOMP 2019-2020 Project - Sprint 3 - Member 1180778 folder
===========================================
# BUILDING A

I will show in this document all the necessary commands to run in the varius devices for my configuration to work.

Please take in consideration the following table from the previous sprint:

```
| VTP Domain    | VLAN ID | Subnet Address    | Net Mask        | Available Address Range         | Broadcast Address |
| ------------- | ------- | ----------------- | --------------- | ------------------------------- | ----------------- |
| BACKBONE      | 290     | 10.166.136.0/25   | 255.255.255.128 | 10.166.136.1 - 10.166.137.126   | 10.166.137.127    |
| A_DMZ_VLAN    | 291     | 10.166.136.128/25 | 255.255.255.128 | 10.166.136.129 - 10.166.136.254 | 10.166.136.255    |
| A_Floor0_VLAN | 292     | 10.166.137.0/26   | 255.255.255.192 | 10.166.137.1 - 10.166.137.62    | 10.166.137.63     |
| A_Floor1_VLAN | 293     | 10.166.137.64/26  | 255.255.255.192 | 10.166.137.65 - 10.166.137.126  | 10.166.137.127    |
| A_Wifi_VLAN   | 294     | 10.166.137.128/27 | 255.255.255.224 | 10.166.137.129 - 10.166.137.158 | 10.166.137.159    |
| A_VoIP_VLAN   | 295     | 10.166.137.160/27 | 255.255.255.224 | 10.166.137.161 - 10.166.137.190 | 10.166.137.191    |
```

And take in account these commands ran to configure all the vlans in the router for Building A:

#### BACKBONE:  
```
interface FastEthernet 1/0.290  
encapsulation dot1Q 290  
ip address 10.166.136.1 255.255.255.128  
no shutdown  
exit  
```

#### A_DMZ:  
```
interface FastEthernet 1/0.291  
encapsulation dot1Q 291  
ip address 10.166.136.129 255.255.255.128  
no shutdown  
exit  
```

#### A_Floor0:  
```
interface FastEthernet 1/0.292  
encapsulation dot1Q 292  
ip address 10.166.137.1 255.255.255.192  
no shutdown  
exit  
```

#### A_Floor1_VLAN:  
```
interface FastEthernet 1/0.293  
encapsulation dot1Q 293  
ip address 10.166.137.65 255.255.255.192  
no shutdown  
exit  
```

#### A_Wifi_VLAN: 
``` 
interface FastEthernet 1/0.294  
encapsulation dot1Q 294  
ip address 10.166.137.129 255.255.255.224  
no shutdown  
exit  
```

#### A_VoIP_VLAN:  
```
interface FastEthernet 1/0.295  
encapsulation dot1Q 295  
ip address 10.166.137.161 255.255.255.224  
no shutdown  
exit  
```


# OSPF COMMANDS

#### BUILDING A:
```
no router ospf 1
router ospf 1
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.136.0 255.255.254.0 area 1  
```

#### BUILDING B:
```
no router ospf 1
router ospf 1
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.132.0 255.255.254.0 area 2  
```

#### BUILDING C:
```
no router ospf 1
router ospf 1
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.128.0 255.255.254.0 area 3  
```

#### BUILDING D:
```
no router ospf 1
router ospf 1
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.140.0 255.255.254.0 area 4 
```

#### FOR THE MAIN ROUTER:
```
no router ospf 1
router ospf 1
network 10.166.142.0 255.255.254.0 area 0  
network 10.166.136.0 255.255.254.0 area 1  
network 10.166.132.0 255.255.254.0 area 2  
network 10.166.128.0 255.255.254.0 area 3 
network 10.166.140.0 255.255.254.0 area 4 
```

# DNS COMMANDS

```
ip dhcp pool A_DMZ  
network 10.166.137.128 255.255.255.224  
default-router 10.166.136.129
domain-name rcomp-19-20-de-g3  
dns-server 10.166.136.130  
```

```
ip dhcp pool A_Wifi_VLAN  
network 10.166.137.128 255.255.255.224  
default-router 10.166.137.129  
domain-name rcomp-19-20-de-g3  
dns-server 10.166.136.130  
```

```
ip dhcp pool A_Floor0_VLAN  
network 10.166.137.0 255.255.255.192  
default-router 10.166.137.1  
domain-name rcomp-19-20-de-g3  
dns-server 10.166.136.130  
```

```
ip dhcp pool A_Floor1_VLAN  
network 10.166.137.64 255.255.255.192  
default-router 10.166.137.65  
domain-name rcomp-19-20-de-g3  
dns-server 10.166.136.130  
```

```
ip dhcp pool A_VoIP_VLAN  
default-router 10.166.137.161  
option 150 ip 10.166.137.161  
network 10.166.137.160 255.255.255.224  
domain-name rcomp-19-20-de-g3  
dns-server 10.166.136.130  
```

```
ip dhcp excluded-address 10.166.136.129
ip dhcp excluded-address 10.166.137.129  
ip dhcp excluded-address 10.166.137.1  
ip dhcp excluded-address 10.166.136.161  
ip dhcp excluded-address 10.166.137.65  
```


# VoIP COMMANDS

```
interface Fa2/1  
switchport mode access  
switchport voice vlan 295  
no switchport access vlan  
```

```
interface Fa1/1  
switchport mode access  
switchport voice vlan 295  
no switchport access vlan  
```

```
telephony-service  
auto-reg-ephone  
ip source-address 10.166.137.161 port 2000  
max-ephones 20  
max-dn 20  
auto assign 1 to 2  
```

```
ephone-dn 1  
number 1001  
ephone-dn 2  
number 1002
```

#### BUILDING A:
```
dial-peer voice 1000 voip
destination-pattern 1...
session target ipv4:10.166.137.161
```

#### BUILDING B:
```
dial-peer voice 2000 voip
destination-pattern 2...
session target ipv4:10.166.133.65
```

#### BUILDING C:
```
dial-peer voice 3000 voip
destination-pattern 3...
session target ipv4:10.166.129.193
```

#### BUILDING D:
```
dial-peer voice 4000 voip
destination-pattern 4...
session target ipv4:10.166.141.193
```

# DNS

#### Here is the result of the generated DNS, as requested in Sprint3:

```
| No. | Name                            | Type     | Detail               |
|-----|---------------------------------|----------|----------------------|
| 0   | dns                             | CNAME    | rcomp-19-20-de-g3    |
| 1   | ns                              | CNAME    | ns.rcomp-19-20-de-g3 |
| 2   | ns.building-b.rcomp-19-20-de-g3 | A Record | 10.166.133.130       |
| 3   | ns.building-c.rcomp-19-20-de-g3 | A Record | 10.166.128.0         |
| 4   | ns.building-d.rcomp-19-20-de-g3 | A Record | 10.166.140.1         |
| 5   | server1                         | A Record | 10.166.136.130       |
| 6   | web                             | CNAME    | server1              |
| 7   | www                             | CNAME    | server1              |
```

As can be seen, I have created a dns link to all the servers from the other buildings using their IP addresses.

# NAT COMMANDS

```
ip nat inside source static tcp 10.166.136.130 80 10.166.136.0 8081
ip nat inside source static tcp 10.166.136.130 443 10.166.136.0 8082
```