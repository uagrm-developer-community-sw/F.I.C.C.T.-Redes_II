# Tarea # 1

## Imagenes:
![Tarea # 1](https://github-production-user-asset-6210df.s3.amazonaws.com/36086876/479177699-0c813d58-3543-44af-82a0-ce8bde211310.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250818%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250818T184756Z&X-Amz-Expires=300&X-Amz-Signature=d9c2b6e8715dcfed2e4a288ae54c280a48b801059a67e6042656e1337f09ea33&X-Amz-SignedHeaders=host)

---

![Packetracer](https://github-production-user-asset-6210df.s3.amazonaws.com/36086876/479175740-f2e5f2e6-4426-4237-8548-a912a43c6b39.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250818%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250818T184414Z&X-Amz-Expires=300&X-Amz-Signature=523470841e16c563b7a45fa3c45ec7398cf5b2ec2dade5af94f4d8518b31b48c&X-Amz-SignedHeaders=host)

## Enunciado de la tarea:
```bash
Objetivo:

Crear 2 VLANs:

VLAN 888 → Mujeres (círculos en el diagrama).
VLAN 777 → Alumnos (cuadrados en el diagrama).

Asignar puertos:

Puertos Fa0/1 → Fa0/10 = Alumnos (VLAN 777).
Puertos Fa0/14 → Fa0/20 = Mujeres (VLAN 888).

Los enlaces troncales (líneas gruesas entre switches) deben permitir ambas VLANs.
```

## Paso para desarrollar:

### 1. Entrar en modo configuración.
```bash
enable
configure terminal
```

### 2. Crear las VLANs.
```bash
vlan 777
 name Alumnos
vlan 888
 name Mujeres
exit
```
Respuesta:
```bash
Switch#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
777  Alumnos                          active    
888  Mujeres                          active    
1002 fddi-default                     act/unsup 
1003 token-ring-default               act/unsup 
1004 fddinet-default                  act/unsup 
1005 trnet-default                    act/unsup 

```


### 3. Asignar los puertos a cada VLAN.
Para Alumnos (VLAN 777), puertos Fa0/1 hasta Fa0/10:
```bash
interface range fa0/1 - 10
 switchport mode access
 switchport access vlan 777
exit
```
Para Mujeres (VLAN 888), puertos Fa0/14 hasta Fa0/20:
```bash
interface range fa0/14 - 20
 switchport mode access
 switchport access vlan 888
exit
```

Respuesta:
```bash
Switch#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/11, Fa0/12, Fa0/13, Fa0/21
                                                Fa0/22, Fa0/23, Fa0/24
777  Alumnos                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10
888  Mujeres                          active    Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/18, Fa0/19, Fa0/20
1002 fddi-default                     act/unsup 
1003 token-ring-default               act/unsup 
1004 fddinet-default                  act/unsup 
1005 trnet-default                    act/unsup 
```

### 4. Configurar los enlaces troncales entre switches.
(Por ejemplo Fa0/21 y Fa0/22 que se usan para interconexión)
```bash
interface range fa0/21 - 22
 switchport mode trunk
 switchport trunk allowed vlan 777,888
exit
```

Respuesta:
```bash
Switch(config)#interface range fa0/21 - 22
Switch(config-if-range)#switchport mode trunk


Switch(config-if-range)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/21, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/21, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/22, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/22, changed state to up

Switch(config-if-range)#switchport trunk allowed vlan 777,888
Switch(config-if-range)#exit
Switch(config)#exit
Switch#
```