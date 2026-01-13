# Part 3 : DHCP is a nice guy

### 3. Setuuuup

🌞 Installer un serveur DHCP

```
sudo dnf install -y dnsmasq

sudo nano /etc/dnsmasq.conf

interface=enp0s3
dhcp-range=10.1.1.10,10.1.1.50,255.255.255.0,12h
dhcp-lease-max=40
dhcp-leasefile=/var/lib/dnsmasq/dnsmasq.leases
```

### 4. Proof or you're lying
🌞 Récupérer une IP automatiquement depuis les 3 nodes

```
PC1> dhcp
DORA IP 10.1.1.45/24 GW 10.1.1.253

PC1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC1    10.1.1.45/24         10.1.1.253        00:50:79:66:68:00  10008  127.0.0.1:10009
       fe80::250:79ff:fe66:6800/64
```

```
PC2> dhcp
DDORA IP 10.1.1.46/24 GW 10.1.1.253

PC2> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC2    10.1.1.46/24         10.1.1.253        00:50:79:66:68:01  10010  127.0.0.1:10011
       fe80::250:79ff:fe66:6801/64
```

```
PC3> dhcp
DDORA IP 10.1.1.47/24 GW 10.1.1.253

PC3> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC3    10.1.1.47/24         10.1.1.253        00:50:79:66:68:02  10012  127.0.0.1:10013
       fe80::250:79ff:fe66:6802/64
```

➜ Wireshark !

📁 p3_dhcp.pcap

### 5. DHCP lease

🌞 Bail DHCP

```
sudo cat /var/lib/dnsmasq/dnsmasq.leases
1767666650 00:50:79:66:68:02 10.1.1.47 PC31 01:00:50:79:66:68:02
1767666680 00:50:79:66:68:01 10.1.1.46 PC21 01:00:50:79:66:68:01
1767666717 00:50:79:66:68:00 10.1.1.45 PC11 01:00:50:79:66:68:00
```

🌞 Use grep

```
1767666717 00:50:79:66:68:00 10.1.1.45 PC11 01:00:50:79:66:68:00
```