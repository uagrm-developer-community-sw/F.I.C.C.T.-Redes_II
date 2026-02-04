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
* Los puertos access solo pertenecen a UNA VLAN

---

Configurar el puerto TRUNK hacia el router
```bash
interface gigabitEthernet 0/2
 switchport mode trunk
 switchport trunk allowed vlan 10,20
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