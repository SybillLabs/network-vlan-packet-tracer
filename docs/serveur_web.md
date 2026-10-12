<h1 align="center">
    🔐 Contrôle d'accès au serveur Web
</h1>

## `> quickstart`
L'**objectif** est de faire respecté les règles de politiques sur l'accès HTTP/HTTPS du serveur web.

## `> sercurity_rules`
- VLAN 10 : Accès HTTP/HTTPS du serveur web refusée
- VLAN 20 : Accès HTTP/HTTPS du serveur web refusée
- VLAN 30 : Accès HTTP/HTTPS du serveur web autorisée
- VLAN 99 : Accès HTTP/HTTPS du serveur web autorisée

## `> configuration_RTR-INTERNE`
### Création des ACLs
```
enable
configure terminal
# Blocage HTTP/HTTPS pour le VLAN 10 (PROD) vers le SRV-WEB
access-list 102 deny tcp 172.16.10.0 0.0.0.127 host 192.168.200.1 eq 80
access-list 102 deny tcp 172.16.10.0 0.0.0.127 host 192.168.200.1 eq 443
# Blocage HTTP/HTTPS pour le VLAN 20 (GESTION) vers le SRV-WEB
access-list 102 deny tcp 172.16.10.128 0.0.0.63 host 192.168.200.1 eq 80
access-list 102 deny tcp 172.16.10.128 0.0.0.63 host 192.168.200.1 eq 443
access-list 102 permit ip any any
end
write
```

### Application de l'ACL sur l'interface de la salle des serveurs
```
config terminal
interface gigabitEthernet 0/0
    ip access-group 102 out
    end
write
```

## `> validation`
### VLAN 10 & 20
![alt text](/screenshots/image-12.png)

### VLAN 30 & 99
![alt text](/screenshots/image-13.png)

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>