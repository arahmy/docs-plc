
## Doc 4

```markdown
# Mission 2 - Mise en place de l'infrastructure réseau

**Compte rendu rédigé par :** MANCEAU Léandre, RAHMY Arthur, BIDANESSY Coumba  
**Formation :** BTS SIO 1ère année - Option SISR  
**Établissement :** Lycée Paul-Louis Courier, Tours

## Sommaire

- 1. Schéma physique
- 2. Choix des VLANS dans les switchs
- 3. Liaisons trunk entre le commutateur central des salles et le routeur
- 4. Routage statique sur le routeur qui relie le modem ADSL
- 5. Translation d'adresse mis en place sur le routeur qui relie le modem ADSL
- Route statique sur le routeur reliée à la passerelle du lycée pour l'accès Internet
- 6. Captures d'écran Switch / Routeur

## 1. Schéma physique

## 2. Choix des VLANS dans les switchs

Tout d'abord j'ai attribuer pour chaque vlan de chaque salle un ID de VLAN avec l'attribution de chaque port selon leur vlan adaptée.

```text
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#vlan 20
Switch(config-vlan)#name Autres
Switch(config-vlan)#exit
Switch(config)#exit
Switch#
%SYS-5-CONFIG_I: Configured from console by console
Switch#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#interface FastEthernet0/1
Switch(config-if)#switchport access vlan 20
Switch(config-if)#exit
Switch(config)#exit
Switch#
%SYS-5-CONFIG_I: Configured from console by console
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#int g0/1
Switch(config-if)#switchport mode trunk
Switch(config-if)#end
Switch#
%SYS-5-CONFIG_I: Configured from console by console

access-list 1 permit 172.40.0.0 0.0.0.255
access-list 1 permit 172.40.1.0 0.0.0.127
access-list 1 permit 172.40.1.128 0.0.0.63
access-list 1 permit 172.40.2.0 0.0.0.63
access-list 1 permit 172.40.2.64 0.0.0.63

interface GigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 172.40.1.254 255.255.255.128
ip nat inside

interface GigabitEthernet0/0.20
encapsulation dot1Q 20

ip address 172.40.1.126 255.255.255.128
ip nat inside

interface GigabitEthernet0/0.30
encapsulation dot1Q 30
ip address 172.40.0.254 255.255.255.0
ip nat inside

interface GigabitEthernet0/0.40
encapsulation dot1Q 40
ip address 172.40.2.126 255.255.255.192
ip nat inside

interface GigabitEthernet0/0.50
encapsulation dot1Q 50
ip address 172.40.2.62 255.255.255.192
ip nat inside

ip nat inside source list 1 interface g0/1 overload
