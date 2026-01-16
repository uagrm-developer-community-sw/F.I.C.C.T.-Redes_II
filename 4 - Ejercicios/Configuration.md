Router>en
Router#conf t
Router(config)#host R1

R1(config)#int gig0/0/0
R1(config-if)#ip add 192.168.1.1 255.255.255.0
R1(config-if)#no sh
R1(config-if)#exit

R1(config)#int se0/2/0
R1(config-if)#ip add 10.0.0.1 255.255.255.252
R1(config-if)#no sh

R1(config-if)#do wr
R1(config-if)#exit

-----  enrrutando estaticamente para llegar a la otra red ------
R1(config)#ip route 192.168.2.0 255.255.255.0 10.0.0.2
R1(config)#ip route 192.168.3.0 255.255.255.0 10.0.0.2
R1(config)#ip route 10.0.0.4 255.255.255.252 10.0.0.2
R1(config)#do wr



show ip interface brief
show ip route
ping 192.168.2.1
ping 192.168.3.1


copy running-config startup-config

write