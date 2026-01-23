## LAN-IZQ
```bash

192.168.0.64 /29
255.255.255.248

# CONFS:
LAN-IZQ>en
LAN-IZQ#conf t
LAN-IZQ(config)#host LAN-IZQ

# LANS:
LAN-IZQ(config)#int g0/0/0
LAN-IZQ(config-if)#ip add 192.168.0.65 255.255.255.248
LAN-IZQ(config-if)#do sh
LAN-IZQ(config-if)#exit
LAN-IZQ(config)#do wr

LAN-IZQ(config)#int g0/0/1
LAN-IZQ(config-if)#ip add 192.168.0.66 255.255.255.248
LAN-IZQ(config-if)#do sh
LAN-IZQ(config-if)#exit
LAN-IZQ(config)#do wr

# WANS:
LAN-IZQ(config)#int se0/1/0
LAN-IZQ(config-if)#ip add 192.168.0.1 255.255.255.252
LAN-IZQ(config-if)#no sh
LAN-IZQ(config-if)#exit
LAN-IZQ(config)#do wr

LAN-IZQ(config)#int se0/1/1
LAN-IZQ(config-if)#ip add 192.168.0.9 255.255.255.252
LAN-IZQ(config-if)#no sh
LAN-IZQ(config-if)#exit
LAN-IZQ(config)#do wr

LAN-IZQ(config)#int se0/2/0
LAN-IZQ(config-if)#ip add 192.168.0.00 255.255.255.252
LAN-IZQ(config-if)#no sh
LAN-IZQ(config-if)#exit
LAN-IZQ(config)#do write



# Rutas estáticas
LAN-IZQ(config)ip route 192.168.1.64 255.255.255.192 192.168.1.130
LAN-IZQ(config)ip route 192.168.2.0 255.255.255.0 192.168.1.130

LAN-IZQ(config)#exit
LAN-IZQ#write
```

---

## LAN-DER
```bash

192.168.0.72 /29
255.255.255.248

# CONFS:
LAN-DER>en
LAN-DER#conf t
LAN-DER(config)#host LAN-DER

# LANS:
LAN-DER(config)#int g0/0/0
LAN-DER(config-if)#ip add 192.168.0.74 255.255.255.248
LAN-DER(config-if)#do sh
LAN-DER(config-if)#exit
LAN-DER(config)#do wr

LAN-DER(config)#int g0/0/1
LAN-DER(config-if)#ip add 192.168.0.78 255.255.255.248
LAN-DER(config-if)#do sh
LAN-DER(config-if)#exit
LAN-DER(config)#do wr

# WANS:
LAN-DER(config)#int se0/1/1
LAN-DER(config-if)#ip add 192.168.0.6 255.255.255.252
LAN-DER(config-if)#do sh
LAN-DER(config-if)#exit
LAN-DER(config)#do wr

LAN-DER(config)#int se0/1/0
LAN-DER(config-if)#ip add 192.168.0.66 255.255.255.248
LAN-DER(config-if)#do sh
LAN-DER(config-if)#exit
LAN-DER(config)#do wr

LAN-DER(config)#int se0/2/0
LAN-DER(config-if)#ip add 192.168.0.66 255.255.255.248
LAN-DER(config-if)#do sh
LAN-DER(config-if)#exit
LAN-DER(config)#do write

# Rutas estáticas
LAN-DER(config)ip route 192.168.1.64 255.255.255.192 192.168.1.130
LAN-DER(config)ip route 192.168.2.0 255.255.255.0 192.168.1.130

LAN-DER(config)#exit
LAN-DER#write
```
---

### WAN1
```bash
WAN1(config)#int se0/1/0
WAN1(config-if)#ip add 192.168.0.2 255.255.255.252
WAN1(config-if)#no sh
WAN1(config-if)#exit
WAN1(config)#do wr

WAN1(config)#int se0/1/1
WAN1(config-if)#ip add 192.168.0.5 255.255.255.252
WAN1(config-if)#no sh
WAN1(config-if)#exit
WAN1(config)#do wr

WAN1(config)#int se0/2/0
WAN1(config-if)#ip add 192.168.0.18 255.255.255.252
WAN1(config-if)#no sh
WAN1(config-if)#exit
WAN1(config)#do wr

```

### WAN2
```bash
WAN2(config)#int se0/1/1
WAN2(config-if)#ip add 192.168.0.10 255.255.255.252
WAN2(config-if)#no sh
WAN2(config-if)#exit
WAN2(config)#do wr

WAN2(config)#int se0/1/1
WAN2(config-if)#ip add 192.168.0.5 255.255.255.252
WAN2(config-if)#no sh
WAN2(config-if)#exit
WAN2(config)#do wr

WAN2(config)#int se0/1/0
WAN2(config-if)#ip add 192.168.0.2 255.255.255.252
WAN2(config-if)#no sh
WAN2(config-if)#exit
WAN2(config)#do wr

WAN2(config)#int se
WAN2(config-if)#ip add 192.168.0.5 255.255.255.252
WAN2(config-if)#no sh
WAN2(config-if)#exit
WAN2(config)#do wr
```
### WAN3
```bash
Red: 192.168.0.8/30
Router A: 192.168.0.9
Router B: 192.168.0.10

```

### WAN4
```bash
Red: 192.168.0.12/30
Router A: 192.168.0.13
Router B: 192.168.0.14

```

### WAN5
```bash
Red: 192.168.0.16/30
Router A: 192.168.0.17
Router B: 192.168.0.18

```

### WAN6
```bash
Red: 192.168.0.20/30
Router A: 192.168.0.21
Router B: 192.168.0.22

```

### WAN7
```bash
Red: 192.168.0.24/30
Router A: 192.168.0.25
Router B: 192.168.0.26

```

### WAN8
```bash
Red: 192.168.0.28/30
Router A: 192.168.0.29
Router B: 192.168.0.30

```

### WAN9
```bash
Red: 192.168.0.32/30
Router A: 192.168.0.33
Router B: 192.168.0.34

```

### WAN10
```bash
Red: 192.168.0.36/30
Router A: 192.168.0.37
Router B: 192.168.0.38

```

---

LAN-IZQ:
ip route 192.168.0.20 255.255.255.252 192.168.0.10  (LAN-IZQ)
ip route 192.168.0.44 255.255.255.252 192.168.0.22  (WAN2)
ip route 192.168.0.64 255.255.255.252 192.168.0.46  (WAN5)

ip route 192.168.0.88 255.255.255.248 192.168.0.66  (WAN8)
ip route 192.168.0.96 255.255.255.248 192.168.0.66  (WAN8)

LAN-DER:
ip route 192.168.0.44 255.255.255.252 192.168.0.65  (LAN-DER)
ip route 192.168.0.20 255.255.255.252 192.168.0.45  (WAN8)
ip route 192.168.0.8 255.255.255.252 192.168.0.21   (WAN5)

ip route 192.168.0.72 255.255.255.248 192.168.0.9   (WAN2)
ip route 192.168.0.80 255.255.255.248 192.168.0.9   (WAN2)