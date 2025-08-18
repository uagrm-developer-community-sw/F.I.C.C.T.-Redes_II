## Comandos en los Switches.

📌 Resumen rápido de comandos:

vlan [id] → crear VLAN

name [nombre] → asignar nombre

switchport mode access → poner el puerto en acceso

switchport access vlan [id] → asignar puerto a VLAN

switchport mode trunk → configurar trunk

show vlan brief → ver VLANs activas

### 1. Entrar al switch.
```bash
enable
configure terminal
```

### 2. Crear VLANs.
Ejemplo con VLAN 10 y 20:

```bash
vlan 10
name Ventas
exit

vlan 20
name Contabilidad
exit

```

### 3. Asignar puertos a VLANs.
Ejemplo: puertos FastEthernet 0/1 y 0/2 → VLAN 10, y 0/3 → VLAN 20
```bash
interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
exit

interface fastEthernet 0/2
switchport mode access
switchport access vlan 10
exit

interface fastEthernet 0/3
switchport mode access
switchport access vlan 20
exit

```

### 4. Configurar un puerto trunk (para conectar switches o router-on-a-stick).
Ejemplo en FastEthernet 0/24:
```bash
interface fastEthernet 0/24
switchport mode trunk
switchport trunk allowed vlan all
exit

```

### 5. Verificar configuración.
```bash
show vlan brief
show running-config

```

### 6. (Opcional) Router-on-a-Stick – configurar subinterfaces en el router.
(Esto permite comunicación entre VLANs).

```bash
interface fastEthernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit

interface fastEthernet 0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit

```