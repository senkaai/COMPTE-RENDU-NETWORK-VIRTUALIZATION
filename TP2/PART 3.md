# TP2 Part3 : Time to attack all this¶

### 3. ARP spoofing
➜ Avec du ARP spoofing, mener une attaque MITM entre node1 et r1

je recommande toujours arpspoof, but as you want
➜ You guessed it : Wireshark this

lancez Wireshark sur la machine attaquante
directement sur la machine attaquante, pas depuis GNS
capturez le trafic qui circule quand node1 envoie des ping vers efrei.fr
Tip
En ligne de commande, y'a la commande tcpdump qui permet d'effectuer des captures réseau.
Pas besoin de sortir Wireshark et son interface graphique dans une VM quoi !

📁 p3_arp_mitm.pcap

on doit voir un beau spam de ARP (vers la passerelle, et vers le client victime node1)
on doit voir des ping qui viennent de node1 et qui vont vers l'adresse IP publique qui correspond à efrei.fr
ha et du coup on doit aussi voir la requête DNS du client qui est partie vers 1.1.1.1, avec la réponse
Note
La requête DNS est envoyée automatiquement et spontanément par un client qui a besoin de contacter un nom de domaine ; comme ici efrei.fr.
Vous la trouverez donc forcément avant les ping : le client doit la faire avant pour apprendre l'adresse IP de efrei.fr.
La réponse du serveur DNS (vous pouvez le voir dans Wireshark si vous êtes attentifs), c'est l'adresse IP qui correspond à efrei.fr.
Une fois la réponse reçue, le client a appris l'adresse IP du serveur efrei.fr et peut donc envoyer des ping vers cette adresse.

### 4. DHCP spoofing

De toute évideeeeence, coupez votre attaque ARP en cours avant de procéder à la suite, et mener la deuxième attaque.
Bah ouais, dans les deux cas on finit en MITM, pas utile de faire les deux.
T'envoies pas deux équipes de cambriolage différentes cambrioler la même banque, si ? T'es tordu. Comment ça j'suis tordu ?

➜ Installer votre rogue DHCP server

il doit attribuer des adresses IP dans la range 10.2.1.201 - 10.2.1.250
il doit indiquer que la passerelle du réseau, bah c'est lui-même : l'attaquant
pour le DNS : indique 1.1.1.1 pour le moment (comme ça ton client conserve un accès internet normal)
B. Proofs
🌞 Test test test : ajouter un nouveau VPCS au LAN1, le bro node6.tp2.efrei

```
PC6> ip dhcp
DDORA IP 10.2.1.165/24 GW 10.2.1.254

PC6> show ip

NAME        : PC6[1]
IP/MASK     : 10.2.1.165/24
GATEWAY     : 10.2.1.254
DNS         : 1.1.1.1
DHCP SERVER : 10.2.1.253
DHCP LEASE  : 43198, 43200/21600/37800
MAC         : 00:50:79:66:68:05
LPORT       : 10024
RHOST:PORT  : 127.0.0.1:10025
MTU:        : 1500

PC6> ping efrei.fr
efrei.fr resolved to 51.210.229.203
84 bytes from 51.210.229.203 icmp_seq=1 ttl=253 time=77.764 ms
84 bytes from 51.210.229.203 icmp_seq=2 ttl=253 time=142.017 ms
84 bytes from 51.210.229.203 icmp_seq=3 ttl=253 time=122.266 ms
84 bytes from 51.210.229.203 icmp_seq=4 ttl=253 time=116.992 ms
84 bytes from 51.210.229.203 icmp_seq=5 ttl=253 time=126.391 ms
```
➜ You guessed it : Wireshark this

lancez Wireshark sur la machine attaquante
directement sur la machine attaquante, pas depuis GNS
capturez le trafic qui circule quand node6 envoie des ping vers efrei.fr
📁 p3_dhcp_mitm.pcap

on doit voir un DORA où vous gagnez la course contre le serveur DHCP légitime du réseau
on doit voir des ping qui viennent de node6 et qui vont vers l'adresse IP publique qui correspond à efrei.fr
ha et du coup on doit aussi voir la requête DNS du client qui est partie vers 1.1.1.1, avec la réponse

**MALHEUREUSEMENT J'AI UTILISER ARPING POUR FAIRE TOUT ÇA, C'EST COMPLÈTEMENT NUL, MAIS J'AI PAS EU LE TEMPS DE CHANGER DE VM POUR PASSER SUR AUTRE CHOSE QUE LA BONNE VIEILLE ROCKY...🙏** 