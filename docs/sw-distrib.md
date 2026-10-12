<h1 align="center">
    ⇆ Configuration intiale de SW-DISTRIB
</h1>

## `> quickstart`
L'**objectif** est de sécuriser l'accès initial, désactiver les services inutiles, et préparer l’équipement pour une intégration dans l’infrastructure.

## `> identification and security`
- Configuration de l'identification de l'équipement
- Sécurisation de l'accès privilégié et de la console
- Ajout d'une bannière d'avertissement
- Configuration d'évitement de recherche DNS inutiles provoquées par erreur de saisie

```
enable
configure terminal
hostname SW-DISTRIB
enable secret <MDP_CHIFFRE>
line console 0
password <MDP_CONSOLE>
login
exit
banner motd #ACCES RESTREINT AU SEUL PERSONNEL AUTORISE#
no ip domain-lookup
end
write memory
```

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>