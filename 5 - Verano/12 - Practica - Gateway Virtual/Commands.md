## 🔹 I. CONFIGURACIÓN EN EL SWITCH (SW01) IZQUIERDO.

Entrar al modo configuración
```bash
enable
configure terminal
```

Creaer Vlan:
```bash
vlan 10
 name VLAN10
exit

vlan 20
 name VLAN20
exit

vlan 30
 name VLAN30
exit
```

Asignar puertos a VLAN 10 (PCs)
```bash
interface range fastEthernet 0/1 - 5
 switchport mode access
 switchport access vlan 10
exit
```

Asignar puertos a VLAN 20 (PCs)
```bash
interface range fastEthernet 0/6 - 10
 switchport mode access
 switchport access vlan 20
exit
```

Asignar puertos a VLAN 30 (PCs)
```bash
interface range fastEthernet 0/11 - 15
 switchport mode access
 switchport access vlan 30
exit
```
* Los puertos access solo pertenecen a UNA VLAN

---


Configurar el puerto TRUNK hacia el router
```bash
interface gigabitEthernet 0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 no shutdown
exit
```
* El trunk permite que varias VLAN viajen por un solo cable.

Guardar configuración del switch
```bash
end
write
```

## 🔹 II. CONFIGURACIÓN EN EL ROUTER (Router-on-a-Stick)

Entrar al router
```bash
enable
configure terminal
```

SWML-01#
SWML-01#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
SWML-01(config)#int
SWML-01(config)#interface vlan 10
SWML-01(config-if)#
%LINK-5-CHANGED: Interface Vlan10, changed state to up

SWML-01(config-if)#ip a
SWML-01(config-if)#ip add
SWML-01(config-if)#ip address 192.168.10.1 255.255.255.0
SWML-01(config-if)#exit
SWML-01(config)#int
SWML-01(config)#interface vlan 20
SWML-01(config-if)#
%LINK-5-CHANGED: Interface Vlan20, changed state to up

SWML-01(config-if)#ip add
SWML-01(config-if)#ip address 192.168.20.1 255.255.255.0
SWML-01(config-if)#exit
SWML-01(config)#int vlan 30
SWML-01(config-if)#
%LINK-5-CHANGED: Interface Vlan30, changed state to up

SWML-01(config-if)#ip add 192.168.30.1 255.255.255.0
SWML-01(config-if)#end
SWML-01#

Configurar el puerto TRUNK hacia el switch

SWML-01(config)#int g1/0/1
SWML-01(config-if)#sw mode trunk
SWML-01(config-if)#

SWML-01(config)# ip routing








Creaer Vlan:
```bash
vlan 40
 name VLAN40
exit

vlan 50
 name VLAN50
exit

vlan 60
 name VLAN60
exit
```

Asignar puertos a VLAN 40 (PCs)
```bash
interface range fastEthernet 0/1 - 5
 switchport mode access
 switchport access vlan 40
exit
```

Asignar puertos a VLAN 50 (PCs)
```bash
interface range fastEthernet 0/6 - 10
 switchport mode access
 switchport access vlan 50
exit
```

Asignar puertos a VLAN 60 (PCs)
```bash
interface range fastEthernet 0/11 - 15
 switchport mode access
 switchport access vlan 60
exit
```

Configurar el puerto TRUNK hacia el router
```bash
interface gigabitEthernet 0/1
 switchport mode trunk
 switchport trunk allowed vlan 40,50,60
 no shutdown
exit    
```



SWML-01#
SWML-01#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
SWML-01(config)#int
SWML-01(config)#interface vlan 40
SWML-01(config-if)#
%LINK-5-CHANGED: Interface Vlan10, changed state to up

SWML-01(config-if)#ip a
SWML-01(config-if)#ip add
SWML-01(config-if)#ip address 192.168.40.1 255.255.255.0
SWML-01(config-if)#exit
SWML-01(config)#int
SWML-01(config)#interface vlan 50
SWML-01(config-if)#
%LINK-5-CHANGED: Interface Vlan20, changed state to up

