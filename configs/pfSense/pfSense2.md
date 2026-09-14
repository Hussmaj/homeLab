# Oppsett av pfSense som gateway og ruter

## Oppdaterte IP-Adresser:

<img width="720" height="131" alt="image" src="https://github.com/user-attachments/assets/63c3e035-acca-48db-8686-ea8430c137f5" />


## Forklaring av IP-adressene:

**WAN:** 10.0.2.15 Dette er IP-adressen pfSense får fra VirtualBox sitt NAT-nettverk. Den brukes av pfSense for å kommunisere ut mot Internett.

**LAN-gateway:** 192.168.10.1/24 Dette er IP-adressen til pfSense på klientnettverket. Windows-klienten bruker denne adressen som standard gateway når den skal kommunisere med andre nettverk eller Internett.

**VLAN 10-gateway:** 192.168.20.1/24 Dette er IP-adressen til pfSense på servernettverket. Ubuntu Server bruker denne som gateway for trafikk ut av VLAN 10.

**Windows-klient:** 192.168.10.100 Dette er IP-adressen til Windows-maskinen på LAN-nettverket. Adressen blir tildelt fra DHCP-serveren på pfSense.

**Ubuntu Server:** 192.168.20.100 Dette er IP-adressen Ubuntu Server får fra DHCP-serveren på VLAN 10. Serveren bruker VLAN 10 for å kommunisere med pfSense og andre nettverk.

OPT1 har ingen IP-adresse fordi det bare er det fysiske parent-interfacet som brukes til VLAN-konfigurasjonen.

### Trafikken beveger seg slik:

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
