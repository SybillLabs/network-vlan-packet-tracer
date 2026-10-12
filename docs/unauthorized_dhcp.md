<h1 align="center">
    🔐 Protection contre un serveur DHCP non autorisé
</h1>

## `> quickstart`
L'**objectif** est de protéger l'infrastructure d'un `FAKE-SRV-DHCP`.

## `> configuration_FAKE-SRV-DHCP`
![alt text](/screenshots/image-19.png)

## `> configuration_snooping`
> Configuration à appliquer sur `SW-E1` et `SW-E2`

```
configure terminal
# 1. Activation globale du DHCP Snooping
ip dhcp snooping
# 2. Activation du filtrage spécifiquement sur vos VLANs
ip dhcp snooping vlan 10,20,30
# 3. Déclaration du port Trunk comme étant "De confiance" (Reçoit le serveur 
légitime)
interface fastEthernet 0/24
ip dhcp snooping trust
end
write
```

## `> validation`
Le **port Fa0/7** où se trouve le pirate n'a pas besoin de configuration spécifique, car par défaut, tous les ports non configurés deviennent automatiquement **Untrusted**.

![alt text](/screenshots/image-20.png)

> **Note** : Sur CiscoPacketTracer, je suis bien branché en Fa0/7 mais la commande me mets sur le port Fa0/8. Cela peut être dû à un bug de simulatin de Cisco.

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>