# Part 2 : Bring that switch in¶

### 3. Même chose en fast¶
🌞 Déterminer l'adresse MAC de vos trois machines

```
PC1> ip 10.1.1.1
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0

PC1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC1    10.1.1.1/24          0.0.0.0           00:50:79:66:68:00  10004  127.0.0.1:10005
       fe80::250:79ff:fe66:6801/64
```

```
PC2> ip 10.1.1.2
Checking for duplicate address...
PC1 : 10.1.1.2 255.255.255.0
PC2> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC2    10.1.1.2/24          0.0.0.0           00:50:79:66:68:01  10000  127.0.0.1:10001
       fe80::250:79ff:fe66:6800/64
```

```
PC3> ip 10.1.1.3
Checking for duplicate address...
PC1 : 10.1.1.3 255.255.255.0

PC3> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC3    10.1.1.3/24          0.0.0.0           00:50:79:66:68:02  10006  127.0.0.1:10007
       fe80::250:79ff:fe66:6802/64
```

🌞 Effectuer des ping d'une machine à l'autre

```
PC1> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=1.498 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=2.181 ms
```

```
PC2> ping 10.1.1.3
84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=1.436 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=1.107 ms
```

```
PC1> ping 10.1.1.3
84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=0.382 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=0.777 ms
```

### 4. ARP old friend

🌞 Afficher la table ARP de node1

```
PC1> show arp

00:50:79:66:68:01  10.1.1.2 expires in 103 seconds
00:50:79:66:68:02  10.1.1.3 expires in 114 seconds
```

➜ Capturer un échange ARP

📁 p2_arp_node2.pcap

📁 p2_arp_node3.pcap