SWML-01(config-if)#ip add
SWML-01(config-if)#ip address 192.168.50.1 255.255.255.0
SWML-01(config-if)#exit
SWML-01(config)#int vlan 60
SWML-01(config-if)#
%LINK-5-CHANGED: Interface Vlan30, changed state to up

SWML-01(config-if)#ip add 192.168.60.1 255.255.255.0
SWML-01(config-if)#end
SWML-01#

Configurar el puerto TRUNK hacia el switch

SWML-01(config)#int g1/0/1
SWML-01(config-if)#sw mode trunk
SWML-01(config-if)#

SWML-01(config)# ip routing




✅ SOLUCIÓN MÁS SIMPLE (EXAMEN / LAB): RUTAS ESTÁTICAS

🔹 1️⃣ En SWML-01

(decirle cómo llegar a VLAN 40–50–60)


SWML-01# conf t
ip route 192.168.40.0 255.255.255.0 10.0.0.2
ip route 192.168.50.0 255.255.255.0 10.0.0.2
ip route 192.168.60.0 255.255.255.0 10.0.0.2
end


🔹 2️⃣ En SWML-02

(decirle cómo llegar a VLAN 10–20–30)

SWML-02# conf t
ip route 192.168.10.0 255.255.255.0 10.0.0.1
ip route 192.168.20.0 255.255.255.0 10.0.0.1
ip route 192.168.30.0 255.255.255.0 10.0.0.1
end





Creaer Vlan:
```bash
vlan 70
 name VLAN70
exit

vlan 80
 name VLAN80
exit

vlan 90
 name VLAN90
exit
```

Asignar puertos a VLAN 70 (PCs)
```bash
interface range fastEthernet 0/1 - 5
 switchport mode access
 switchport access vlan 70
exit
```

Asignar puertos a VLAN 80 (PCs)
```bash
interface range fastEthernet 0/6 - 10
 switchport mode access
 switchport access vlan 80
exit
```

Asignar puertos a VLAN 90 (PCs)
```bash
interface range fastEthernet 0/11 - 15
 switchport mode access
 switchport access vlan 90
exit

Configurar el puerto TRUNK hacia el router
```bash
interface gigabitEthernet 0/1
 switchport mode trunk
 switchport trunk allowed vlan 70,80,90
 no shutdown
exit    
```
* El trunk permite que varias VLAN viajen por un solo cable.

Guardar configuración del switch
```bash
end
write
```

## 🔹 II. CONFIGURACIÓN EN EL ROUTER (Router-on-a-Stick)

Activar la interfaz física (OBLIGATORIO)
```bash
interface gigabitEthernet 1/0/3
 no shutdown
exit
```

* Sin esto, el trunk nunca levanta.

Subinterfaz para VLAN 70
```bash
interface gigabitEthernet 0/0/0.70
 encapsulation dot1Q 70
 ip address 192.168.70.1 255.255.255.0
exit

```
* dot1Q 10 → identifica la VLAN
* 192.168.10.1 → será el gateway de VLAN 10

Subinterfaz para VLAN 80
```bash
interface gigabitEthernet 0/0/0.80
 encapsulation dot1Q 80
 ip address 192.168.80.1 255.255.255.0
exit
```
* Gateway de VLAN 80

Subinterfaz para VLAN 90
```bash
interface gigabitEthernet 0/0/0.90
 encapsulation dot1Q 90
 ip address 192.168.90.1 255.255.255.0
exit
```
* Gateway de VLAN 90


SWML-01(config)#int g1/0/3
SWML-01(config-if)#sw mode trunk
SWML-01(config-if)#

---
























































Activar la interfaz física (OBLIGATORIO)
```bash
interface gigabitEthernet 0/0/0
 no shutdown
exit
```
* Sin esto, el trunk nunca levanta.

Subinterfaz para VLAN 10
```bash
interface gigabitEthernet 0/0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
exit

