# Part 1 : Most simplest LAN

### 3. Know your MAC
🌞 Déterminer l'adresse MAC de vos deux machines
```
PC1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC1    0.0.0.0/0            0.0.0.0           00:50:79:66:68:00  10001  127.0.0.1:10002
       fe80::250:79ff:fe66:6800/64

```

```
PC2> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC2    0.0.0.0/0            0.0.0.0           00:50:79:66:68:01  10004  127.0.0.1:10005
       fe80::250:79ff:fe66:6801/64

```

### 4. IP Setup
🌞 Définir une IP statique sur les deux machines

```
PC1> ip 10.1.1.1/24
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0

PC1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC1    10.1.1.1/24          0.0.0.0           00:50:79:66:68:00  10001  127.0.0.1:10002
       fe80::250:79ff:fe66:6800/64
```

```
PC2> ip 10.1.1.2/24
Checking for duplicate address...
PC1 : 10.1.1.2 255.255.255.0

PC2> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC2    10.1.1.2/24          0.0.0.0           00:50:79:66:68:01  10004  127.0.0.1:10005
       fe80::250:79ff:fe66:6801/64

```

🌞 Effectuer un ping d'une machine à l'autre

```
PC1> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=0.465 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=0.623 ms
```

### 5. Analyze
➜ Wireshark !

***à voir dans le fichier :p1_ping.pcapng***

🌞 Protocolz ?

***protocole utilisé : icmp***
