<h1 align="center">
    🔐 Isolation des VLANs PROD et Gestion
</h1>

## `> quickstart`
L'**objectif** est d'isoler les postes des VLANs PROD et GESTION et qu'ils ne doivent pas pouvoir communiquer entre eux. Les autres connexions nécessaires ne seront pas perturbées.

## `> configuration_RTR-INTERNE`
### Création des ACLs étendues
```
configure terminal
# ACL pour le trafic entrant depuis le VLAN 10
access-list 101 deny ip 172.16.10.0 0.0.0.127 172.16.10.128 0.0.0.63
# ACL pour le trafic entrant depuis le VLAN 20
access-list 101 deny ip 172.16.10.128 0.0.0.63 172.16.10.0 0.0.0.127
access-list 101 permit ip any any
end
write
```

### Création des ACLS pour chaque sous-interface
```
# Application du filtre sur la sous-interface du VLAN 10
interface gigabitEthernet 0/1.10
    ip access-group 101 in
    exit
# Application du filtre sur la sous-interface du VLAN 20
interface gigabitEthernet 0/1.20
    ip access-group 101 in
    end
write
```

## `> validation`
![alt text](/screenshots/image-11.png)

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>