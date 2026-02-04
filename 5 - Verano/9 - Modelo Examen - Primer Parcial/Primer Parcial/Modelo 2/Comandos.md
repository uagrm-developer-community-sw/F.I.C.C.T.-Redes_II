1.1 Excluir direcciones (todas las redes)
```bash
ip dhcp excluded-address 192.168.4.1 192.168.4.3

ip dhcp excluded-address 192.168.0.129 192.168.0.139
ip dhcp excluded-address 192.168.1.1 192.168.1.11
ip dhcp excluded-address 192.168.3.1 192.168.3.11
ip dhcp excluded-address 192.168.2.1 192.168.2.11

```
Pool DHCP – LAN 192.168.4.0
```bash
ip dhcp pool LAN-192-168-4
 network 192.168.4.0 255.255.255.248
 default-router 192.168.4.1
 dns-server 8.8.8.8
 ```

 ```bash
ip dhcp pool LAN-192.168.0
 network 192.168.0.128 255.255.255.128
 default-router 192.168.0.129
 dns-server 8.8.8.8
 ```

 ```bash
ip dhcp pool LAN-192.168.1
 network 192.168.1.0 255.255.255.128
 default-router 192.168.1.1
 dns-server 8.8.8.8
 ```

  ```bash
ip dhcp pool LAN-192.168.3
 network 192.168.3.0 255.255.255.128
 default-router 192.168.3.1
 dns-server 8.8.8.8
 ```

 ```bash
ip dhcp pool LAN-192.168.2
 network 192.168.2.0 255.255.255.128
 default-router 192.168.2.1
 dns-server 8.8.8.8
 ```

## PASO 2: CONFIGURAR OSPF (EN TODOS LOS ROUTERS)

```bash
router ospf 1
 router-id 1.1.1.1
 network 192.168.4.0 0.0.0.7 area 0
 network 192.168.1.132 0.0.0.3 area 0
 network 192.168.1.136 0.0.0.3 area 0
```

R01
```bash
router ospf 1
 router-id 1.1.1.1
 network 192.168.0.128 0.0.0.127 area 0
 network 192.168.0.8 0.0.0.3 area 0
 network 192.168.0.0 0.0.0.3 area 0
```

R03
```bash
router ospf 1
 router-id 3.3.3.3
 network 192.168.1.0 0.0.0.127 area 0
 network 192.168.0.4 0.0.0.3 area 0
 network 192.168.0.8 0.0.0.3 area 0
```

R04
```bash
router ospf 1
 router-id 4.4.4.4
 network 192.168.3.0 0.0.0.127 area 0
 network 192.168.1.152 0.0.0.3 area 0
 network 192.168.1.148 0.0.0.3 area 0
```

R05
```bash
router ospf 1
 router-id 5.5.5.5
 network 192.168.2.0 0.0.0.127 area 0
 network 192.168.1.152 0.0.0.3 area 0
 network 192.168.1.144 0.0.0.3 area 0
```