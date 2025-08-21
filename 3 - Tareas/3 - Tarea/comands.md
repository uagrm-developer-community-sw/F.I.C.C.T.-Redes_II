enable
configure terminal
vlan 888
name Mujeres
exit

enable
configure terminal
vlan 777
name Alumunos
exit

show vlan

interface range f0/01-10
switchport mode access
switchport access vlan 888
exit

interface range f0/14-20
switchport mode access
switchport access vlan 777
exit