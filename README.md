<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d0d0d,100:1a1a2e&fontColor=FF003C&fontSize=48&height=160&width=900&text=Network%20VLAN%20Packet%20Tracer&section=header&animation=fadeIn" alt="Header"/>
</p>

## `> tech_stack`
![Static Badge](https://img.shields.io/badge/Cisco%20Packet%20Tracer-t?logo=cisco&logoColor=white&color=%231BA0D7)

## `> overview`
Mise en œuvre complète d'une infrastructure réseau segmentée : adressage VLSM, VLANs, routage inter-VLAN, OSPF sur liaison WAN, services DHCP/DNS/NTP et politiques de sécurité (SSH restreint, ACL, port-security, DHCP snooping).

Maquette réalisée sur **Cisco Packet Tracer**. Le fichier de laboratoire est disponible dans `lab/topology.pkt` et les comptes rendus par domaine technique dans `docs/`.

> Ce dépôt est référencé depuis [**SysNet Practice Labs**](https://github.com/SybillLabs/sysnet-practice-labs.git), le hub central de mes labs d'administration d'infrastructure sécurisée.

## `> initial_model`
![image](/screenshots/image.png)

## `> model_perimeter`

| Exigence                                                 | Mise en œuvre                                                |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| Segmentation en 4 VLAN (PROD, GESTION, DIRECTION, ADMIN) | VLSM sur 172.16.10.0/24, ports access répartis sur SW-E1/E2  |
| Routage inter-VLAN                                       | Router-on-a-stick sur RTR-INTERNE, sous-interfaces dot1Q     |
| Adressage automatique des postes                         | DHCP centralisé sur SRV-DHCP-DNS, 3 pools                    |
| Publication interne                                      | SRV-WEB 192.168.200.1, résolution DNS www.ais.fr             |
| Interconnexion des sites                                 | Liaison série /30, OSPF process 1, area 0                    |
| Administration à distance                                | SSH uniquement, ACL vty (VLAN 99 + PC-NOMADE), Telnet refusé |
| Isolation PROD/GESTION                                   | ACL étendue 101 sur sous-interfaces VLAN 10/20               |
| Accès web restreint                                      | ACL 102 : HTTP/HTTPS refusés aux VLAN 10/20                  |
| Filtrage DNS ciblé                                       | ACL 103 : UDP/53 bloqué pour le VLAN 30                      |
| Contrôle des accès physiques                             | Port-security sticky + shutdown sur Fa0/1 (SW-E1)            |
| Protection DHCP                                          | DHCP snooping VLANs 10/20/30, ports trunk trusted            |
| Horloge équipements                                      | NTP vers SRV-DHCP-DNS (192.168.200.2)                        |

## `> equipment`

| Equipement    | Rôle                           | IP de management (VLAN 99) |
| ------------- | ------------------------------ | -------------------------- |
| RTR-INTERNE   | Routage inter-VLAN, OSPF, ACL  | 172.16.10.222 (GW)         |
| RTR-EXTERNE   | Routage site distant, OSPF     | 192.168.1.254              |
| SW-DISTRIB    | Switch de distribution, trunks | 172.16.10.221              |
| SW-E1 / SW-E2 | Switches d'accès utilisateurs  | 172.16.10.220 / .219       |
| SRV-DHCP-DNS  | DHCP, DNS, NTP                 | 192.168.200.2              |
| SRV-WEB       | Serveur HTTP interne           | 192.168.200.1              |

## `> documents`

1. [**Plan d'adressage VLSM**](/docs/vlsm.md)
2. [**Configuration initiale de `SW-DISTRIB`**](/docs/sw-distrib.md)
3. [**VLAN et affectation des ports**](/docs/vlan.md)
4. [**Routage inter-VLAN**](/docs/inter-vlan.md)
5. [**VLAN 99 - Administration**](/docs/vlan99.md)
6. [**Service DHCP**](/docs/dhcp.md)
7. [**DNS et Serveur web**](/docs/dns_serveur-web.md)
8. [**Liaison WAN et routage OSPF**](/docs/wan_ospf.md)
9. [**Administration distante sécurisée**](/docs/secure_remote.md)
10. [**Isolation des VLANs PROD & GESTION**](/docs/isolation_VLANs.md)
11. [**Contrôle d'accès au serveur web**](/docs/serveur_web.md)
12. [**Test de filtrage DNS**](/docs/dns_filtering.md)
13. [**Port Security - PC1 PROD**](/docs/pc1_prod.md)
14. [**Protection contre un serveur DHCP non autorisé**](/docs/unauthorized_dhcp.md)
15. [**Synchronisation horaire**](/docs/ntp.md)

## `> final_model`
![image-23](/screenshots/image-23.png)

---

<p align="center">
    <a href="https://github.com/SybillLabs">
    <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,100:0d0d0d&fontColor=FF003C&fontSize=32&height=100&width=900&text=%5BEOF%20-%20From%20SybillLabs%5D&section=footer"/>
    </a>
</p>