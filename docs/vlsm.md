<h1 align="center">
    📝 Plan d'adressage VLSM
</h1>

## `> quickstart`
Le réseau global `172.16.10.0/24` est découpé en VLSM pour répondre aux exigences de segmentation par VLAN, avec une optimisation des plages d’adresses et une marge pour l’évolution.

## `> the_needs`
| VLAN | Nom       | Nombre d'hôtes |
| ---- | --------- | -------------- |
| 10   | PROD      | 100            |
| 20   | GESTION   | 50             |
| 30   | DIRECTION | 12             |
| 99   | ADMIN/DSI | 7              |

## `> adressing_plan`

| VLAN | Réseau        | CIDR | Masque          | Première IP   | Dernière IP (GW) | Broadcast     |
| ---- | ------------- | ---- | --------------- | ------------- | ---------------- | ------------- |
| 10   | 172.16.10.0   | /25  | 255.255.255.128 | 172.16.10.1   | 172.16.10.126    | 172.16.10.127 |
| 20   | 172.16.10.128 | /26  | 255.255.255.192 | 172.16.10.129 | 172.16.10.190    | 172.16.10.191 |
| 30   | 172.16.10.192 | /28  | 255.255.255.240 | 172.16.10.193 | 172.16.10.206    | 172.16.10.207 |
| 99   | 172.16.10.208 | /28  | 255.255.255.240 | 172.16.10.209 | 172.16.10.222    | 172.16.10.223 |

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>