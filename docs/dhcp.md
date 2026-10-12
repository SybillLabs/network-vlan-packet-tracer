<h1 align="center">
    🌐 Service DHCP
</h1>

## `> quickstart`
L'**objectif** est de mettre en place le serveur DHCP-DNS (`192.168.200.2/24`) qui fournira la configuration IPv4 aux postes des VLANs 10,20,30. Les clients recevront : adresse ip, masque de sous-réseau, passerelle et serveur DNS.

## `> pool_configuration`

| Pool Name      | Default Gateway | DNS Server    | Start IP Address | Subnet Mask     | Max. N° Users |
| -------------- | --------------- | ------------- | ---------------- | --------------- | ------------- |
| POOL-PROD      | 172.16.10.126   | 192.168.200.2 | 172.16.10.1      | 255.255.255.128 | 124           |
| POOL-GESTION   | 172.16.10.190   | 192.168.200.2 | 172.16.10.129    | 255.255.255.192 | 60            |
| POOL-DIRECTION | 172.16.10.206   | 192.168.200.2 | 172.16.10.193    | 255.255.255.240 | 12            |

![alt text](/screenshots/image-3.png)

## `> validation`
> Suppression des adresses ip statiques si existantes dans les pool concernées, activation du mode **DHCP**.

![alt text](/screenshots/image-5.png)  
![alt text](/screenshots/image-6.png)

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>