Configuración OSPF

SWML01
enable
configure terminal
ip routing
router ospf 1
network 10.10.0.0 0.0.0.3 area 0
network 192.168.0.0 0.0.0.31 area 0
network 192.168.x.32 0.0.0.31 area 0
network 192.168.x.64 0.0.0.31 area 0

SWML02
enable
configure terminal
ip routing
router ospf 1
network 10.10.0.4 0.0.0.3 area 0
network 192.168.x.0 0.0.0.31 area 0
network 192.168.x.32 0.0.0.31 area 0
network 192.168.x.64 0.0.0.31 area 0

R02
enable
configure terminal
router ospf 1
network 10.10.0.0 0.0.0.3 area 0
network 10.10.0.4 0.0.0.3 area 0
network 10.10.0.8 0.0.0.3 area 0
network 10.10.0.12 0.0.0.3 area 0

DHCP
enable
configure terminal
router ospf 1
network 10.10.0.8 0.0.0.3 area 0
network 10.10.0.16 0.0.0.3 area 0

R03
enable
configure terminal
router ospf 1
network 10.10.0.16 0.0.0.3 area 0
network 10.10.0.12 0.0.0.3 area 0
network 10.10.0.24 0.0.0.3 area 0
network 10.10.0.20 0.0.0.3 area 0

R04
enable
configure terminal
router ospf 1
network 10.10.0.24 0.0.0.3 area 0
network 10.10.0.20 0.0.0.3 area 0
network 192.168.x.96 0.0.0.31 area 0
network 192.168.x.128 0.0.0.31 area 0
network 192.168.0.160 0.0.0.31 area 0

R05
enable
configure terminal
router ospf 1
network 10.10.0.20 0.0.0.3 area 0
network 192.168.x.96 0.0.0.31 area 0
network 192.168.x.128 0.0.0.31 area 0
network 192.168.x.160 0.0.0.31 area 0

DHCP
enable
configure termina
ip dhcp excluded-address 192.168.X.1 192.168.X.5
ip dhcp excluded-address 192.168.X.33 192.168.X.37
ip dhcp excluded-address 192.168.X.65 192.168.X.69
ip dhcp excluded-address 192.168.X.97 192.168.X.101
ip dhcp excluded-address 192.168.X.129 192.168.X.134
ip dhcp excluded-address 192.168.X.161 192.168.X.165

ip dhcp pool VLAN10
network 192.168.X.0 255.255.255.224
default-router 192.168.X.5
dns-server 8.8.8.8

ip dhcp pool VLAN20
network 192.168.X.32 255.255.255.224
default-router 192.168.X.37
dns-server 8.8.8.8

ip dhcp pool VLAN30
network 192.168.X.64 255.255.255.224
default-router 192.168.X.69
dns-server 8.8.8.8

ip dhcp pool VLAN40
network 192.168.X.96 255.255.255.224
default-router 192.168.X.101
dns-server 8.8.8.8

ip dhcp pool VLAN50
network 192.168.X.128 255.255.255.224
default-router 192.168.X.134
dns-server 8.8.8.8

ip dhcp pool VLAN60
network 192.168.X.160 255.255.255.224
default-router 192.168.X.165
dns-server 8.8.8.8

VLANS

SW01
enable
config t
vlan 10
name VLAN10
vlan 20
name VLAN20
vlan 30
name VLAN30
vlan 40
name VLAN40
vlan 50
name VLAN50
vlan 60
name VLAN60
exit
interface range fastEthernet 0/6-10
switchport mode access
switchport access vlan 10
interface range fastEthernet 0/11-15
switchport mode access
switchport access vlan 20 
interface range fastEthernet 0/16-20
switchport mode access
switchport access vlan 30

SW02
enable
config t
vlan 10
name VLAN10
vlan 20
name VLAN20
vlan 30
name VLAN30
vlan 40
name VLAN40
vlan 50
name VLAN50
vlan 60
name VLAN60
exit
interface range fastEthernet 0/6-10
switchport mode access
switchport access vlan 10
interface range fastEthernet 0/11-15
switchport mode access
switchport access vlan 20 
interface range fastEthernet 0/16-20
switchport mode access
switchport access vlan 30


SW03
enable
config t
vlan 10
name VLAN10
vlan 20
name VLAN20
vlan 30
name VLAN30
vlan 40
name VLAN40
vlan 50
name VLAN50
vlan 60
name VLAN60
exit
interface range fastEthernet 0/6-10
switchport mode access
switchport access vlan 10
interface range fastEthernet 0/11-15
switchport mode access
switchport access vlan 20 
interface range fastEthernet 0/16-20
switchport mode access
switchport access vlan 30



SW04
enable
config t
vlan 10
name VLAN10
vlan 20
name VLAN20
vlan 30
name VLAN30
vlan 40
name VLAN40
vlan 50
name VLAN50
vlan 60
name VLAN60
exit

