<h1 align="center">
    🌐 VLAN et affectation des ports
</h1>

## `> quickstart`
L'**objectif** est de segmenter le réseau par VLAN, affecter les ports utilisateurs en mode access et configurer les liaisons trunk pour le transport inter-VLAN et le routage vers `RTR-INTERNE`.

## `> VLANs`
> Les VLANs sont créés et nommés uniquement sur `SW-DISTRIB` (référence centrale), puis propagés vers `SW-E1` et `SW-E2` via le trunking. Les VLANs sont identiques sur tous les switches du domaine de broadcast :

| VLAN | Nom       | Ports utilisateurs (SW-E1/SW-E2) | Plage IP         |
| ---- | --------- | -------------------------------- | ---------------- |
| 10   | PROD      | Fa0/1-Fa0/7                      | 172.16.10.0/25   |
| 20   | GESTION   | Fa0/8-Fa0/13                     | 172.16.10.128/26 |
| 30   | DIRECTION | Fa0/14-Fa0/20                    | 172.16.10.192/28 |
| 99   | ADMIN     | Fa0/21-Fa0/23                    | 172.16.10.208/28 |

## `> VLAN_creation`
> Configuration appliqué sur les 3 switches.
```
configure terminal
vlan 10
    name PROD
vlan 20
    name GESTION
vlan 30
    name DIRECTION
vlan 99
    name ADMIN
end
write
```

## `> access_mode`
> Configuration appliqué sur `SW-E1` et `SW-E2`.
```
configure terminal
interface range Fa0/1 - 7
    switchport mode access
    switchport access vlan 10
    exit
interface range Fa0/8 - 13
    switchport mode access
    switchport access vlan 20
    exit
interface range Fa0/14 - 20
    switchport mode access
    switchport access vlan 30
    exit
interface range Fa0/21 - 23
    switchport mode access
    switchport access vlan 99
    end
write
```

## `> trunk_mode`
### Topologie
- Fa0/24 (`SW-E1`) ↔ Fa0/1 (`SW-DISTRIB`)
- Fa0/24 (`SW-E2`) ↔ Fa0/2 (`SW-DISTRIB`)
- `SW-DISTRIB` ↔ `RTR-INTERNE` : Gi0/1 (`SW-DISTRIB`)

### Sur `SW-E1` et `SW-E2`
```
interface Fa0/24
    switchport mode trunk
    switchport trunk allowed vlan 10,20,30,99
    end
write
```

### Sur `SW-DISTRIB`
```
interface range Fa0/1 - 2
    switchport mode trunk
    switchport trunk allowed vlan 10,20,30,99
    exit
interface Gi0/1
    switchport mode trunk
    switchport trunk allowed vlan 10,20,30,99
    end
write
```

## `verification`
```
show vlan brief             # Vérification des VLANs et ports associés          
show interfaces trunk       # État des trunks (VLANs autorisés)
show interfaces status      # État global des ports
```

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>