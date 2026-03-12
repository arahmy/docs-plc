# Mission 2 - Mise en place de l'infrastructure réseau

**Compte rendu rédigé par :** BIDANESSY Coumba  
**Formation :** BTS SIO 1ère année - Option SISR  
**Établissement :** Lycée Paul-Louis Courier, Tours  
**Date :** 15 janvier 2026

## Sommaire

- 1. Schéma physique
- 2. Choix des VLANS dans les switchs
- 3. Liaisons trunk entre le commutateur central des salles et le routeur
- 4. Routage statique sur le routeur qui relie le modem ADSL
- 5. Translation d'adresse mis en place sur le routeur qui relie le modem ADSL

## 1. Schéma physique

## 2. Choix des VLANS dans les switchs

Tout d'abord j'ai attribué pour chaque VLAN de chaque salle un ID de VLAN avec l'attribution de chaque port selon leur VLAN adaptée.

## 3. Liaisons trunk entre le commutateur central des salles et le routeur

- Activation du mode trunk sur le commutateur
- Exemple du mode trunk depuis le retour vers le sous réseaux en VLAN 50

## 4. Routage statique sur le routeur qui relie le modem ADSL

## 5. Translation d'adresse mis en place sur le routeur qui relie le modem ADSL

```text
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


## Doc 2

```markdown
# Mission 3 - Mise en place de l'infrastructure réseau avec VLAN visiteurs et dans le VLAN commerciaux

**Compte rendu rédigé par :** BIDANESSY Coumba, MANCEAU Léandre, RAHMY Arthur  
**Formation :** BTS SIO 1ère année - Option SISR  
**Établissement :** Lycée Paul-Louis Courier, Tours

## VLAN Visiteurs

### Calcul VLSM WiFi Visiteurs

```text
16 * 1,2 = 20 hôtes
2^x - 2 = 20 hôtes
Donc : 2^5 - 2 = 30
Et 32 - 5 = 27 bits
