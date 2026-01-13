# TP2 Part1 : Network Setup¶

### 7. Proof or lie
🌞 Tout le monde doit pouvoir se ping
```
PC1> ping 10.2.1.12
84 bytes from 10.2.1.12 icmp_seq=1 ttl=64 time=3.994 ms
84 bytes from 10.2.1.12 icmp_seq=2 ttl=64 time=5.589 ms
84 bytes from 10.2.1.12 icmp_seq=3 ttl=64 time=9.177 ms
84 bytes from 10.2.1.12 icmp_seq=4 ttl=64 time=3.655 ms
84 bytes from 10.2.1.12 icmp_seq=5 ttl=64 time=3.203 ms
```

```
PC3> ping 10.2.2.12
84 bytes from 10.2.2.12 icmp_seq=1 ttl=64 time=3.583 ms
84 bytes from 10.2.2.12 icmp_seq=2 ttl=64 time=9.952 ms
84 bytes from 10.2.2.12 icmp_seq=3 ttl=64 time=5.351 ms
84 bytes from 10.2.2.12 icmp_seq=4 ttl=64 time=5.272 ms
84 bytes from 10.2.2.12 icmp_seq=5 ttl=64 time=5.177 ms
```

```
PC1> ping 10.2.2.11
84 bytes from 10.2.2.11 icmp_seq=1 ttl=63 time=31.374 ms
84 bytes from 10.2.2.11 icmp_seq=2 ttl=63 time=15.700 ms
84 bytes from 10.2.2.11 icmp_seq=3 ttl=63 time=27.242 ms
84 bytes from 10.2.2.11 icmp_seq=4 ttl=63 time=18.941 ms
84 bytes from 10.2.2.11 icmp_seq=5 ttl=63 time=23.147 ms
```

```
PC4> ping 10.2.1.12
84 bytes from 10.2.1.12 icmp_seq=1 ttl=63 time=55.801 ms
84 bytes from 10.2.1.12 icmp_seq=2 ttl=63 time=34.983 ms
84 bytes from 10.2.1.12 icmp_seq=3 ttl=63 time=25.234 ms
84 bytes from 10.2.1.12 icmp_seq=4 ttl=63 time=28.922 ms
84 bytes from 10.2.1.12 icmp_seq=5 ttl=63 time=24.571 ms
```

➜ Wireshark this shiet

capture Wireshark du câble entre le routeur et le switch
on doit y voir des ping qui vont du LAN1 au LAN2 (peu importe qui ping qui)
📁 p1_routed_ping.pcap