```
* dot1Q 10 → identifica la VLAN
* 192.168.10.1 → será el gateway de VLAN 10

Subinterfaz para VLAN 20
```bash
interface gigabitEthernet 0/0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
exit
```
* Gateway de VLAN 20

---

##🔹 I. CONFIGURACIÓN EN EL SWITCH (SW01) DERECHO

Entrar al modo configuración
```bash
enable
configure terminal
```

Creaer Vlan:
```bash
vlan 30
 name VLAN0010
exit

vlan 40
 name VLAN20
exit

Asignar puertos a VLAN 30 (PCs)
```bash
interface range fastEthernet 0/1 - 5
 switchport mode access
 switchport access vlan 30
exit
```

Asignar puertos a VLAN 40 (PCs)
```bash
interface range fastEthernet 0/6 - 10
 switchport mode access
 switchport access vlan 40
exit
* Los puertos access solo pertenecen a UNA VLAN

---

Configurar el puerto TRUNK hacia el router
```bash
interface gigabitEthernet 0/1
 switchport mode trunk
 switchport trunk allowed vlan 30,40
 no shutdown
exit
```
* El trunk permite que varias VLAN viajen por un solo cable.

Guardar configuración del switch
```bash
end
write
```

## 🔹 II. CONFIGURACIÓN EN EL ROUTER (Router-on-a-Stick)
Entrar al router
```bash
enable
configure terminal
```

Activar la interfaz física (OBLIGATORIO)
```bash
interface gigabitEthernet 0/0/0
 no shutdown
exit
```
* Sin esto, el trunk nunca levanta.

Subinterfaz para VLAN 30
```bash
interface gigabitEthernet 0/0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0
exit

```
* dot1Q 30 → identifica la VLAN
* 192.168.30.1 → será el gateway de VLAN 30

Subinterfaz para VLAN 40
```bash
interface gigabitEthernet 0/0/0.40
 encapsulation dot1Q 40
 ip address 192.168.40.1 255.255.255.0
exit
```
* Gateway de VLAN 40


---

## 🔹 III. COMANDOS DE VERIFICACIÓN
En el SWITCH
```bash
show vlan brief
show ip interface brief
show interfaces trunk
```

En el ROUTER
```bash
show ip interface brief
show running-config | section interface GigabitEthernet0/0/0
```

---

## 🌐 REDES INVOLUCRADAS
🔹 Lado R1

* VLAN 10 → 192.168.10.0/24
* VLAN 20 → 192.168.20.0/24

🔹 Enlace serial

* R1 → 10.0.0.1/30
* R2 → 10.0.0.2/30

🔹 Lado R2

* VLAN 30 → 192.168.30.0/24
* VLAN 40 → 192.168.40.0/24

### SOLUCIÓN RECOMENDADA (EXAMEN): RUTAS ESTÁTICAS
🔹 CONFIGURACIÓN EN R1 (hacia R2)

Entra a R1
```bash
enable
configure terminal
```

Rutas hacia las VLAN del lado derecho
```bash
ip route 192.168.30.0 255.255.255.0 10.0.0.2
ip route 192.168.40.0 255.255.255.0 10.0.0.2
```

> Le dices a R1:
>“Para llegar a las redes 30 y 40, ve por R2 (10.0.0.2)”

Guardar
```bash
end
write
```

CONFIGURACIÓN EN R2 (hacia R1)

Entra a R2
```bash
enable
configure terminal
```

Rutas hacia las VLAN del lado izquierdo
```bash
ip route 192.168.10.0 255.255.255.0 10.0.0.1
ip route 192.168.20.0 255.255.255.0 10.0.0.1
```
* Le dices a R2:
* “Para llegar a las redes 10 y 20, ve por R1 (10.0.0.1)”

Guardar
```bash
end
write
```
VERIFICACIÓN EN LOS ROUTERS
```bash
show ip route
```