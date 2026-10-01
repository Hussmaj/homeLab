# pfSense

pfSense fungerer som gateway, DHCP-server, DNS, router og brannmur i labben.

## Nettverksgrensesnitt

| Interface | Nettverk | IP-adresse | Funksjon |
|---|---|---|---|
| WAN | VirtualBox NAT | DHCP | Tilkobling mot Internett |
| LAN | LAN | `192.168.10.1/24` | Administrasjon |
| VLAN 10 | SERVERS | `192.168.20.1/24` | Gateway for servernettverket |
| VLAN 20 | CLIENTS | `192.168.30.1/24` | Gateway for klientnettverket |
| VLAN 30 | DMZ | `192.168.40.1/24` | Gateway for DMZ |

VLAN 10, 20 og 30 er opprettet på `em0`. `em0` er nettverkskortet som brukes som parent for VLAN 10, 20 og 30.

## DHCP

DHCP brukes for automatisk tildeling av IP-adresser til klienter og DMZ.

- CLIENTS: `192.168.30.100–200`
- DMZ: `192.168.40.100–200`

## Brannmur

pfSense brukes til å kontrollere trafikken mellom de ulike nettverkene og mellom labben og Internett.
