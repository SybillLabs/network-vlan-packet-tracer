<h1 align="center">
    🌐 VLAN et affectation des ports
</h1>

## `> quickstart`
L'**objectif** est d'assurer le routage entre les différents VLAN tout en respectant le plan d'adressage VLSM et vérifier la communication entre les VLANs.

## `> config_RTR-INTERNE`
### Activation de l'interface physique
```
enable
configure terminal
interface gigabitEthernet 0/1
    no shutdown
    end
write
```

### Création des sous-interfaces pour chaque VLAN
```
# Sous-interface pour le VLAN 10 (PROD)
interface gigabitEthernet 0/1.10
    encapsulation dot1Q 10
    ip address 172.16.10.126 255.255.255.128
    exit

# Sous-interface pour le VLAN 20 (GESTION)
interface gigabitEthernet 0/1.20
    encapsulation dot1Q 20
    ip address 172.16.10.190 255.255.255.192
    exit

# Sous-interface pour le VLAN 30 (DIRECTION)
interface gigabitEthernet 0/1.30
    encapsulation dot1Q 30
    ip address 172.16.10.206 255.255.255.240
    exit

# Sous-interface pour le VLAN 99 (ADMIN)
interface gigabitEthernet 0/1.99
    encapsulation dot1Q 99
    ip address 172.16.10.222 255.255.255.240
    end
write
```

### Vérification de la table de routage
```
show ip route
```

## `> verification`
- PC1-PROD du VLAN10 avec ip statique `172.16.10.1/25` et gateway `172.16.10.126`
- PC2-GESTION du VLAN20 avec ip statique `172.16.10.130/26` et gateway `172.16.10.190`

### Comportement observé du ping
- Le premier ping ne passe pas car il construit sa route
- Les autres ping fonctionnent
- La communication inter-VLAN est **opérationnelle**

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>