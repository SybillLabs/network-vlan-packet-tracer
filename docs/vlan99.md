<h1 align="center">
    🌐 VLAN 99 - Administration
</h1>

## `> quickstart`
L'**objectif** est de donner des adresses IP statiques aux PC du VLAN 99, rendre les switches administrables dans le VLAN 99.

## `> equipment`

| Equipement | Adresse IP    | CIDR | Gateway       | Broadcast     |
| ---------- | ------------- | ---- | ------------- | ------------- |
| PC1-ADMIN  | 172.16.10.209 | /28  | 172.16.10.222 | 172.16.10.223 |
| PC2-ADMIN  | 172.16.10.210 | /28  | 172.16.10.222 | 172.16.10.223 |
| SW-DISTRIB | 172.16.10.221 | /28  | 172.16.10.222 | 172.16.10.223 |
| SW-E1      | 172.16.10.220 | /28  | 172.16.10.222 | 172.16.10.223 |
| SW-E1      | 172.16.10.219 | /28  | 172.16.10.222 | 172.16.10.223 |

## `> configuration` 
### A appliqué sur les 3 switches

```
configure terminal
    interface vlan 99   
        ip address "adresse IP d'un des trois switches" 255.255.255.24
        no shutdown
        exit
    ip default-gateway 172.16.10.222
    end
write
```

### Validation par test de ping
![image-7](/screenshots/image-7.png)
---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>