# Oppsett av pfSense som gateway og ruter

## Oppdaterte IP-Adresser:

<img width="694" height="122" alt="image" src="https://github.com/user-attachments/assets/fa10a579-a1bb-4fa9-a9e4-b05b167ec151" />

Trafikken beveger seg slik:

```text
Ubuntu Server
   │
VLAN 10-tagget trafikk
   │
em0
   │
em0.10
   │
OPT2 / SERVERS
192.168.20.1
```
