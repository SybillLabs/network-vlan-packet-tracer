<h1 align="center">
    🌐 Administration distante sécurisée
</h1>

## `> quickstart`
L'**objectif** est de pouvoir administrer à distance de façon sécurisée depuis un ordinateur nomade via une connexion SSH.

## `> configuration_RTR`
### Prérequis pour le SSH
```
configure terminal
ip domain-name ais.fr
    crypto key generate rsa
    # à la question choisir 1024 ou 2048, pour une meilleur sécurité et performance (plus grand plus difficile à casser) et être conforme avec CISCO.
    username admin privilege 15 secret SuperMotDePasse
    end
write
```

### Création des ACL de restriction
```
configure terminal
access-list 10 permit 172.16.10.208 0.0.0.15
access-list 10 permit host 192.168.1.1
end
write
```

### Application de l'ACL sur les lignes virtuelles et interdiction de Telnet
```
line vty 0 4
transport input ssh
access-class 10 in
login local
end
write
```

## `> validation`
### Accès autorisé
![alt text](/screenshots/image-8.png)

### Accès refusé
![alt text](/screenshots/image-9.png)

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>