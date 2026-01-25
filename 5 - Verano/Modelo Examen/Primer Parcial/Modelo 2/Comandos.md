1.1 Excluir direcciones (todas las redes)
```bash
ip dhcp excluded-address 192.168.4.1 192.168.4.3

```
Pool DHCP – LAN 192.168.4.0 (DNS, WEB)
```bash
ip dhcp pool LAN-192-168-4
 network 192.168.4.0 255.255.255.248
 default-router 192.168.4.1
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