interface range fastEthernet 0/1-5
switchport mode access
switchport access vlan 40
interface range fastEthernet 0/6-10
switchport mode access
switchport access vlan 30 
interface range fastEthernet 0/11-15
switchport mode access
switchport access vlan 60

SW05
enable
config t
vlan 10
name VLAN10
vlan 20
name VLAN20
vlan 30
name VLAN30
vlan 40
name VLAN40
vlan 50
name VLAN50
vlan 60
name VLAN60
exit
interface range fastEthernet 0/1-5
switchport mode access
switchport access vlan 40
interface range fastEthernet 0/6-10
switchport mode access
switchport access vlan 30 
interface range fastEthernet 0/11-15
switchport mode access
switchport access vlan 60

SWML01
enable
config t
vlan 10
name VLAN10
vlan 20
name VLAN20
vlan 30
name VLAN30
vlan 40
name VLAN40
vlan 50
name VLAN50
vlan 60
name VLAN60
exit

SWML02
enable
config t
vlan 10
name VLAN10
vlan 20
name VLAN20
vlan 30
name VLAN30
vlan 40
name VLAN40
vlan 50
name VLAN50
vlan 60
name VLAN60
exit

SWML03
enable
config t
vlan 10
name VLAN10
vlan 20
name VLAN20
vlan 30
name VLAN30
vlan 40
name VLAN40
vlan 50
name VLAN50
vlan 60
name VLAN60
exit

[15:16, 6/2/2026] +591 60823278: HSRP

SWML01
int vlan 10
ip add 192.168.x.1 255.255.255.224
standby 1 ip 192.168.x.5
standby 1 priority 150
standby 1 preempt
no sh

int vlan 20
ip add 192.168.x.33 255.255.255.224
standby 2 ip 192.168.x.37
standby 2 priority 150
standby 2 preempt
no sh

int vlan 30
ip add 192.168.x.65 255.255.255.224
standby 3 ip 192.168.x.69
standby 3 priority 150
standby 3 preempt
no sh

SWML02
int vlan 10
ip add 192.168.x.2 255.255.255.224
standby 1 ip 192.168.x.5
standby 1 priority 100
no sh

int vlan 20
ip add 192.168.x.34 255.255.255.224
standby 2 ip 192.168.x.37
standby 2 priority 100
no sh

int vlan 30
ip add 192.168.x.66 255.255.255.224
standby 3 ip 192.168.x.69
standby 3 priority 100
no sh
[15:31, 6/2/2026] +591 60823278: R4
int gi 0/0/0
no sh
int gi 0/0/0.40
encapsulation dot1Q 40
ip add 192.168.x.97 255.255.255.224
no sh
int gi 0/0/0.50
encapsulation dot1Q 50
ip add 192.168.x.129 255.255.255.224
no sh
int gi 0/0/0.60
encapsulation dot1Q 60
ip add 192.168.x.161 255.255.255.224
no sh


R5

int gi 0/0/0
no sh
int gi 0/0/0.40
encapsulation dot1Q 40
ip add 192.168.x.98 255.255.255.224
no sh
int gi 0/0/0.50
encapsulation dot1Q 50
ip add 192.168.x.130 255.255.255.224
no sh
int gi 0/0/0.60
encapsulation dot1Q 60
ip add 192.168.x.162 255.255.255.224
no sh

R4
int gi 0/0/0.40
standby 1 ip 192.168.X.101
standby 1 priority 150
standby 1 preempt

int gi 0/0/0.50
standby 2 ip 192.168.X.134
standby 2 priority 150
standby 2 preempt

int gi 0/0/0.60
standby 3 ip 192.168.X.165
standby 3 priority 150
standby 3 preempt

R5
int gi 0/0/0.40
standby 1 ip 192.168.X.101
standby 1 priority 100

int gi 0/0/0.50
standby 2 ip 192.168.X.134
standby 2 priority 100

int gi 0/0/0.60
standby 3 ip 192.168.X.165
standby 3 priority 100

CONTINUACION HSRP

ETHERCHANNEL

SWML01
en
config t
int range gi1/0/10-11
sw mode trunk
channel-protocol lacp
channel-group 1 mode active
exit
int port-channel 1
switchport mode trunk
exit


SWML02
en
config t
int range gi1/0/10-11
sw mode trunk
channel-protocol lacp
channel-group 1 mode active
exit
int port-channel 1
switchport mode trunk
exit

SWML03
en
config t
int range gi1/0/21-22
sw mode trunk
channel-protocol lacp
channel-group 1 mode active
exit
int port-channel 1
switchport mode trunk
exit

int range gi1/0/23-24
sw mode trunk
channel-protocol lacp
channel-group 2 mode active
exit
int port-channel 2
switchport mode trunk
exit


SW04
en
config t
int range gi0/1-2
sw mode trunk
channel-protocol lacp
channel-group 1 mode active
exit
int port-channel 1
switchport mode trunk
exit


SW05
en
config t
int range gi0/1-2
sw mode trunk
channel-protocol lacp
channel-group 2 mode active
exit
int port-channel 2
switchport mode trunk
exit