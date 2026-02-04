Recorrido estatico.

R01:
ip route 192.168.2.0 255.255.255.0 10.0.0.2
ip route 172.20.1.0 255.255.255.0 10.0.0.6
ip route 172.20.2.0 255.255.255.0 10.0.0.6

R02:
ip route 192.168.1.0 255.255.255.0 10.0.0.1
ip route 172.20.1.0 255.255.255.0 10.0.0.10
ip route 172.20.2.0 255.255.255.0 10.0.0.14


R03:
ip route 192.168.1.0 255.255.255.0 10.0.0.5
ip route 192.168.2.0 255.255.255.0 10.0.0.9
ip route 172.20.2.0 255.255.255.0 10.0.0.9


R04:
ip route 192.168.1.0 255.255.255.0 10.0.0.13
ip route 192.168.2.0 255.255.255.0 10.0.0.13
ip route 172.20.1.0 255.255.255.0 10.0.0.13

## TOPOLOGIA:
>R01 → Servidor DHCP
>OSPF área 0 en todos los routers
>LANs:

>> 192.168.1.0/24 → PC0, PC1
>> 192.168.2.0/24 → PC2, PC3
>> 172.20.1.0/24 → PC4
>> 172.20.2.0/24 → PC5

---

# Se implementó un servidor DHCP centralizado en R01 y se utilizó DHCP Relay (ip helper-address) en los routers intermedios para permitir la asignación automática de direcciones IP en redes remotas. El enrutamiento dinámico se realizó mediante OSPF en el área 0.

## PASO 1: CONFIGURAR DHCP EN R01 (SERVIDOR)
1.1 Excluir direcciones (todas las redes)
```bash
R01>en
R01#conf t
ip dhcp excluded-address 192.168.1.1 192.168.1.10
ip dhcp excluded-address 192.168.2.1 192.168.2.10
ip dhcp excluded-address 172.20.1.1 172.20.1.10
ip dhcp excluded-address 172.20.2.1 172.20.2.10
```

---

Pools DHCP

```bash
1.2 Pool DHCP – LAN 192.168.1.0 (PC0, PC1)
ip dhcp pool LAN-192-168-1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
 exit

1.3 Pool DHCP – LAN 192.168.2.0 (PC2, PC3)
ip dhcp pool LAN-192-168-2
 network 192.168.2.0 255.255.255.0
 default-router 192.168.2.1
 dns-server 8.8.8.8
 exit

1.4 Pool DHCP – LAN 172.20.1.0 (PC4)
ip dhcp pool LAN-172-20-1
 network 172.20.1.0 255.255.255.0
 default-router 172.20.1.1
 dns-server 8.8.8.8
 exit

1.5 Pool DHCP – LAN 172.20.2.0 (PC5)
ip dhcp pool LAN-172-20-2
 network 172.20.2.0 255.255.255.0
 default-router 172.20.2.1
 dns-server 8.8.8.8
 exit
end
wr
```

## PASO 2: CONFIGURAR OSPF (EN TODOS LOS ROUTERS)
RO1:
```bash
R01#conf t
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
 network 10.0.0.4 0.0.0.3 area 0
exit
end
wr
```

R02
```bash
R02#conf t
router ospf 1
 router-id 2.2.2.2
 network 192.168.2.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
 network 10.0.0.8 0.0.0.3 area 0
 network 10.0.0.12 0.0.0.3 area 0
exit
end
wr
```

R03
```bash
R03#conf t
router ospf 1
 router-id 3.3.3.3
 network 172.20.1.0 0.0.0.255 area 0
 network 10.0.0.4 0.0.0.3 area 0
 network 10.0.0.8 0.0.0.3 area 0
exit
end
wr
```

RO4
```bash
R04#conf t
router ospf 1
 router-id 4.4.4.4
 network 172.20.2.0 0.0.0.255 area 0
 network 10.0.0.12 0.0.0.3 area 0
exit
end
wr
```

## PASO 3: CONFIGURAR DHCP RELAY (ip helper-address)
Esto permite que DHCP cruce routers

> En R02 (LAN 192.168.2.0)
```bash
interface g0/0/0
 ip helper-address 192.168.1.1
 exit
```

> En R03 (LAN 172.20.1.0)
```bash
interface g0/0/0
 ip helper-address 192.168.1.1
 exit
```

> En R04 (LAN 172.20.2.0)
```bash
interface g0/0/0
 ip helper-address 192.168.1.1
 exit
```

192.168.1.1 = R01 (servidor DHCP)

## PASO 4: CONFIGURAR LAS PCs
En TODAS las PCs (PC0–PC5):

* Desktop
* IP Configuration
* Seleccionar DHCP

Esperar unos segundos.


## PASO 5: VERIFICACIONES (OBLIGATORIO)
DHCP

En R01:
```bash
show ip dhcp binding

Router>show ip dhcp binding
IP address       Client-ID/              Lease expiration        Type
                 Hardware address
192.168.1.11     0001.C712.7D2C           --                     Automatic
192.168.1.12     0040.0BB0.2A7D           --                     Automatic
192.168.2.11     000D.BD6E.72EE           --                     Automatic
192.168.2.12     0060.472B.3CA7           --                     Automatic
172.20.1.11      0010.1199.2011           --                     Automatic
172.20.2.11      0002.171E.479B           --                     Automatic
```
---

OSPF

En cualquier router:
```bash
show ip ospf neighbor

Router>show ip ospf neighbor


Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           0   FULL/  -        00:00:38    10.0.0.2        Serial0/1/1
3.3.3.3           0   FULL/  -        00:00:38    10.0.0.6        Serial0/1/0
```

---

Rutas
```bash
show ip route

Router>show ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

     10.0.0.0/8 is variably subnetted, 6 subnets, 2 masks
C       10.0.0.0/30 is directly connected, Serial0/1/1
L       10.0.0.1/32 is directly connected, Serial0/1/1
C       10.0.0.4/30 is directly connected, Serial0/1/0
L       10.0.0.5/32 is directly connected, Serial0/1/0
O       10.0.0.8/30 [110/128] via 10.0.0.2, 00:02:45, Serial0/1/1
                    [110/128] via 10.0.0.6, 00:02:45, Serial0/1/0
O       10.0.0.12/30 [110/128] via 10.0.0.2, 00:02:45, Serial0/1/1
     172.20.0.0/24 is subnetted, 2 subnets
S       172.20.1.0/24 [1/0] via 10.0.0.6
S       172.20.2.0/24 [1/0] via 10.0.0.6
     192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.1.0/24 is directly connected, GigabitEthernet0/0/0
L       192.168.1.1/32 is directly connected, GigabitEthernet0/0/0
S    192.168.2.0/24 [1/0] via 10.0.0.2

Router>
```