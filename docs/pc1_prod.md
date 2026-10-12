<h1 align="center">
    🔐 Port Security - PC1 PROD
</h1>

## `> quickstart`
L'**objectif** est de sécuriser le port Fa0/1 de `SW-E1` sur lequel est connecté **PC1-PROD**. Une seule adresse MAC doit être autorisée, l’adresse MAC du poste légitime doit être apprise automatiquement et conservée dans la configuration.  
Utilisation de **PC VIOLATION** pour simuler le remplacement du poste autorisé par un poste non autorisé. En cas de violation, le port doit devenir inutilisable et rester indisponible jusqu’à l’intervention d’un administrateur, même si le poste légitime est reconnecté.

## `> configuration_SW-E1`
```
configure terminal
interface fastEthernet 0/1
    switchport mode access                          # Car le VLAN est en access
    switchport port-security
    switchport port-security maximum 1              # Limite le nombre d'adresse MAC autorisées à 1
    switchport port-security mac-address sticky     # Le switch écoute le réseau et apprends automatiquement l'adresse MAC du premier PC connecté et l'inscrit directement.
    switchport port-security violation shutdown     # En cas d'intrusion, le port se désactive complètement.
end
write
```

## `> simulation_violation`
- Générer du trafic depuis PC1-PROD, pour le rendre légitime
- Débrancher PC1-PROD, puis brancher PC-VIOLATION sur le même port
- Générer du trafic depuis PC-VIOLATION pour l'intrusion.

![alt text](/screenshots/image-16.png)  

## `> port-recovery`
```
configure terminal
interface fastEthernet 0/1
    shutdown                    # Interface réinitialisé
    no shutdown
    end
write
```

![alt text](/screenshots/image-18.png)

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>