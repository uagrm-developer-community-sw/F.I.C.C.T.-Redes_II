## R01
```bash
R01>en
R01#conf t
R01(config)#host R01
R01(config)#int g0/0/0
R01(config-if)#ip add 192.168.1.1 255.255.255.192
R01(config-if)#do sh
R01(config-if)#exit
R01(config)#do wr

R01(config)#int g0/0/1
R01(config-if)#ip add 192.168.1.129 255.255.255.252
R01(config-if)#do sh
R01(config-if)#exit
R01(config)#do wr

! Rutas estáticas
R01(config)ip route 192.168.1.64 255.255.255.192 192.168.1.130
R01(config)ip route 192.168.2.0 255.255.255.0 192.168.1.130

R01(config)#exit
R01#write
```

---

## R02

```bash
R02>en
R02#conf t
R02(config)#host R02
R02(config)#int g0/0/1
R02(config-if)#ip add 192.168.1.130 255.255.255.252
R02(config-if)#do sh
R02(config-if)#exit
R02(config)#do wr

R02(config)#int g0/0/0
R02(config-if)#ip add 192.168.1.65 255.255.255.192
R02(config-if)#do sh
R02(config-if)#exit
R02(config)#do wr

R02(config)#int se0/1/0
R02(config-if)#ip add 10.0.0.1 255.255.255.252
R02(config-if)#do sh
R02(config-if)#exit
R02(config)#do wr

! Rutas estáticas
R02(config)#ip route 192.168.1.0 255.255.255.192 192.168.1.129
R02(config)#ip route 192.168.2.0 255.255.255.0 10.0.0.2

R02(config)#exit
R02#write
```
---

## R03

```bash
R03>en
R03#conf t
R03(config)#host R03
R03(config)#int se0/1/0
R03(config-if)#ip add 10.0.0.2 255.255.255.252
R03(config-if)#do sh
R03(config-if)#exit
R03(config)#do wr

R03(config)#int g0/0/0
R03(config-if)#ip add 192.168.1.129 255.255.255.252
R03(config-if)#do sh
R03(config-if)#exit
R03(config)#do wr

! Rutas estáticas
R03(config)#ip route 192.168.1.0 255.255.255.192 10.0.0.1
R03(config)#ip route 192.168.1.64 255.255.255.192 10.0.0.1

R03(config-if)exit
R03#write
```

---

### PC0
```bash
IP: 192.168.1.3
Mask: 255.255.255.192
Gateway: 192.168.1.1
```

### PC1
```bash
IP: 192.168.1.2
Mask: 255.255.255.192
Gateway: 192.168.1.1
```

### PC2
```bash
IP: 192.168.1.66
Mask: 255.255.255.192
Gateway: 192.168.1.65
```

### PC3
```bash
IP: 192.168.1.67
Mask: 255.255.255.192
Gateway: 192.168.1.65
```

### PC4
```bash
IP: 192.168.2.2
Mask: 255.255.255.0
Gateway: 192.168.2.1
```

---

### Comandos de verificación

```bash
show ip interface brief
show ip route
```