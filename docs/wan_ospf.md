<h1 align="center">
    🌐 Liaison WAN et routage OSPF
</h1>

## `> quickstart`
L'**objectif** est de configurer une liaison WAN et mettre en oeuvre `OSPF` afin que les réseaux nécessaires soient automatiquement connus des routeurs.

## `> configuration_WAN`
```
enable
configure terminal
    interface serial 0/3/0
        ip address 1.10.20.X 255.255.255.252      # 1.10.20.1 pour RTR-INTERNE et 1.10.20.2 pour RTR-EXTERNE
        no shutdown
        end
write
```

## `> validation_WAN`
> Faire un ping depuis les deux routeurs pour vérifier la connexion avec un résultat à 100%.

## `> configuration_OSPF`
> Ce protocole sera en processus 1 (numéro d'identification) et en zone 0 (zone géographique pour
éviter l'épuisement et le plantage).

| **Réseau / Usage** | **CIDR** | **Masque de sous-réseau** | **Masque inversé (Wildcard)** |
| :--- | :--- | :--- | :--- |
| **VLAN 10** (PROD) | `/25` | `255.255.255.128` | `0.0.0.127` |
| **VLAN 20** (GESTION) | `/26` | `255.255.255.192` | `0.0.0.63` |
| **VLAN 30** (DIRECTION) | `/28` | `255.255.255.240` | `0.0.0.15` |
| **VLAN 99** (ADMIN) | `/28` | `255.255.255.240` | `0.0.0.15` |
| **Liaison WAN** (Série) | `/30` | `255.255.255.252` | `0.0.0.3` |
| **Salle Serveurs** / **PC-NOMADE** | `/24` | `255.255.255.0` | `0.0.0.255` |

### Configuration sur `RTR-INTERNE` 
```
router ospf 1
    network 1.10.20.0 0.0.0.3 area 0
    network 192.168.200.0 0.0.0.255 area 0
    network 172.16.10.0 0.0.0.127 area 0
    network 172.16.10.128 0.0.0.63 area 0
    network 172.16.10.192 0.0.0.15 area 0
    network 172.16.10.208 0.0.0.15 area 0
    end
write
```

### Configuration sur `RTR-EXTERNE`
```
router ospf 1
    network 1.10.20.0 0.0.0.3 area 0
    network 192.168.1.0 0.0.0.255 area 0
    end
write
```

## `> validation_OSPF`

### `show ip ospf neighbor` : Affichage du **NeighBor ID** du routeur avec l'état
![alt text](/screenshots/image-2.png)

### `show ip route` : Affichage de la table de routage du routeur
![alt text](/screenshots/image-1.png)

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>