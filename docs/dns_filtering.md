<h1 align="center">
    🌐 Test de filtrage DNS
</h1>

## `> quickstart`
L'**objectif** est d'interdire la résolution DNS aux postes du VLAN DIRECTION pour une opération de test.

## `> configuration_RTR-INTERNE`
### Création des ACLs
```
configure terminal
# Blocage du trafic DNS (port 53 en UDP) venant du VLAN 30 vers n'importe quel 
serveur DNS
access-list 103 deny udp 172.16.10.192 0.0.0.15 any eq 53
# Autorisation de tout le reste du trafic pour la DIRECTION
access-list 103 permit ip any any
end
write
```

### Application des ACLs
```
configure terminal
interface gigabitEthernet 0/1.30
    ip access-group 103 in
    end
write
```

## `> validation`
### Résolution avec www.ais.fr
![alt text](/screenshots/image-14.png)

### Résolution avec 192.168.200.1
![alt text](/screenshots/image-15.png)

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>