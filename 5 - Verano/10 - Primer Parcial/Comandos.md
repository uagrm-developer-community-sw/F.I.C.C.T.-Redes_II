en la x reemplaza tu numero

R5 DHCP
en
config t

ip dhcp excluded-address 100.x.1.129
ip dhcp excluded-address 100.x.1.1
ip dhcp excluded-address 172.x.1.1
ip dhcp excluded-address 200.x.8.1
ip dhcp excluded-address 192.x.1.17
ip dhcp excluded-address 192.x.1.1

ip dhcp pool 32HOSTS
network 100.x.1.128 255.255.255.192
default-router 100.x.1.129
dns-server 8.8.8.8

ip dhcp pool 64HOSTS
network 100.x.1.0 255.255.255.128
default-router 100.x.1.1
dns-server 8.8.8.8

ip dhcp pool RED172
network 172.x.1.0 255.255.255.0
default-router 172.x.1.1
dns-server 8.8.8.8

ip dhcp pool RED200
network 200.x.8.0 255.255.255.248
default-router 200.x.8.1
dns-server 8.8.8.8

ip dhcp pool 10HOSTS
network 192.x.1.16 255.255.255.240
default-router 192.x.1.17
dns-server 8.8.8.8

ip dhcp pool 11HOSTS
network 192.x.1.0 255.255.255.240
default-router 192.x.1.1
dns-server 8.8.8.8

R1

en
config t
int g0/0/0
ip add 100.x.1.129 255.255.255.192
no sh
ip helper-address 10.x.0.34
exit

int se0/1/0
ip add 10.x.0.1 255.255.255.248
no sh
exit

R2

en
config t
int se0/1/0
ip add 10.x.0.2 255.255.255.248
no sh
exit

int gi0/0/0
ip add 100.x.1.1 255.255.255.128
no sh
ip helper-address 10.x.0.34
exit

int se0/2/0
ip add 10.x.0.17 255.255.255.248
no sh
exit

int se0/1/1
ip add 10.x.0.9 255.255.255.248
no sh
exit

R3

en
config t
int se0/1/1
ip add 10.x.0.10 255.255.255.248
no sh
exit

int se0/2/1
ip add 10.x.0.25 255.255.255.248
no sh
exit

int se0/1/0
ip add 10.x.0.33 255.255.255.248
no sh
exit

R4

en
config t
int se0/2/0
ip add 10.x.0.18 255.255.255.248
no sh
exit

int se0/2/1
ip add 10.x.0.26 255.255.255.248
no sh
exit

int g0/0/0
ip add 172.x.1.1 255.255.255.0
no sh
ip helper-address 10.x.0.34
exit

R5

en
config t
int se0/1/0
ip add 10.x.0.34 255.255.255.248
no sh
exit

int se0/1/1
ip add 10.x.0.41 255.255.255.248
no sh
exit

int se0/2/0
ip add 10.x.0.49 255.255.255.248
no sh
exit

R6

en
config t
int se0/1/1
ip add 10.x.0.42 255.255.255.248
no sh
exit

int g0/0/0
ip add 200.x.8.1 255.255.255.248
no sh
exit

R7

en
config t
int se0/2/0
ip add 10.x.0.50 255.255.255.248
no sh
exit

int g0/0/0
ip add 192.x.1.17 255.255.255.240
no sh
ip helper-address 10.x.0.49
exit

int g0/0/1
ip add 192.x.1.1 255.255.255.240
no sh
ip helper-address 10.x.0.49
exit

enrutamiento ospf

R3
en
config t
router ospf x
network 10.x.0.32 0.0.0.7 area 0


R5
en
config t
router ospf x
network 10.x.0.32 0.0.0.7 area 0
network 10.x.0.40 0.0.0.7 area 0
network 10.x.0.48 0.0.0.7 area 0

R7
en
config t
router ospf x
network 192.x.1.16 0.0.0.15 area 0
network 192.x.1.0 0.0.0.15 area 0
network 10.x.0.48 0.0.0.7 area 0

eigrp
R2
router eigrp x
no auto-summary
network 10.x.0.8 0.0.0.7
network 10.x.0.16 0.0.0.7

R3
router eigrp x
no auto-summary
network 10.x.0.8 0.0.0.7
network 10.x.0.24 0.0.0.7

R4

router eigrp x
no auto-summary
network 10.x.0.16 0.0.0.7
network 10.x.0.24 0.0.0.7
network 172.x.1.0 0.0.0.255

RIPv2

R1
router rip
version 2
no auto-summary
network 100.x.1.128
network 10.x.0.0

R2

router rip
version 2
no auto-summary
network 10.x.0.0
network 100.x.1.0

R2
router eigrp x
redistribute rip metric 10000 100 255 1 1500

router rip
version 2
redistribute eigrp x metric 5

edistribución eigrp- ospf
R3
router ospf x
redistribute eigrp x subnets

router eigrp x
no auto-summary
redistribute ospf x metric 10000 100 255 1 1500