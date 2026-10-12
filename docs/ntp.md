<h1 align="center">
    🕒 Synchronisation horaire
</h1>

## `> quickstart`
L'**objectif** est d'ajouter le service **NTP** sur `SRV-DHCP-DNS` avec synchronisation des équipements `RTR-INTERNE`, `SW-DISTRIB`, `SW-E1` et `SW-E2`.

## `> configuration_SRV-DHCP-DNS`
![alt text](/screenshots/image-21.png)

## `> configuration`
> A appliquer sur `RTR-INTERNE`, `SW-DISTRIB`, `SW-E1` et `SW-E2`
```
configure terminal
ntp server 192.168.200.2
end
write
```

## `> validation`
> A faire sur `RTR-INTERNE`, `SW-DISTRIB`, `SW-E1` et `SW-E2`
```
show ntp status
show ntp associations
show clock
```
![alt text](/screenshots/image-22.png)

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/network-vlan-packet-tracer.git"> Network VLAN Packet Tracer</a></i>
</p>