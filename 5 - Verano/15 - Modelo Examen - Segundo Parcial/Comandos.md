! ================================
! CONFIGURACIÓN BÁSICA DEL ROUTER
! ================================

Router>enable
! Entra al modo privilegiado para administración del router

Router#configure terminal
! Entra al modo de configuración global

Router(config)#hostname R01
! Asigna el nombre R01 al router para su identificación

R01(config)#no ip domain-lookup
! Desactiva la resolución DNS para evitar retrasos por comandos mal escritos

R01(config)#enable secret RCenable
! Configura la contraseña del modo privilegiado usando cifrado seguro

R01(config)#service password-encryption
! Cifra todas las contraseñas visibles en la configuración

R01(config)#banner motd "ESTE DISPOSITO PERTENECE A LA UAGRM"
! Muestra un mensaje legal de advertencia al iniciar sesión

! ================================
! CONFIGURACIÓN DE INTERFAZ LAN
! ================================

R01(config)#interface gigabitEthernet 0/0/0
! Entra a la configuración de la interfaz hacia la LAN

R01(config-if)#description LAN-INTERNA
! Describe la función de la interfaz

R01(config-if)#ip address 192.168.1.1 255.255.255.0
! Asigna la IP 192.168.1.1/24 como gateway de la red LAN

R01(config-if)#no shutdown
! Activa la interfaz

! ================================
! SEGURIDAD DE ACCESO POR CONSOLA
! ================================

R01(config)#line console 0
! Accede a la configuración de la consola

R01(config-line)#logging synchronous
! Evita interrupciones por mensajes del sistema

R01(config-line)#exec-timeout 5 0
! Cierra la sesión tras 5 minutos de inactividad

R01(config-line)#login local
! Obliga a autenticarse usando usuarios locales

! ================================
! CREACIÓN DE USUARIO LOCAL
! ================================

R01(config)#username admin privilege 15 secret RCadmin
! Crea el usuario admin con máximo privilegio y contraseña cifrada

! ================================
! CONFIGURACIÓN Y SEGURIDAD SSH
! ================================

R01(config)#ip domain-name redes2.com
! Define el dominio necesario para habilitar SSH

R01(config)#crypto key generate rsa
! Genera claves RSA para SSH (usar tamaño recomendado 2048)

R01(config)#ip ssh time-out 60
! Define el tiempo máximo para autenticación SSH

R01(config)#ip ssh authentication-retries 3
! Limita los intentos de autenticación SSH a 3

R01(config)#line vty 0 15
! Accede a la configuración de acceso remoto (VTY)

R01(config-line)#transport input ssh
! Permite solo conexiones SSH (bloquea Telnet)

R01(config-line)#login local
! Autenticación usando usuarios locales

R01(config-line)#exec-timeout 5 0
! Cierra la sesión SSH tras 5 minutos de inactividad

! ================================
! GUARDAR CONFIGURACIÓN
! ================================

R01#write
! Guarda la configuración en la memoria permanente

! ================================
! CONEXIÓN DESDE UNA PC
! ================================

C:\>ssh -l admin 192.168.1.1
! Conexión remota segura al router mediante SSH
