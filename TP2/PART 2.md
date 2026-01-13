# TP2 Part2 : C'est mieux avec internet

### 1. Accès internet routeur
A réaliser sur le routeur Cisco r1.tp2.efrei.

➜ Configurer une adresse IP sur l'interface qui pointe vers le nuage GNS3

il faut récupérer une adresse IP en DHCP
vérifier que vous avez bien récupéré une adresse IP avec un show ip int br en mode enable
🌞 Prouver que...

```
PC1> ping 1.1.1.1
1.1.1.1 icmp_seq=1 timeout
1.1.1.1 icmp_seq=2 timeout
1.1.1.1 icmp_seq=3 timeout
1.1.1.1 icmp_seq=4 timeout
1.1.1.1 icmp_seq=5 timeout
```
➜ Wireshark this

lancer Wireshark sur le câble entre r1.tp2.efrei et le nuage GNS
capturer un ping de node1 vers 1.1.1.1
vous devriez le voir passer, mais jamais de réponse
si vous voulez capter ce qu'il se passe :

regardez l'adresse IP source du paquet ping
vous devriez voir l'adresse IP de node1
📁 p1_no_nat.pcap

### 2. Accès internet clients
➜ Configurer un NAT simpliste sur votre routeur

référez-vous toujours au mémo Cisco pour ça
l'interface "externe" (outside) est celle qui pointe vers internet (le nuage GNS)
les interfaces "internes" (inside) sont celle qui pointent vers les LANs
🌞 Proooooooooof or lie

```
PC1> ping 1.1.1.1
84 bytes from 1.1.1.1 icmp_seq=1 ttl=253 time=65.353 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=253 time=26.833 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=253 time=25.785 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=253 time=44.414 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=253 time=33.990 ms
```

```
PC2> ping 1.1.1.1
84 bytes from 1.1.1.1 icmp_seq=1 ttl=253 time=71.069 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=253 time=33.227 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=253 time=26.089 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=253 time=23.254 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=253 time=31.590 ms
```
➜ Wireshark this

lancer Wireshark sur le câble entre r1.tp2.efrei et le nuage GNS
capturer un ping de node1 vers 1.1.1.1
vous devriez le voir passer, avec une réponse cette fois
si vous voulez capter ce qu'il se passe :

regardez l'adresse IP source du paquet ping
vous devriez voir l'adresse IP de r1 : r1 a modifié le paquet pour mettre sa propre IP : c'est le NAT en action
📁 p1_nat.pcap

➜ Gimme the config !

c'était la dernière conf routeur pour ce TP
je veux la running-config dans le compte-rendu
📁 r1_running_config.txt

contient toute la running-config de r1

### 3. Vrai accès internet clients

🌞 Prove it

```
PC1> ip dns 1.1.1.1

PC1> ping efrei.fr
efrei.fr resolved to 51.210.229.203
84 bytes from 51.210.229.203 icmp_seq=1 ttl=253 time=61.881 ms
84 bytes from 51.210.229.203 icmp_seq=2 ttl=253 time=28.919 ms
```

### 4. DHCP again

🌞 Test test test : ajouter un nouveau VPCS au LAN1, le bro node5.tp2.efrei
```
PC5> ip dhcp
DDORA IP 10.2.1.164/24 GW 10.2.1.254

PC5> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC5    10.2.1.164/24        10.2.1.254        00:50:79:66:68:04  10014  127.0.0.1:10015
       fe80::250:79ff:fe66:6804/64

PC5>
PC5> ping efrei.fr
efrei.fr resolved to 51.210.229.203
84 bytes from 51.210.229.203 icmp_seq=1 ttl=253 time=43.092 ms
84 bytes from 51.210.229.203 icmp_seq=3 ttl=253 time=110.143 ms
84 bytes from 51.210.229.203 icmp_seq=4 ttl=253 time=126.032 ms
84 bytes from 51.210.229.203 icmp_seq=5 ttl=253 time=130.935 ms
```