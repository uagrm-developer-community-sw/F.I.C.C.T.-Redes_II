# Ejercicio 1 - Configuración de Red con Tres Routers

## Topología de Red

Esta configuración establece una red con tres routers interconectados:

- **R1**: Router de borde conectado a la red local 192.168.1.0/24
- **R2**: Router central que interconecta R1 y R3
- **R3**: Router de borde conectado a la red local 192.168.3.0/24

### Conexiones entre routers:
- R1 ↔ R2: Enlace serial 10.0.0.0/30 (R1: 10.0.0.1, R2: 10.0.0.2)
- R2 ↔ R3: Enlace serial 10.0.0.4/30 (R2: 10.0.0.5, R3: 10.0.0.6)

---

## Configuración Router R1

### Interfaces configuradas:
- **GigabitEthernet0/0/0**: Red LAN 192.168.1.0/24 (Gateway: 192.168.1.1)
- **Serial0/1/0**: Conexión WAN a R2 (IP: 10.0.0.1/30)

```bash
Router>en                                    # Entrar al modo privilegiado
Router#conf t                                # Entrar al modo de configuración global
Enter configuration commands, one per line.  End with CNTL/Z.

# Configurar interfaz LAN (GigabitEthernet)
Router(config)#int gig0/0/0                  # Acceder a la interfaz GigabitEthernet0/0/0
Router(config-if)#ip add 192.168.1.1 255.255.255.0   # Asignar IP de la red local
Router(config-if)#no sh                      # Activar la interfaz (no shutdown)

Router(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up

Router(config-if)#exit

# Configurar interfaz WAN Serial hacia R2
Router(config)#int se0/1/0                   # Acceder a la interfaz Serial0/1/0
Router(config-if)#ip add 10.0.0.1 255.255.255.252    # Asignar IP del enlace WAN
Router(config-if)#no sh                      # Activar la interfaz

%LINK-5-CHANGED: Interface Serial0/1/0, changed state to down    # Estado inicial down (esperando conexión de R2)
Router(config-if)#exit
Router(config)#
```

---

## Configuración Router R2

### Interfaces configuradas:
- **GigabitEthernet0/0/0**: Red LAN 192.168.2.0/24 (Gateway: 192.168.2.1)
- **Serial0/1/0**: Conexión WAN a R1 (IP: 10.0.0.2/30)
- **Serial0/1/1**: Conexión WAN a R3 (IP: 10.0.0.5/30)

```bash
Router>en                                    # Entrar al modo privilegiado
Router#conf t                                # Entrar al modo de configuración global
Enter configuration commands, one per line.  End with CNTL/Z.

# Configurar interfaz LAN (GigabitEthernet)
Router(config)#int g0/0/0                    # Acceder a la interfaz GigabitEthernet0/0/0
Router(config-if)#ip add 192.168.2.1 255.255.255.0   # Asignar IP de la red local
Router(config-if)#no sh                      # Activar la interfaz

Router(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up

Router(config-if)#exit

# Configurar interfaz WAN Serial hacia R1
Router(config)#int se0/1/0                   # Acceder a la interfaz Serial0/1/0
Router(config-if)#ip add 10.0.0.2 255.255.255.252    # Asignar IP del enlace WAN con R1
Router(config-if)#no sh                      # Activar la interfaz

Router(config-if)#
%LINK-5-CHANGED: Interface Serial0/1/0, changed state to up    # Enlace activo con R1

Router(config-if)#exit

# Configurar interfaz WAN Serial hacia R3
Router(config)#int se0/1/1                   # Acceder a la interfaz Serial0/1/1
Router(config-if)#ip add 10.0.0.5 255.255.255.252    # Asignar IP del enlace WAN con R3
Router(config-if)#no sh                      # Activar la interfaz

%LINK-5-CHANGED: Interface Serial0/1/1, changed state to down    # Estado inicial down (esperando conexión de R3)
Router(config-if)#exit
Router(config)#
Router#
```

---

## Configuración Router R3

### Interfaces configuradas:
- **GigabitEthernet0/0/0**: Red LAN 192.168.3.0/24 (Gateway: 192.168.3.1)
- **Serial0/1/0**: Conexión WAN a R2 (IP: 10.0.0.6/30)

```bash
Router>en                                    # Entrar al modo privilegiado
Router#conf t                                # Entrar al modo de configuración global
Enter configuration commands, one per line.  End with CNTL/Z.

Router(config)#host R3                       # Asignar nombre al router (opcional pero recomendado)

# Configurar interfaz LAN (GigabitEthernet)
R3(config)#int g0/0/0                        # Acceder a la interfaz GigabitEthernet0/0/0
R3(config-if)#ip add 192.168.3.1 255.255.255.0       # Asignar IP de la red local
R3(config-if)#no sh                          # Activar la interfaz

R3(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up

R3(config-if)#exit

# Configurar interfaz WAN Serial hacia R2
R3(config)#int se0/1/0                       # Acceder a la interfaz Serial0/1/0
R3(config-if)#ip add 10.0.0.6 255.255.255.252        # Asignar IP del enlace WAN con R2
R3(config-if)#no sh                          # Activar la interfaz

R3(config-if)#
%LINK-5-CHANGED: Interface Serial0/1/0, changed state to up    # Enlace activo con R2

R3(config-if)#exit
R3(config)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface Serial0/1/0, changed state to up
```

---

## Resumen de Comandos Cisco IOS

| Comando | Descripción |
|---------|-------------|
| `en` o `enable` | Accede al modo privilegiado (EXEC privilegiado) |
| `conf t` o `configure terminal` | Accede al modo de configuración global |
| `int <interfaz>` | Accede al modo de configuración de una interfaz específica |
| `ip add <IP> <máscara>` | Asigna una dirección IP y máscara de subred a la interfaz |
| `no sh` o `no shutdown` | Activa la interfaz (por defecto están deshabilitadas) |
| `host <nombre>` | Asigna un nombre al router |
| `exit` | Sale del modo actual y regresa al nivel anterior |

---

## Notas Importantes

1. **Máscara /30 en enlaces WAN**: Se utiliza la máscara 255.255.255.252 (/30) para enlaces punto a punto entre routers, ya que solo proporciona 2 direcciones IP utilizables.

2. **Estados de las interfaces seriales**: Una interfaz serial solo cambia a estado "up" cuando ambos extremos están configurados y conectados.

3. **Falta configuración de enrutamiento**: Esta configuración solo establece las direcciones IP. Para que las redes se comuniquen entre sí, es necesario configurar un protocolo de enrutamiento (RIP, OSPF, EIGRP) o rutas estáticas.

4. **Comando `no shutdown`**: Las interfaces de los routers Cisco están deshabilitadas por defecto. El comando `no sh` es necesario para activarlas.